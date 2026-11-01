# Proteus FY2026 Audit Readiness Progress

Shared progress page for Proteus, Inc. and Martinez Accounting, Inc. It shows which requested documents have been received, the status of each piece of work, and the timeline to the November 16, 2026 submission to Price Paige & Company.

The page is static. `index.html` reads live data from the Supabase project "Proteus DB" (tables `requests`, `milestones`, `workstreams`, `update_log`, `site_status`, `pbc_items`). Since the Nov 1, 2026 multi-tenant change, every table requires a signed-in user: the page asks for the same email and password as the questions and monthly close pages, and reads only Proteus rows (`org_id` filter). There is no offline snapshot; if Supabase is unreachable the page says so instead of showing old numbers. Netlify publishes the repository root on every push to `main`; there is no build step.

Status changes are made in Supabase, not in this repo, so they appear on the page immediately without a deploy.

## Table fields

- `requests`: one row per requested document. `status` is one of `Not yet received`, `Partial`, `Received`. Set `received` (YYYY-MM-DD) when anything arrives and put what is still missing in `note`.
- `workstreams`: Martinez work items. `status` is `Not started`, `Waiting on documents`, `In progress` or `Done`; `done` / `total` drive the progress bar.
- `milestones`: dated timeline. `status` is `Upcoming` or `Done`; `major` + `short` put a date on the timeline strip.
- `site_status` and `update_log`: `updated_at` (shown in the header), `last_upload_check`, and the newest-first list shown under Recent updates.
- Every insert sets `org_id` to the Proteus organization, or the row will not show.

## Rules for updates

- Documents and progress only. No dollar amounts, findings, account numbers or anything about individual employees.
- Notes are written for Proteus staff: plain language, what came in and what is still needed, never who is at fault.
- Every change gets a `log` entry and a new `updated_at`.
