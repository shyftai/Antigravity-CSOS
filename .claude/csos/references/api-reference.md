# API Reference — CS:OS Supported Tools

Quick reference for making API calls from Claude Code. Auth, base URLs, key endpoints, and safety warnings.

---

## Dangerous Endpoints

**HARD GATE — even in AUTO mode, always stop and confirm before calling any endpoint below.**

**Rules (apply to ALL platforms):**
1. Never delete customer conversation history — it may be needed for disputes or compliance
2. Always prefer closing/archiving tickets over deletion
3. Customer data operations may be subject to GDPR/CCPA — verify before destructive actions
4. Log all destructive API calls in `logs/decisions.md` with full context
5. Never bulk-close or bulk-delete tickets without reviewing each one

---

### Intercom (api.intercom.io)

**Auth:** Bearer token in header `Authorization: Bearer {token}`
**Base URL:** `https://api.intercom.io`

| Endpoint | Blast Radius | Irreversible? | Safe Alternative |
|----------|-------------|---------------|-----------------|
| `DELETE /contacts/{id}` | Permanently deletes a contact and ALL their conversation history. Notes, tags, custom attributes — all gone. | YES | Archive the contact: `POST /contacts/{id}/archive`. |
| `DELETE /contacts/{id}` (GDPR) | Same as above but specifically for GDPR requests. Must comply within 30 days. | YES | Ensure you have the deletion request documented before executing. |
| `POST /contacts/merge` | Merges two contacts. The secondary contact is destroyed. Conversations move to primary. If you merge wrong direction, the primary contact's data is polluted. | YES — cannot unmerge | Verify which contact should be primary BEFORE calling. |
| `DELETE /conversations/{id}/tags/{tagId}` | Removes tag from conversation. If tag was used for routing or automation, the conversation may fall through cracks. | YES | Add a replacement tag before removing the old one. |
| `POST /conversations/{id}/parts` with `type: "close"` | Closes a conversation. Customer is notified (if configured). Cannot be auto-reopened. | NO — can reopen | Close only after resolution is confirmed. |
| `DELETE /data_attributes/{id}` | Deletes a custom data attribute from ALL contacts/companies. Data in that field is lost across your entire database. | YES | Rename or hide the attribute instead. |
| `DELETE /segments/{id}` | Deletes a saved segment. Any automation or campaigns using this segment lose their audience. | YES | Remove segment from automations first, then archive. |

**Unexpected behaviors:**
- **Contact deletion cascades aggressively.** Deleting a contact removes: all conversations, all notes, all events, all custom attributes, all tags. Export data first.
- **Conversation assignment changes** trigger notifications to the new assignee. Bulk reassignment floods inboxes.
- **Rate limit:** 1,000 API calls per minute (83 per app per minute for some endpoints). Exceeding returns 429 with `Retry-After` header.
- **Webhook events fire on closes/updates.** Closing conversations via API triggers the same webhooks as manual closes — may trigger downstream automation.

---

### Zendesk (your-subdomain.zendesk.com/api/v2)

**Auth:** Basic auth (`{email}/token:{api_token}`) or OAuth Bearer token
**Base URL:** `https://{subdomain}.zendesk.com/api/v2`

| Endpoint | Blast Radius | Irreversible? | Safe Alternative |
|----------|-------------|---------------|-----------------|
| `DELETE /tickets/{id}` | Moves ticket to "deleted" status. Can be recovered by admin within 30 days. After 30 days, permanently purged. | 30-day window | Set ticket status to "closed" instead. |
| `DELETE /tickets/destroy_many?ids=1,2,3` | Bulk soft-delete up to 100 tickets per call. Same 30-day recovery window. | 30-day window | Bulk close instead: `PUT /tickets/update_many`. |
| `DELETE /users/{id}` | Soft-deletes a user. Can be recovered within 30 days. After that, permanent. Associated tickets remain but lose the requester link. | 30-day window | Suspend the user instead: `PUT /users/{id}` with `suspended: true`. |
| `DELETE /users/{id}/identities/{identityId}` | Removes an identity (email, phone) from a user. If this was their primary identity, the user becomes unreachable. | YES | Change primary identity to a different one first. |
| `PUT /tickets/{id}` with `status: "closed"` | Closes a ticket permanently. Closed tickets CANNOT be reopened in Zendesk — only new follow-up tickets can be created. | YES — cannot reopen | Use "solved" status instead (can be reopened within 28 days by default). |
| `DELETE /organizations/{id}` | Soft-deletes an organization. All users remain but lose the org association. | 30-day window | Remove users from org individually if needed. |
| `DELETE /macros/{id}` | Deletes a macro. Any trigger or automation referencing it may break silently. | YES | Deactivate macro instead of deleting. |
| `DELETE /triggers/{id}` | Deletes a trigger. Active ticket routing may break. | YES | Deactivate trigger first, monitor for 7 days, then delete. |
| `DELETE /automations/{id}` | Deletes an automation. Scheduled actions stop. | YES | Deactivate instead. |

**Unexpected behaviors:**
- **"Closed" is permanent in Zendesk.** Unlike most platforms, closing a ticket is NOT the same as archiving. Closed tickets cannot be reopened — only new linked tickets can be created. Use "solved" for temporary resolution.
- **Bulk operations are async.** `destroy_many` and `update_many` return a job status URL. The actual deletion happens in the background — you may not see failures immediately.
- **Triggers fire on API updates.** Changing ticket properties via API triggers the same automation as manual changes. Bulk updates can cascade into mass email notifications.
- **Rate limit:** 700 requests per minute (Team/Growth), 2,500 (Professional), 5,000 (Enterprise). Exceeding returns 429.

---

### HubSpot Service Hub (api.hubapi.com)

