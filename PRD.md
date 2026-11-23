# Hostel Laundry Pickup Tracker

**Product Requirements Document**  
**Course:** BU-209 Backend Engineering — Week 4 Assignment  
**Author:** Oluwapelumi Emmanuel Killa  
**Date:** 23 November 2026  
**Version:** 2.0

## 1. The idea

Handing clothes to a laundry vendor is a small transaction, but several details have to stay clear: the number of clothes, the service requested, the price, and the collection date. If something goes wrong later, both the student and the vendor need a record they can refer to.

Consider a simple example. A student drops off five shirts and two trousers on Monday and expects to collect them on Thursday. Before walking over, the student wants to know whether the order is ready. At the counter, the vendor needs to find the right bundle and check whether the student has paid. If only four shirts come back, the original count suddenly matters a lot.


The proposed solution is a small website for one laundry vendor serving Babcock students. The vendor records an order when the clothes arrive, gives the student a numbered receipt, and updates its progress. The student can open the receipt later to check the item list, balance, and collection estimate.

Here, “pickup” means collecting finished clothes at the vendor's location. The first version will not arrange deliveries or collect laundry from hostel rooms.

## 2. The problem worth solving

The main problem is the uncertainty between dropping clothes off and collecting them. A student should be able to answer three ordinary questions without starting a fresh conversation each time:

- What did I hand over?
- Is it ready, and if not, when should I come back?
- How much do I still owe?

The vendor needs the same information, especially when another attendant takes over. A record that only says “one bag” may identify a transaction, but it gives little help if the contents are disputed.

The likely effects are wasted trips, repeated enquiries, slow searches at collection, and disagreements that are harder to investigate than they need to be. These are the problems to test locally. Their frequency at Babcock has not been measured for this PRD.

The aim is to make each order easier to follow. The website will still depend on the attendant counting accurately, labelling the clothes, and updating the record. If those steps do not happen, a digital receipt will be no more reliable than a badly kept notebook.

## 3. Research and what it tells us

The research for this document consists of documentation from existing babcock laundry businesses and a number of babcock boys hostel students some which said
1. Hebrom kanu: "the timing between when the clothes and picked and dropped are sometimes inconsistent causing clothes to pile up and cost more money"
2. Olokodana muhammed: "some of my clothes get lost and cant even be found later and nothings done to stop it from happening gain, its just give and pray"
3. Abubakar sijibomi: " clothes get mixed up and its annoying"

### 3.1 The receipt should stay connected to the clothes

The Coin Laundry Association's *Gold Book* recommends numbered forms for drop-off orders, with copies for the customer and the business and a copy accompanying the bundle through cleaning. It also recommends keeping voided forms rather than allowing them to disappear from the records. Coin Laundry Association, “Drop-off Procedures”

The useful lesson is straightforward: the customer record and the physical bundle need a common reference. The proposed tracker will use one receipt number on the student's order and the vendor's bag label. Corrections will leave a history. The guide describes an older US business context; its prices and collection of customer addresses are not adopted here.

### 3.2 Existing software already handles this kind of workflow

CleanCloud documents a process that separates item detailing, cleaning, and ready orders. It supports due-date filters, item notes, and customer or bag labels. CleanCloud order-management guide

This matters because the project is not claiming to invent laundry tracking. The question is whether a small version fits a particular vendor's needs. our proposed first version borrows the basic separation between receiving, cleaning, and readiness, while leaving out delivery management and other features that do not help at a single collection point.

CleanCloud's documentation explains its features; it does not prove that this project would reduce delays. That needs to be measured during a pilot but is not the point of this document.

### 3.3 Item counts and complaints belong to the same order

Laundryheap explains that its facilities record the laundry received and use recorded items when calculating final charges. Its missing-item process starts with the customer's order history and uses information such as item descriptions and internal records during an investigation. Laundryheap's service process, missing-item guidance

For our project, that suggests two decisions. First, count and agree the items while the student is present. Second, keep any later complaint attached to that original order. A staff member should not be able to change “five shirts” to “four shirts” without an explanation and a visible correction history.

These are documented business practices, not evidence of how often items go missing at Babcock. The vendor's complaint procedure will also need to be agreed separately.

