# Procimo Tech – Support Team Technical Challenge

**Candidate:** Olabode Adetula  |  **Role:** Junior Support Engineer

## Task 1 — Ticket Analysis & Triage

### Ticket 1 – Door badge not working again (Maria S., Client A)

**a) Category:** Configuration issue (probable). The failure is intermittent, tied to one door and happens "before my shift", which points to access rules or schedules rather than a broken reader. The symptom could also come from the badge, the reader or the access-control hardware, so evidence is needed before the cause is confirmed.

**b) Severity & priority:** Severity **Low**: one user, no safety or data impact, and a workaround exists (a colleague lets her in). Priority **Medium**: it is the third occurrence this month, the client is frustrated, and a recurring pattern is usually cheap to fix and costly to ignore.

**c) Missing information:**

- Dates and times of the three failures, her shift start time on those days, and the matching access-control event log entries.
- Whether she arrived before her shift started.
- Whether other badges also fail at the North door, whether hers works at other doors, and whether her badge was recently replaced or damaged.
- What the reader did (error message, light or beep, or no response), and the North door reader's ID or log identifier.
- Her badge serial number or RFID ID, and her access group and schedule as configured, plus any recent schedule changes.

**d) Next action:** Ask the client a clarifying question and coordinate internally; do not escalate to Development yet. Acknowledge the frustration, check the access logs for her badge at the North door on those dates, and send the client the questions above. If the logs show "denied: outside schedule", coordinate with the Client Account / Shift-Schedule Configuration team. If the logs show no read at all, escalate to Hardware. Because her failures happen before her shift, ask the configuration team to confirm her schedule window before her next shift and, if the window is the cause, to apply an interim fix. Reply to Maria with an apology and an update on what we are checking.

### Ticket 2 – Positioning system down, whole plant (Site Manager, Client A, Plant B)

**a) Category:** Bug (suspected). The live map has been frozen plant-wide since last night. A broad RTLS failure is reported, but data ingestion, connectivity, infrastructure, software or hardware could each be responsible, and the ticket does not allow the cause to be confirmed.

**b) Severity & priority:** Severity **Critical**, priority **P1 (highest)**: the client uses the map to keep people clear of forklifts at the loading dock, so there is an active physical safety hazard and core safety monitoring is halted across the entire plant, and it has already been down for hours.

**c) Missing information:**

- Exact time the map froze (and the last successful update), and whether anything changed beforehand (update, maintenance, power or network outage).
- Whether the map is frozen for every tag or only some, and whether only the wall screens are frozen or the admin portal shows stale data too.
- Whether tags are still active (LEDs or signals), whether anchors or gateways show as online, and the health of the RTLS service and data ingestion.
- Whether other plants or clients are affected.
- Any error messages or screenshots.

**d) Next action:** Escalate immediately to Development or the on-call engineer, and notify the Hardware/infrastructure contact in parallel. Run a few quick checks first (connectivity, service health, screen refresh, admin portal, whether other clients' maps are also affected), but do not wait for the client's answers before escalating. Reply to the client within minutes: confirm it is being treated as P1, advise them to follow their established safe operating procedure for forklift movements (for example spotters or restricted movement near the dock) and not rely on the frozen map until live tracking is confirmed restored, and promise regular updates.

### Ticket 3 – Numbers look off (Client B)

**a) Category:** Question (unclassified). It could turn out to be a bug, a configuration issue or a hardware issue, but nothing in the ticket supports any of them yet.

**b) Severity & priority:** Severity **cannot be rated yet**; provisionally Low-to-Medium. Priority **Medium**: wrong monitoring data may be driving decisions, so the client should get a fast reply, but nothing indicates an outage.

**c) Missing information:**&#32;

- Which machine-monitoring metric looks wrong, and on which machine ID(s) or line.
- The expected versus displayed values.
- The time period and timestamps, and when it started.
- Whether one user or several see it.
- Whether the machine was running during that period.
- Whether anything changed recently (machine swapped, settings changed, new shift).
- A screenshot or export, with the relevant data-source context.

**d) Next action:** Ask the client for a concrete example, with the expected value and its source. Do not guess or escalate until it is clear whether the data is actually wrong or just differently understood. Then compare the screen with the source data for the same timestamps; if the mismatch is reproducible after validating filters and configuration, log it as a bug with that evidence and escalate to Development.

