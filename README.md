# SMART ADR Connect

```
 ██████╗███╗   ███╗ █████╗ ██████╗ ████████╗ █████╗ ██████╗ ██████╗
██╔════╝████╗ ████║██╔══██╗██╔══██╗╚══██╔══╝██╔══██╗██╔══██╗██╔══██╗
███████╗██╔████╔██║███████║██████╔╝   ██║   ███████║██║  ██║██████╔╝
╚════██║██║╚██╔╝██║██╔══██║██╔══██╗   ██║   ██╔══██║██║  ██║██╔══██╗
██████╔╝██║ ╚═╝ ██║██║  ██║██║  ██║   ██║   ██║  ██║██████╔╝██║  ██║
╚═════╝╚═╝     ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝   ╚═╝╚═╝  ╚═╝╚═════╝ ╚═╝  ╚═╝
```

---

## ◆ PULSE

An adverse drug reaction reported at 2 a.m. is the reaction that
matters most. SMART ADR Connect is the serverless PWA built for the
off-hours and the rounds: search a patient's drug allergy history by
HN or CID in seconds, submit a new ADR report from a form shaped for a
phone held in one hand, and let the Naranjo calculator assess
probability on the spot. The backend is a Google Sheet and an Apps
Script - zero-cost, zero-maintenance, and always on.

| Search ▣ | Report ▣ | Naranjo ▣ | Serverless ▣ |
|---|---|---|---|

*The loop - search, report, assess - is sealed.*

> Built with Vue 3 + TypeScript + Tailwind, served by Google Sheets and
> Apps Script - infrastructure that costs nothing and disappears
> nothing.
>
> **suradet-ps**, artifact keeper

---

## ◆ IGNITION

Two setups, one command.

```
⟫ git clone https://github.com/suradet-ps/smart-adr.git
⟫ cd smart-adr
⟫ bun install
⟫ bun run dev
```

Open [http://localhost:5173](http://localhost:5173).

<details>
<summary>Backend setup (Sheets + Apps Script)</summary>

1. Create a Google Sheet named e.g. `SmartADR_DB`.
2. Add a tab `SmartADR_Reports` with the columns: `hn`, `timestamp`,
   `agent`, `symptom`, `reporter`, `note`, `naranjo_result`,
   `patient_cid`.
3. Extensions > Apps Script: paste `Code.gs`, set `SHEET_ID` from the
   spreadsheet URL.
4. Deploy as a web app - execute as Me, access Anyone - and copy the
   Web App URL into the frontend's `API_URL`.

</details>

The release artifact: `⟫ bun run build` - `dist/` deploys to any
static host.

---

## ◆ ANATOMY

One sheet, one script, a form that fits the hand.

- **Searches** - instant allergy-history lookup by Hospital Number or
  Citizen ID - the history a nurse needs before the next order is
  typed.
- **Reports** - a streamlined form for ADR reports: agent, symptom,
  reporter, note - structured enough to count, fast enough to finish
  between rounds.
- **Assesses** - the built-in Naranjo algorithm calculator walks the
  ten questions and returns the probability - the report leaves with
  its verdict attached.
- **Serves** - Google Sheets is the database and Apps Script is the
  API: no server to maintain, no bill to pay, no deadline to renew.
- **Wears** - mobile-first Tailwind, built for nurses and pharmacists
  on rounds - one hand holds the phone, the other holds the pen.

---

## ◆ RITUALS

**The core ceremony** - the off-hour report:

1. Search by HN or CID. The allergy history answers in seconds.
2. When a new reaction is seen, open the report form - built for the
   phone in the pocket.
3. Fill agent, symptom, and reporter; run the Naranjo questions; the
   probability attaches itself.
4. Submit. The sheet rows grow; the record is in the shared ledger,
   not in a shift handover that may be forgotten.

**The ceremony of the sheet** - the database is a spreadsheet the
department already understands: rows visible, history queryable, and
the whole backend inspectable by anyone who can read a table.

**The ceremony of the zero bill** - serverless is not an acronym
here, it is a promise: no infrastructure to fund, no endpoint to
renew, no DevOps to page at 2 a.m. - the same hour the form was built
to serve.

---

## ◆ ECHOES

**Where this artifact is heading**

```
search  ▸ HN/CID allergy history lookup ─────────────────────────────── ▸ sealed
report  ▸ streamlined ADR form ──────────────────────────────────────── ▸ sealed
assess  ▸ Naranjo probability calculator ────────────────────────────── ▸ sealed
serve   ▸ Google Sheets + Apps Script backend ───────────────────────── ▸ sealed
```

**Raising the artifact** - the backend script is `Code.gs`; the
components are `SearchPanel.vue` and `ReportForm.vue`; the types in
`src/types.ts`. Open an issue first to discuss a change.

**Status** - dependencies are maintained through Renovate; the build
deploys to any static host.

---

```
  ─────────────────────────────────────────
   A reaction reported at 2 a.m.
   is a reaction the system did not miss.
  ─────────────────────────────────────────
```

Licensed under the [MIT License](LICENSE).