### 3.5 Decisions taken from the research

| Evidence or concern | Decision for the first version |
|---|---|
| Physical bundles need to match the customer's record. | Use the same reference on the receipt and bag label. |
| Receiving, cleaning, and readiness are different steps. | Use a few clear statuses rather than one vague “processing” label. |
| A dispute may require the original item list. | Preserve accepted quantities and record later corrections. |
| A record can be useful even without an app. | Keep a numbered paper fallback and test whether the website adds enough value. |
| Local availability does not demonstrate local dissatisfaction. | Measure the actual problems before expanding beyond one vendor. |

The biggest unanswered question is whether the vendor will keep the record current during a busy day. The pilot must test that as seriously as student interest.

## 4. Who the product is for

**The student** wants to leave clothes, understand the charge, and collect the correct items without unnecessary follow-up. A readable receipt matters more than a busy home page.

**The attendant** needs to record an order while another customer may already be waiting. Common item types and quantities should be quick to enter. Looking up a receipt should take only a few steps.

**The owner or manager** needs to find late orders, correct mistakes, and handle complaints. In a small shop, the owner may also be the attendant. Separate permissions still help prevent ordinary edits from changing an accepted price or payment record without an explanation.

## 5. What the first version will do

The first version should:

1. Give each accepted order a receipt both sides can inspect.
2. Make the latest recorded status and collection estimate visible to the student.
3. Help the vendor find orders that are overdue or waiting for collection.
4. Record payment and collection without losing the earlier history.
5. Keep a clear record when an item count or price is disputed.

### Included in the MVP

- One vendor and one collection location.
- Student accounts linked to their own orders.
- Staff accounts with role-based access.
- Per-item order entry, quantities, service type, and agreed prices.
- A numbered digital receipt and matching physical bag label.
- Received, cleaning, ready, and collected statuses.
- Expected-ready date and delay explanations.
- Payment records for money received outside the website.
- A collection check and order issue log.
- A vendor dashboard with search and filters.

### Not included

Online payments, delivery riders, live location tracking, multiple vendors, subscriptions, loyalty points, public reviews, automatic compensation, washing-machine integration, or AI features.

The first version supports item-priced services. Weight-based pricing and partial collection are deferred so that the initial counting and collection rules remain clear.

## 6. User stories

| User | Need | Reason |
|---|---|---|
| Student | See the items and quantities on my receipt. | I can check that the handover was recorded correctly. |
| Student | See whether my order is ready and when it was last updated. | I can decide when to visit the vendor. |
| Student | See my agreed total and outstanding balance. | I know what I still need to pay. |
| Student | Report a missing or incorrect item against my order. | The complaint stays connected to the original record. |
| Attendant | Create an order without retyping unnecessary details. | Recording the order does not hold up the queue. |
| Attendant | Search by receipt number or customer. | I can find the correct bundle at collection. |
| Manager | See overdue orders and unresolved issues. | I can follow up on work that needs attention. |
| Manager | Review corrections and staff actions. | I can understand what changed and who changed it. |

## 7. How an order moves through the service

### Step 1: Receive and count

The student and attendant count the clothes together. The attendant records each item category, quantity, service, and identifying description where needed. “Blue long-sleeved shirt” is more useful than “shirt” when an item needs separate identification. Optional condition notes capture visible issues discussed at handover.

The student reviews the count, total price, and expected-ready date on the screen. The attendant records that the student confirmed the details. This confirmation means the attendant has shown the details to the student and recorded their agreement.

### Step 2: Issue the receipt

Saving the confirmed order creates a unique receipt number and a student-visible record. The same reference is attached to the laundry bundle. If items leave the bundle during cleaning, the vendor must maintain a physical identification method. A website alone cannot keep separated garments matched to their owners.

The receipt includes the vendor's collection location, item list, total, payment recorded, balance, expected-ready date, and current status. It does not expose another customer's information.

### Step 3: Update progress

The attendant changes the order from received to cleaning when work begins. “Cleaning” covers washing, drying, ironing, and packing in the MVP. The student mainly needs to know whether to come for collection. Asking the attendant to update every washing and ironing step would add more work than the first version needs.