### Ticket 4 – How do I export last month's report? (Client C)

**a) Category:** Question.

**b) Severity & priority:** Severity **Low** (nothing is broken). Priority **Low-to-Medium**: it is quick to answer and tied to a meeting deadline, so reply the same day.

**c) Missing information:** Nothing essential. The FAQ covers the request. If the Export option is not visible, confirm which report they are viewing and whether the client's user role is allowed to export.

**d) Next action:** Resolve directly. Reply with the FAQ steps (open the report, click the ⋮ menu top-right, choose Export, then PDF), mention CSV as an alternative, and ask them to reply with the exact error or a screenshot if the Export option does not appear, so I can check permissions and, if those are correct, log a possible defect.

## Task 2 — Documentation Validation

**What's wrong:**

- **Wrong button name:** step 3 says "Transfer Tag"; the admin portal button is "Reassign Tag".
- **Missing step:** the tag must first be removed from its current zone. Skipping this causes a "duplicate tag" error, which the article never mentions.
- **Incorrect timing:** step 4 says the tag appears "immediately"; it can take up to 2 minutes, so readers may think it failed.
- **Unsupported instruction:** step 5 (hold the button to restart the tag) is not in the System Facts and cannot be verified; it should be removed or confirmed with the product team.
- **Unhelpful escalation:** step 6 gives no wait-and-check step (verify the tag was removed and reassigned correctly) before contacting support, and does not say what to include (serial number, old and new zones, time of reassignment, error message).

**Rewritten article: How to Re-Pair a Lost or Damaged RTLS Tag**

1. Open the admin portal and go to **Tags**.
2. Find the tag using its serial number.
3. Remove the tag from its current zone.
4. Click **Reassign Tag** and select the new zone. (*If you skip step 3, you will see a "duplicate tag" error. Remove the tag from its current zone, then try again.)*
5. Wait up to 2 minutes for the tag to reappear on the live map.
6. If the tag has not appeared after 2 minutes, confirm it was removed from its previous zone and reassigned to the intended new zone. If the issue persists, contact Support and include the tag's serial number, the old and new zones, the time of reassignment, and any error message you saw (including “duplicate tag”).

*Note to author: the "restart the tag" step was removed because it is not supported by the system facts. Please confirm with the product team before re-adding it.*

## Task 3 — Testing

### a) Bug report

**Summary:** Total Units Produced is lower when a Shift filter and a date range are applied together than when the same shift is viewed on its own for the same days. The date range alone gives the correct total.

**Assumptions:**

- "Shift alone" and "Shift + date range" cover exactly the same days. If the shift-only view covers a wider period, a lower number would be expected, so this must be confirmed with the client.
- The client is comparing against a known or cross-checkable total.
- The issue may be specific to certain shifts (for example, a shift that runs past midnight); this is not yet known.

**Steps to reproduce:**

1. Open the dashboard and apply only a date range (D1 to D2). Record the Total Units Produced (A).
2. Clear the filters. Select one Shift only, with the displayed period covering exactly D1 to D2. Record the total (B).
3. Keep the same Shift and apply the date range D1 to D2. Record the total (C).

**Expected result:** C equals B. The sum of all shifts' totals for D1 to D2 should equal A.

**Actual result:** C is lower than B. Date range alone (A) appears correct.

**Severity & priority:** Severity **Major**: the dashboard shows a wrong production KPI with no error, so users may trust and act on incorrect data that feeds operational reporting and decisions. The scale of impact is not yet known and nothing indicates safety-critical use, so it is Major rather than Critical. Priority **High (P2)**: a workaround exists (view shift only or date range only), and nothing is down, but silent data errors damage client trust.

**Additional information to confirm:**

- The exact shift and dates used, with screenshots showing all three totals
- Whether it affects all shifts or only some (for example, overnight shifts)
- Whether it reproduces for other users and clients, and in our internal environment
- The client's time zone, how shifts start and end, and whether totals are based on event time or processing time
- When it started, whether it followed a recent release, and the dashboard or product version
- Whether other totals on the dashboard are affected (and keep evidence free of unnecessary personal or sensitive data)

### b) Test cases for verifying the fix

