# MWU Admissions Counselor Workspace (embeddable page)

One static page (`index.html` + `jack-mautz.jpg`). No build step, no backend.

## Host it
Any static host that serves over HTTPS and allows iframing works:
- **GitHub Pages:** new public repo → upload both files → Settings → Pages → deploy from `main` / root
- **Netlify Drop:** drag this folder onto app.netlify.com/drop

Opening the page with no parameters shows Jack Mautz, so you can test the URL on its own first.

## Embed in the Genesys script
Add a **Web Page** component (full width, ~820 px tall) and set its URL to:

```
https://adam-mautz.github.io/demo-pages/mwu-admissions/?first_name={{first_name}}&last_name={{last_name}}&phone={{phone}}&email={{email}}&dob={{dob}}&program={{program}}&campus={{campus}}&entry_term={{entry_term}}&app_status={{app_status}}&app_stage_num={{app_stage_num}}&app_owner={{app_owner}}&app_owner_available={{app_owner_available}}&sis_id={{sis_id}}&cas_type={{cas_type}}&cas_id={{cas_id}}&application_id={{application_id}}&admit_date={{admit_date}}&deposit_due_date={{deposit_due_date}}&deposit_amount={{deposit_amount}}&outreach_attempts={{outreach_attempts}}&last_outreach={{last_outreach}}&next_protocol_step={{next_protocol_step}}&stage1_date={{stage1_date}}&stage2_date={{stage2_date}}&stage3_date={{stage3_date}}&stage4_date={{stage4_date}}&stage6_date={{stage6_date}}&slate_record_guid={{slate_record_guid}}
```

- Each parameter is the matching script input variable (same names as the data-table columns).
- Leave out any you don't need. A missing, blank, or unresolved `{{…}}` value falls back to Jack's demo data.
- Optional extras: `photo_url` (full image URL), `slate_base` (e.g. `https://apply.midwestern.edu`), `channel`, `verified`.
- `days_to_deposit` isn't needed: the countdown is calculated live from `deposit_due_date` (formats like `Oct 25, 2026` or `2026-10-25`).
- `app_stage_num` (1–6) drives the timeline: 1 Application · 2 Materials · 3 Interview · 4 Admitted · 5 Deposit · 6 Orientation.

## Notes
- Slate link patterns (`/manage/lookup/record?id=` and `/manage/lookup/application?id=`) are placeholders. Confirm them with the Slate admin.
- "Send deposit link by SMS" only shows a confirmation toast; it is a demo prop.
- Copy buttons use the clipboard API, with a fallback for iframes that block it.
- Avoid `&` or `#` inside field values; they break the query string.