If the expected date changes, the attendant enters a revised date and a short reason. The earlier date stays in the history. A revised estimate must not erase evidence that the original promise was missed.

### Step 4: Mark ready

Before marking the order ready, the attendant checks the packed items against the receipt. An unresolved missing item prevents the order from being marked ready as a complete order. The student sees the updated status when viewing or refreshing their order page.

For now, students check the order page themselves. It shows when the attendant last updated it, so an old entry is not mistaken for a live report. Automatic messages can be considered after the basic workflow has been tested.

### Step 5: Collect

At collection, the attendant finds the order, checks the student's single-use collection code, and counts the returned items with the student. Any outstanding balance is settled directly with the vendor and recorded. The attendant can mark the order collected only when the full count is confirmed, the balance is zero, and no handover discrepancy remains unresolved.

If the student cannot access their code, the manager can use a documented identity check and record an override with a reason. Knowing a receipt number alone is not enough to collect clothes.

## 8. Requirements and how we will check them

| ID | Requirement | Acceptance condition |
|---|---|---|
| FR-01 | Restrict access by role and order ownership. | A student cannot retrieve another student's order, even by changing an order ID. |
| FR-02 | Create an itemised order. | Saving requires an identified customer, at least one item, positive whole-number quantities, a service, non-negative prices, a future expected-ready time, and handover confirmation. |
| FR-03 | Calculate totals consistently. | The total equals the sum of quantity multiplied by agreed unit price for every line. Money is stored in integer kobo. |
| FR-04 | Issue one receipt per accepted order. | Retrying the same submission after a connection failure returns the existing order rather than creating another. |
| FR-05 | Preserve the accepted receipt. | Later catalogue price changes do not alter existing orders. Corrections require a manager, a reason, and recorded customer acknowledgement. Earlier values remain available. |
| FR-06 | Enforce status transitions. | An ordinary staff action cannot jump directly from received to collected or collect an order twice. |
| FR-07 | Show current progress. | The student can see status, expected-ready date, last update, and any customer-visible delay explanation. |
| FR-08 | Track overdue work. | An unready, uncancelled order whose promised time has passed appears as overdue. Original and revised promises remain distinguishable. |
| FR-09 | Record external payments. | Each entry records amount, method, staff member, and time. Entries cannot exceed the balance; corrections use manager-authorised reversals rather than deletion. |
| FR-10 | Check handover before collection. | Collection requires a valid code or recorded manager override, full item confirmation, zero balance, and no unresolved handover issue. |
| FR-11 | Keep an issue record. | A student can submit a missing-item, wrong-item, damage, or payment concern against their order, including after collection. |
| FR-12 | Search operational records. | Staff can search receipts and filter by status, overdue state, expected date, and open issues. |
| FR-13 | Cancel without erasing custody history. | Only a manager can cancel a received order, after recording return of the items and refund of any recorded payment. Orders already in cleaning follow the issue-resolution process. |

Collection confirms a handover. It does not prevent a student from reporting a problem discovered afterwards or automatically resolve an existing complaint.

## 9. Order states and exceptions

The normal path is:

`Received -> Cleaning -> Ready -> Collected`

Cancellation is available from received under FR-13. A manager may return ready to cleaning for rework, with a reason visible in the history. Collected orders remain collected even if a later complaint is opened; complaint status is tracked separately.

Delay is a flag rather than a substitute for the current status. An order can be cleaning and overdue at the same time.

| Situation | Expected behaviour |
|---|---|
| Student says the count is wrong at drop-off. | Correct the draft before confirming receipt of the clothes. |
| Count is disputed after acceptance. | Open an issue; retain the accepted count and record any agreed correction. |
| An item is missing before packing. | Keep the order out of ready status and record the discrepancy. |
| Work takes longer than expected. | Record the reason and revised estimate without removing the original deadline. |
| Two attendants update the same order. | Reject a stale update and ask the second attendant to refresh. |
| Internet fails during submission. | Show that saving is unconfirmed and allow a safe retry. Never show a successful receipt before the server confirms it. |
| Internet remains unavailable. | Use a numbered paper receipt, then reconcile it once. Store its reference to prevent duplicate entry. |
| A student reports damage after collection. | Open an issue linked to the collected order; the manager records the investigation and agreed outcome. |

