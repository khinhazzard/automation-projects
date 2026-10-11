Trigger this workflow when all of these are met:
→ The check_inventory action confirms that the requested product was found in inventory (found = true) and is currently out of stock (available = false).
→ The customer has been informed that the item is out of stock.
→ The customer has agreed to a back-in-stock follow-up.
→ The Extract Product / Model Requested action has completed.