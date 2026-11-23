## shark

Custom app for Shark Shopfits on Frappe / ERPNext.

### Companion apps

#### frePPLe planning — `frepple_connector`

Supply planning for Shark runs in [frePPLe](https://frepple.com) through a separate app,
[VARDHANA87/frepple_connector](https://github.com/VARDHANA87/frepple_connector) (built and tested with
frePPLe community 9.19 and ERPNext 15). It is optional: Shark works without it, and nothing in this app
depends on it.

What it adds to a Shark site:

- **frePPLe Settings** — connection, company, Order Lookback / Demand Horizon, plan options; buttons for
  Test Connection, Export and Run Plan, Import Proposals.
- **Export to frePPLe** — open Sales Order lines (tagged with **Project** and **store location**), open
  Purchase Orders and Work Orders, BOMs with workstation loads, item suppliers with lead times, stock on hand.
  With **Send All BOMs**, every active default BOM is kept in frePPLe (changed BOMs synced on a schedule).
- **Frepple Planned Order** — the plan's proposed purchases and work orders; selected rows become **draft**
  Material Requests / Work Orders (nothing is submitted).
- Reports: **Project BOM Drill Down** (Project → store → SO line → BOM levels, make / buy, shortage) and
  **Item Lead Time Check** (PO-to-receipt days per item).
- **Stock Settings → Item Lead Time from Purchase Receipts** — keeps Item Lead Time Days up to date from
  receipt history (median or average), every N days.

Install alongside this app:

```bash
bench get-app https://github.com/VARDHANA87/frepple_connector --branch develop
bench --site <site> install-app frepple_connector
bench --site <site> migrate
bench restart    # running workers cannot import a newly installed app until they restart
```

A frePPLe instance is needed too: `scripts/frepple/` in that repo has a no-root install
(`setup_local.sh`, `start.sh`, `stop.sh`) and a server install (`install_system.sh`). See its README for
setup and the planner workflow.

#### License

MIT