| # | Scenario | Steps | Expected result |
| --- | --- | --- | --- |
| 1 | Core case: shift + date range | Select one shift and a multi-day range. Compare with the shift-only total for the same days. | Totals match; the figure also matches the known production data. |
| 2 | Filter order | Apply Shift then date range; then reset and apply date range then Shift. | Same total in both cases. |
| 3 | Shifts add up | For one date range, record the total for each shift separately, then the unfiltered total. | Sum of all shifts equals the date-range-only total. |
| 4 | Edge: overnight shift | Choose a shift that crosses midnight and a range starting or ending on those days. | Units are neither dropped nor double-counted; attribution follows the shift definition. |
| 5 | Edge: single-day range | Set start date and end date to the same day with a shift selected. | Total equals that day's production for the shift; both boundary days are included. |
| 6 | Regression and empty result | Re-test shift-only and date-only filters; then pick a shift with no production in the range. | Shift-only and date-only totals are unchanged; the empty case shows 0 with no error. |

## Task 4 — Internal Communication

### a) Escalation to Development (Ticket 2)

@dev-oncall P1 – Client A, Plant B: live RTLS map frozen since last night on all wall screens; forklift and staff positions are not updating. The site relies on it for loading-dock safety.

Checked: multiple screens affected, so not a single missing tag; admin portal shows the same stale positions; no known maintenance; other clients' maps normal.

Requested last-known-good time and screenshots. Client advised to follow their established safe operating procedure meanwhile.

Need from Dev: check RTLS service/ingestion health, recent deployments and logs, and advise ownership and ETA.

### b) Message to the configuration team (Ticket 1)

Hi Configuration team – Maria S. (Shift Supervisor, Client A) says her badge failed at the North door before shift start, three times this month. This may be an access rule or schedule mismatch; the cause isn't confirmed.

Please check: (1) her account, badge status and North-door permissions; (2) her shift-schedule access window; (3) recent access changes, and whether she should have been authorised at those times.

If configuration is correct, I'll continue with reader checks and escalate to Hardware. Could you reply today, before her next shift?

## Task 5 — Optional Bonus: Technical Curiosity

### a) Reading a Data Snippet

I would look first at `last_seen`, then `battery_pct`, then `zone_id`. `status` only tells me what the system already believes, so I use the other fields to test it.

1. **`last_seen` (2026-09-20T08:14:00Z):** This shows when the tag last reported, so I can compare it with when the client says it went offline. A few minutes ago suggests a temporary dropout; several days ago suggests the tag is lost, damaged or switched off. The "Z" means UTC, so I would convert it to the client's local time before comparing.
2. **`battery_pct` (41):** A tag that went offline at 41% probably did not run out of battery, so this helps rule out the most common cause. The reading may be old, so I would treat it as a clue and not as proof. The cause then more likely lies in the tag itself, signal coverage, connectivity or configuration.
3. **`zone_id` (Z12):** I would check whether other tags in Z12 are also offline. If they are, the problem is probably in that zone (for example, an anchor, gateway or network issue). If only this tag is offline, the problem is probably the tag itself. I would also check whether the tag was recently reassigned or moved, because a change of zone can make a tag look offline or cause a duplicate tag error.
4. **`tag_id` and `status`:** I would use `tag_id` to find the same tag in the admin portal and confirm that its status matches this data.

A single snippet cannot prove the cause, so I would also ask the client where the tag physically is, when it last appeared on the live map, and whether other tags are affected.

### b) A Simple Query

```plain
SELECT ticket_id, client, product, status, severity, created_at
FROM support_tickets
WHERE status = 'Open'
  AND severity = 'High'
  AND created_at < CURRENT_TIMESTAMP - INTERVAL '3 days'
ORDER BY created_at ASC;
```

**Assumptions:**

- The table is called `support_tickets`, and "open" is stored as the exact value `'Open'`. I would check the real status values first, since an "In progress" or "Waiting on client" ticket may also count as open.
- "More than 3 days ago" is read strictly, so `created_at` must be earlier than now minus 3 days. Results are sorted oldest first so the most overdue tickets appear at the top.
- The date syntax varies by database. For example, MySQL uses `NOW() - INTERVAL 3 DAY` and SQL Server uses `DATEADD(day, -3, GETDATE())`.

**Plain steps (if SQL is not available):** Filter the table to rows where status is Open and severity is High. Keep only rows whose created\_at is more than 3 days before today. Sort by created\_at, oldest first.
