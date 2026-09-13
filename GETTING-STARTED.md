# How to use an AI Expert

You do not need to be a programmer. You do not need to know this product already.

An **Expert** is a folder on your computer for **one** kind of desk work — bookkeeping, a dental front desk, a shop office, and so on. You open that folder in **Cursor** and talk to it as your assistant for that role. It reads files you drop in, makes lists and write-ups, and **writes down** how *your* shop works so the next job is closer.

A chat app forgets. This folder remembers.

The notes already in the folder are a **head start** for that kind of job. Each Expert comes with **facts** and **rules** that are common for that industry role — for example, how a typical dental front desk or bookkeeping desk works. They are typical for that kind of work, not how *your* shop works, until you tell it otherwise.

---

## 1. Install Cursor

1. Go to [cursor.com](https://www.cursor.com) and install Cursor.
2. Open it and sign in. (Cursor will ask you to pick a plan if you do not have one yet.)
3. You do not need to learn coding. You will type in the chat.

---

## 2. Get an Expert folder

Download or copy this project from GitHub. Inside you will see many folders. Each one is a different job.

**Pick the one closest to your work** (see the list at the bottom). Copy that folder to a place you will keep, for example:

`Documents\my-dental-expert`

Use **that copy** for your business. As you talk to it, it will save notes about *your* shop inside that copy. The download from GitHub is only a starter. It is not a backup of the folder you work in every day.

---

## 3. Open that folder in Cursor (this step matters)

1. In Cursor: **File → Open Folder**.
2. Choose the copied folder itself — the one that contains a file named `role.md` and a `docs` folder.
3. Do **not** open the whole download with every role inside. Open **one** Expert folder. Example: open `dental-office`, not the folder that contains every Expert.

You should see files like `role.md` and `docs` in the left sidebar. There will also be an `items` folder. That is where each appointment, ticket, or month will get its own place.

---

## 4. Start the chat

1. Open the chat / Agent panel (usually on the right).
2. Type in plain English. You can copy this first message and fill in the blanks:

> I run a [kind of business] in [city or state]. We use [software or spreadsheets you already use]. Please read the files in this folder, then ask me anything you need so this matches *our* shop. Do not treat the starter notes as our rules until I say so. Here is what we must never do: [examples: never send money, never guess a price, never diagnose].

3. Answer its questions. Typical ones: what you call things, which reports you export, what “done” looks like, what is someone else’s job (the dentist, the CPA, the owner).

That first talk is you **introducing the shop**. It will save what you said in files. You do not have to edit those files by hand.

---

## Keep each job in its own folder

If every file landed in one shared pile, Tuesday would mix with Monday, and one patient’s visit would mix with the next. So the Expert makes **a separate folder for each job** inside `items/`.

What counts as “one job” is whatever that kind of desk already uses:

- Clinic: one **appointment** (date, time, chart number)
- Shop: one **ticket** or repair order
- Bookkeeping: one **month and account**
- Property: one **unit and work order**

A typical folder looks like this:

```
items/2026-09-15-1000-chart-4412/
  in/         the files you dropped for this visit
  work/       scratch while it works on this job
  out/        the finished list for this visit
```

`items/INDEX.md` is the list of those jobs. If your shop already numbers things another way, tell the Expert — it should use **your** names.

When you start the next appointment, ticket, or month, tell the Expert so it makes a **new** folder. Do not put those files in the last job’s folder.

---

## 5. Give it one small real job

Do not start with the hardest week of the year. Pick a job you already do, with a file you already have.

1. Export or save a file from your usual system (a spreadsheet, a PDF, or a screenshot of a report).
2. Tell the chat **which job this is**, the way that desk already files:
   - A clinic: the appointment (date, time, chart number — not a pile of extra personal details).
   - A shop: the ticket or repair order number.
   - Bookkeeping: the month and the account.
   - Property: the unit and the work order.
3. Put the file in that job’s `in/` folder, or drop it in the Expert folder and say “this is for the 10 a.m. appointment.” The Expert should make a folder under `items/` so **this** job does not mix with the last one.
4. Ask for the work in ordinary words. Examples:

- Bookkeeping: “Here is this month’s bank CSV. Make a list of what still needs a category, and a short write-up. Do not invent categories we have not used.”
- Dental front desk: “Here is tomorrow’s day list export. Make a checklist of missing intake forms. Do not guess clinical notes.”
- Shop office: “Here is the job list. Who is scheduled tomorrow, and which jobs are missing parts on the parts sheet?”

5. When it is done, look in **that job’s** `out/` folder (for example `items/2026-09-15-1000-chart-4412/out/`). The list of jobs is `items/INDEX.md`. Do not expect everything to land in one shared `out/` pile.

If it asks for a missing file, that is correct. Give it the file or tell it the column names on your sheet. Do not let it invent your prices, your hours, or your shop rules.

---

## 6. Correct it. That is how it gets good.

When something is wrong, say so in the same chat. Be specific:

- “We do not call that a work order. We call it a ticket.”
- “Never put full Social Security numbers in these lists.”
- “Late fee is $50 after the 5th. Do not invent a different number.”
- “That job is the dentist’s, not yours.”

It should **save** the correction and use it next time. If it makes the same mistake again, say: “You saved this wrong. Fix the note and use my version.”

A few real jobs plus a few corrections is enough to get going. There is no separate training course.

---

## 7. Use it in the daily rhythm

Once it has done a job once the way you like:

1. Export the same kind of file you always export.
2. Tell it the new appointment, ticket, or month. It should make a **new** folder under `items/` unless you are still working on the same job.
3. Ask for the same kind of list: “Do the Friday invoice list again for this week’s file.”
4. Skim the finished file in **that job’s** `out` folder. If a line is wrong, tell it. If it is right, you are done.

That is the loop: **say which job this is → drop a file → ask → check that folder’s write-up → correct when needed.**

---

## Back up your Expert folder

The folder you opened in Cursor is the memory. Over time it will hold:

- **Facts** — how *your* shop works
- **Rules** — what you told it never to do, and how you want lists written
- **Tools** — which reports and sheets you actually use
- **Each job’s files** — each appointment, ticket, or month under `items/`

If that folder is deleted, overwritten, or only left on one computer that dies, those notes are gone. Cursor and GitHub do not keep a second copy of *your* copy.

**Copy the whole Expert folder** to a safe place on a regular schedule — the same way you back up other business files (another disk, a USB stick, or the backup you already use). Back up the folder you work in every day, not the original download.

Do not put passwords, card numbers, or full account secrets in the folder. Those should not be in the backup either.

---

## What it will not do

- It will not send money, pay a bill, or log into your bank.
- It must not store passwords, card numbers, or full account secrets in the folder.
- It is not a lawyer, doctor, vet, or CPA. It can organize paperwork. It must not stamp a legal opinion, a diagnosis, or a tax opinion.
- The notes that came with the folder are **typical**, not *your* policy, until you tell it otherwise.

If it ever offers to do something on that “never” list, tell it no.

---

## If you picked the wrong folder

Use a different folder for a different job. A dental front desk and bookkeeping are two folders, not one chat that does everything.

If nothing is an exact match, pick the closest desk and tell it how *your* shop works.

---

## Pick a folder

Folder names are the job names at the top of this project.

**Office and money:** `bookkeeping` · `office-operations` · `purchasing-buyer` · `hr-admin` · `nonprofit-office` · `church-office-admin` · `data-visualization`

**Property and housing:** `property-manager` · `apartment-leasing` · `hoa-admin` · `self-storage-office`

**Trades and shops:** `trade-job-coordinator` · `construction-office` · `landscaping-office` · `pest-control-office` · `janitorial-office` · `facilities-maintenance` · `auto-service-advisor` · `auto-body-estimator` · `equipment-rental` · `print-shop-coordinator`

**Health-adjacent desks (not the clinician):** `dental-office` · `veterinary-front-desk` · `medical-clinic-front-desk` · `optometry-front-desk` · `physical-therapy-front-desk`

**Hospitality and personal care:** `restaurant-kitchen-admin` · `bakery-cafe-admin` · `catering-office` · `salon-front-desk` · `gym-front-desk` · `hotel-front-desk` · `event-venue-coordinator`

**Moving goods and people:** `wholesale-inventory` · `shipping-fulfillment` · `fleet-dispatcher` · `manufacturing-scheduler` · `moving-company-office`

**Other desks:** `insurance-agency-csr` · `real-estate-transaction-coordinator` · `mortgage-processor` · `staffing-agency-admin` · `childcare-admin` · `school-office-admin` · `dog-daycare-office`

---

## One-page reminder

1. Install Cursor.  
2. Copy the Expert folder for the role you want.  
3. **File → Open Folder** on that copy.  
4. In chat, introduce your shop.  
5. Say which appointment, ticket, or month this is. Drop one real file from your work.  
6. Read the finished list in that job’s `out` folder.  
7. When it is wrong, tell it. It should save that.  
8. For the next appointment, ticket, or month, start a **new** folder. Do not put those files in the last job’s folder.  
9. Copy the whole Expert folder somewhere safe. It is saving how your shop works.

That is the whole start.