The system records a complaint and its outcome. It does not decide compensation or invent a liability policy for the vendor.

## 10. What the backend needs to keep track of

The choice of programming language comes later. First, the team needs to agree on the records the service must keep and the mistakes it must prevent.

| Record | Key information |
|---|---|
| User | Internal ID, name, verified login contact, role, active status |
| Order | Receipt number, customer ID, status, agreed total, original and current expected-ready times, creation and collection times |
| Order item | Order ID, category, description, service, quantity, accepted unit price, condition note |
| Payment entry | Order ID, amount, method, received/refunded/reversed type, staff member, timestamp, related original entry if reversed |
| Order event | Order ID, action, previous and new values where relevant, actor, timestamp, reason |
| Issue | Order ID, reporter, category, description, status, manager response, resolution |
| Collection verification | Order ID, protected code representation, expiry, attempt count, used status, any manager override |

Hiding a button is not enough to protect an order. The backend must check who is making each request and whether they are allowed to make it. It must also handle retries: a slow connection should not create two receipts or record the same payment twice. Marking an order collected and using up its collection code must happen together, so one cannot succeed while the other fails.

Student contact details and collection codes must not appear on publicly visible bag labels. Staff accounts must be individual so that the event history identifies the person who made a change.

## 11. Quality and privacy requirements

- **Phone usability:** receiving an order and viewing a receipt must work on a 360-pixel-wide screen without horizontal scrolling.
- **Speed:** target a response within two seconds for 95% of order-detail requests under a test of 20 concurrent users, excluding the user's network delay. This is a proposed test target, not an achieved result.
- **Clarity:** status labels must use words, not colour alone. Forms need visible labels and errors beside the relevant field.
- **Data minimisation:** collect a name and necessary login contact. Matric numbers, identity-card photographs, and hostel room numbers are unnecessary for collection at the vendor's location.
- **Protection:** use secure connections, protected sessions, rate-limited authentication and code attempts, and securely hashed passwords if password login is used.
- **Retention:** proposed policy is to retain identifiable order records for 90 days after collection or cancellation, extending only relevant records while an issue remains open. Explain the approved policy before launch and apply deletion to backup copies within the documented backup cycle.
- **Recovery:** take a daily restricted backup during the pilot and test restoration before launch. Record any manual receipts needed to reconstruct orders after an outage.

## 12. How we will know whether it helps

A four-week pilot with one willing vendor should assess whether the tracker helps without slowing the counter down. These are proposed targets, not research results.

| Measure | Definition | Pilot target |
|---|---|---|
| Complete receipts | Accepted orders containing confirmed items, price, and expected date divided by all accepted orders. | 100% |
| Entry time | Time from starting a draft to issuing its receipt, measured for orders of ten items or fewer. | Median of three minutes or less. |
| Student use | Orders viewed by the customer before collection divided by eligible pilot orders. | At least 60%. |
| Readiness accuracy | Orders marked ready that pass the full-item check at collection divided by ready orders collected. | At least 95%. |
| Repeat enquiries | Readiness enquiries per completed order, compared with a one-week baseline recorded by the same vendor. | A reduction of at least 25%. |
| Traceable handovers | Collected orders with staff identity, timestamp, and completed verification record. | 100%. |

Report counts alongside percentages. If fewer than 30 orders complete during the pilot, treat the results as preliminary. Also record staff complaints, customer confusion, unresolved issues, and work done outside the tracker. A dashboard that looks complete while staff rely on a separate notebook is not evidence of adoption.

## 13. When the first version is ready to try

The MVP is ready for a controlled pilot only when:

- A vendor has agreed to use it and maintain the physical labels.
- Student and staff access restrictions have been tested.
- Order totals, payment reversals, and collection checks behave correctly.
- Retried submissions and simultaneous staff edits do not corrupt records.
- A complete order and an order with a discrepancy can be handled from start to finish.
- The vendor has an outage procedure, a named complaint handler, and an agreed data-retention policy.

At the end of the trial, the decision should depend on whether people actually use the record and whether it makes collection easier. More accounts or more features would not answer that question.

