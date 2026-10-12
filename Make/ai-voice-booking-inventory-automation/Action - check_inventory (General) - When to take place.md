Call this action only when the caller asks about a product's current stock, availability, or quantity.

Before calling, identify the exact product in the dedicated product catalog table in the configured Knowledge Base. Copy the SKU directly from the same row as the matched product and send it in the `sku` field.

Never guess, infer, construct, or substitute a SKU. If the exact product and its SKU cannot be verified, do not call this action; ask the caller to clarify or offer human assistance.