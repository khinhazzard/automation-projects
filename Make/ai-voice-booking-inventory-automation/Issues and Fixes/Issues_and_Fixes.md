The Errors:

• Voice AI sent webhook data with different casing even though the item wording was the same, causing Make.com to fail the inventory match.
Error Type: Data mismatch / input normalization issue

• Voice AI reworded the item requested by the customer. The customer said “Gal,” but the Voice AI agent sent “Gallon” to Make.com.
Error Type: Input transformation / data normalization issue

• Voice AI agent responded too quickly and checked back with the caller too quickly.
Error Type: Conversation timing / UX issue

• Knowledge Base and Google Sheets Inventory discrepancy.
Error Type: Data consistency / source-of-truth discrepancy

~~~~~~~~~~~~~~~~~~~~~~~~~~
The Fixes:
→ when a customer asks for an item, we make the voice AI validate that item from knowledge base, and use the exact wording found in knowledge base before checking inventory and send it those exact wordings to make via webhook. This way we save make credits, if customer asks for an item that is not from knowledge base, then for sure it's not from the inventory as well, then no need to send webhook to make

→ Made the Google Sheets and Table from Knowledge base exactly the same with the wordings

→ Added lowercase normalization to both sides of the Make filter so inventory matching is no longer affected by casing differences

→ Set Wait before speaking from 0 to 0.5

→ Set Idle frequency timer from 4 secs to 5 secs, then reminder from 1x to 2x

→ Updated Calendar Timezone

→ fixed conflicting "Gallon" and "Gal" wordings from PDF Knowledge base