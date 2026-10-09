BluePeak Plumbing & Water Heating
Voice AI Essential Test Cases — Expected Results

TEST 1 — BASIC KNOWLEDGE BASE QUESTION
Question:
“Hi, do you install tankless water heaters?”

Expected result:
- Answers using the configured Knowledge Base.
- Does not trigger an inventory lookup or attempt to book an appointment.
- Gives a concise, relevant answer without inventing unsupported service details.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TEST 2 — SERVICE KNOWLEDGE BASE QUESTION
Question:
“Do you replace water heaters?”

Expected result:
- Answers using the configured Knowledge Base. The supported answer is that BluePeak can help with water heater replacement.
- Does not invent detailed steps, prices, guarantees, or policies not in the Knowledge Base.
- After the call, verify that the post-call workflow runs and applies the “BluePeak - Voice AI” tag to the contact.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TEST 3 — APPOINTMENT SCHEDULE / AVAILABILITY
Question:
“I’d like to schedule an appointment for a water heater replacement. What hours are available?”
Follow-up:
“Thanks, I’ll think about it and get back to you.”

Expected result:
- Uses the BluePeak Service Appointments calendar to provide availability.
- Offers only slots returned by the configured calendar. Verify that the options are within the intended local schedule (Monday–Friday, 8:00 AM–5:00 PM) and do not include evenings, midnight, or weekends.
- Does not book an appointment because the caller declines to proceed.
- Does not pressure the caller to book.
- Observe whether it collects contact details or offers follow-up; assess this against the intended contact-creation behavior.
- If the calendar returns incorrect times, record the exact times and check calendar/staff timezone settings before changing the prompt.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TEST 4 — AVAILABLE INVENTORY
Question:
“Do you have a Water Heater Anode Rod available?”

Expected result:
- Calls the check_inventory action with the exact supported item name.
- Based on the current test data, reports the item as available, with quantity 8 if the inventory sheet has not changed.
- Does not rely on the Knowledge Base for live stock information.
- Verify the action result in the tool log if available.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TEST 5 — OUT-OF-STOCK INVENTORY
Question:
“Do you have a Gas Control Valve available?”

Expected result:
- Calls check_inventory with the exact supported item name.
- Based on the current test data, reports the item as unavailable / out of stock, with quantity 0 if the inventory sheet has not changed.
- Verify that the “BluePeak - Out of Stock Internal Notification” workflow is triggered and that the internal notification contains the correct item and stock details.
- Does not say the item was not found if the tool returns found=true and available=false.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

TEST 6 — AMBIGUOUS INVENTORY ITEM
Question:
“Do you have a 50-gallon gas water heater?”

Expected result:
- Recognizes that the wording could refer to more than one supported product.
- Asks which product the caller means rather than choosing one without confirmation.
- Supported gas water heater options are “Rheem 50 Gal Gas Water Heater” and “Bradford White 50 Gal Gas Water Heater.”
- After the caller confirms “Rheem 50 Gal Gas Water Heater,” checks inventory using that exact supported name.
- Based on the current test data, the Rheem item has quantity 0; if the sheet has not changed, it should report unavailable / out of stock.
- Do not require the agent to ask “Which brands do you carry?” as its clarification; if it asks a different clear question that distinguishes the two supported products, that is acceptable.
- Verify the exact item sent to the action and the returned result.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

OVERALL PASS CRITERIA
- No invented service details, appointment times, stock status, or quantities.
- Correct tool use: calendar for availability; check_inventory for current stock.
- No appointment is claimed booked unless booking succeeds.
- No inventory lookup for general Knowledge Base questions.
- Out-of-stock workflow and post-call contact-tag workflow are verified separately.
- Record failures with the exact spoken response and, where available, the corresponding tool/workflow result.

TEST DATA NOTE
Inventory quantities above reflect the latest known test data and may change. Confirm the current Google Sheet before treating a quantity as a definitive expected result.