**Auth:** Bearer token (private app) or OAuth
**Base URL:** `https://api.hubapi.com`

| Endpoint | Blast Radius | Irreversible? | Safe Alternative |
|----------|-------------|---------------|-----------------|
| `POST /crm/v3/objects/tickets/batch/archive` | Archives up to 100 tickets. Goes to recycle bin for 90 days. | 90-day window | Change ticket status/pipeline stage instead. |
| `POST /crm/v3/objects/contacts/gdpr-delete` | Permanent GDPR deletion of contact. All ticket associations severed. Conversation history orphaned. | YES — immediate | Only for genuine GDPR requests. |
| `DELETE /crm/v3/associations/{fromType}/{toType}/batch/archive` | Severs associations between tickets and contacts/companies. Tickets become orphaned — no customer context. | YES | Never bulk-remove associations without review. |

**Same workflow trigger risks as HubSpot CRM — see GTMOS api-reference.md for full details.**

---

### Salesforce Service Cloud (your-instance.salesforce.com)

**Auth:** OAuth 2.0 Bearer token
**Base URL:** `https://{instance}.salesforce.com/services/data/v60.0`

| Endpoint | Blast Radius | Irreversible? | Safe Alternative |
|----------|-------------|---------------|-----------------|
| `DELETE /sobjects/Case/{id}` | Moves case to recycle bin (15 days). All case comments, emails, and attachments go with it. | 15-day window | Close the case instead of deleting. |
| `DELETE /sobjects/Contact/{id}` | Moves contact to recycle bin. All associated cases, activities, and opportunities lose the contact link. | 15-day window | Deactivate or add "Do Not Contact" flag. |
| `POST /composite/batch` | Batch operations (up to 25 subrequests). A single bad request doesn't roll back the others — partial execution. | PARTIAL | Validate all subrequests individually before batching. |
| `DELETE /sobjects/EmailMessage/{id}` | Deletes an email from case history. The email is gone — not in recycle bin. | YES | Never delete customer emails. Archive the case instead. |

**Unexpected behaviors:**
- **Recycle bin is only 15 days** (vs 30 days in most platforms). Set a calendar reminder after any bulk deletion.
- **Validation rules and triggers** fire on API operations identically to UI. Bulk case updates can trigger assignment rules, email alerts, and workflow actions.
- **Rate limit:** Concurrent API request limit varies by edition. Exceeding returns `REQUEST_LIMIT_EXCEEDED`.
- **Governor limits** apply to Apex triggers fired by API calls. Large batch operations can hit limits and fail silently.

---

### Stripe (api.stripe.com) — for billing/subscription management

**Auth:** Bearer token `Authorization: Bearer sk_...`
**Base URL:** `https://api.stripe.com/v1`

Only relevant endpoints for CS operations (refunds, subscription changes):

| Endpoint | Blast Radius | Irreversible? | Safe Alternative |
|----------|-------------|---------------|-----------------|
| `POST /refunds` | Issues a refund. Money moves back to customer. Cannot be reversed once processed. | YES — money moves | Issue credit note or account credit first. Discuss with finance. |
| `DELETE /subscriptions/{id}` | Immediately cancels subscription. Customer loses access. | YES | Use `cancel_at_period_end: true` to cancel at end of billing period instead. |
| `POST /subscriptions/{id}` with plan downgrade | Immediately changes subscription. May issue prorated credit or charge. | NO — can upgrade again | Schedule the change for next billing period. |

**CS:OS should HARD GATE all Stripe operations — refunds and subscription changes are financial decisions.**

---

### Slack (api.slack.com)

**Auth:** Bot token `xoxb-...` or User token `xoxp-...`
**Base URL:** `https://slack.com/api`

| Endpoint | Blast Radius | Irreversible? | Safe Alternative |
|----------|-------------|---------------|-----------------|
| `chat.delete` | Deletes a message. All replies in thread remain but lose parent context. | YES | Edit the message to redact content instead. |
| `conversations.archive` | Archives a channel. Members can still read history but cannot post. | NO — can unarchive | Archive is generally safe. |
| `conversations.kick` | Removes a user from a channel. They lose access to history (private channels). | NO — can re-invite | Remove from channel only if necessary. |
| `admin.conversations.delete` | Permanently deletes an entire channel and ALL message history. Enterprise Grid only. | YES | Archive instead. |

---

### Danger Summary

| Platform | Highest-Risk Endpoint | Worst Case | Recovery |
|----------|----------------------|-----------|----------|
| **Intercom** | `DELETE /contacts/{id}` | Contact + all conversations permanently gone | None |
| **Intercom** | `POST /contacts/merge` | Wrong merge direction, data pollution | None — cannot unmerge |
| **Intercom** | `DELETE /data_attributes/{id}` | Custom field deleted across ALL contacts | None |
| **Zendesk** | `PUT /tickets/{id}` status: "closed" | Ticket permanently closed, cannot reopen | None — use "solved" instead |
| **Zendesk** | `DELETE /triggers/{id}` | Ticket routing breaks silently | None |
| **Salesforce** | `DELETE /sobjects/EmailMessage/{id}` | Customer email permanently deleted | None |
| **Stripe** | `POST /refunds` | Money refunded, cannot reverse | None — money moved |
| **Stripe** | `DELETE /subscriptions/{id}` | Immediate cancellation, customer loses access | None |
| **Slack** | `admin.conversations.delete` | Entire channel + history permanently gone | None |

---

## Notes

- Customer conversation history is often legally required — never delete without compliance review
- Ticket closures in Zendesk are PERMANENT — use "solved" for most cases
- Refunds and subscription changes are financial decisions — always confirm with finance/management
- Log every customer-facing operation in COSTS.md
- For tools not listed here, check the tool's API documentation
