# VxReceiptTotalCost

```
                 o               o
                  \_____  /\    /
                   \    \/__\_ /
                   _\_________/_
                   |           |
                   | (o)   (o) |
__   __  __ _  _ __     _   _ __  __
\ \ / / / _` || '__|| || | | |\ \/ /
 \ V / | (_| || |   | || |_| | >  <
  \_/   \__,_||_|   |_| \__,_|/_/\_\
```

Shows the **Total Cost** box in the header of the Purchase Receipts form (PO302000) in Acumatica ERP.

Acumatica hid this box in 2024 R1. The field behind it, `POReceipt.CuryOrderTotal`, still exists and is still stored; it is just not displayed. This customization project makes it visible again, read-only, in the right-hand header column under Unbilled Quantity. It adds no table, no column, no code, and no change to posting, billing, or landed costs.

> **Status: not released.** Nothing in this folder has been published or tested in a tenant yet. See `CHANGELOG.md`.

## Read this before you rely on the number

Acumatica hid the box on purpose. Its stated reasons were that a purchase receipt is not a financial document and that the total did not reflect line discounts correctly. This project does not change how the number is calculated; it only shows what Acumatica stores. Before your receiving team uses it to check a packing list or vendor invoice, compare it against the total of the Ext. Cost column on a few receipts, including one with a discounted line, one with a freight line, a return, and a transfer receipt. If the numbers disagree on normal receipts, do not use this project.

## What the project contains

| Item | What it does |
|---|---|
| DAC override on `PX.Objects.PO.POReceipt.CuryOrderTotal` | Sets the field's `PXUIField` `Visible` property to true |
| Screen change on PO302000, control `edCuryOrderTotal` | Sets the control's layout `Visible` property to true. Without this the Classic UI page markup keeps the box hidden even when the field attribute says visible |

The whole project is the file `package/project.xml`.

## Supported versions

| Acumatica release | Status |
|---|---|
| 2025 R2 (25.2xx) | Planned for 1.0.0, not yet tested |
| 2025 R1, 2026 R1 | Not tested |
| 2024 R1, 2024 R2 | Not tested (the box was first hidden in 2024 R1) |
| 2023 R2 and earlier | Not needed; the box is visible out of the box |

A customization project has to be republished after every Acumatica upgrade. Check this table for a tag matching the release you are upgrading to before you upgrade.

## Install

1. Download the release zip for your Acumatica version (or `package/project.xml`).
2. Open **Customization Projects** (SM204505) and click **Import**.
3. Tick the imported project **and keep every project that is already published ticked**. Publishing with only some projects ticked unpublishes the rest.
4. Click **Publish**. Publishing restarts the site; do it outside business hours.
5. Open any purchase receipt. The Total Cost box should appear under Unbilled Quantity.

If the box does not appear after publishing, open the project in the Customization Project Editor, go to Screens > PO302000, select Total Cost in the Document form, open Layout Properties, set **Visible** to True, save, and publish again. Whether the import keeps that screen setting on its own is still being confirmed; see `CHANGELOG.md`.

## Modern UI

The screen change above applies to the Classic UI of PO302000. In 2025 R2 and later, forms open in the Modern UI by default. Whether the field attribute change alone is enough there has not been confirmed. If you open PO302000 in the Modern UI and do not see the box, switch the form to the Classic UI from the form's menu, or open an issue with your version.

## Uninstall

Untick the project on Customization Projects and publish again (keeping everything else ticked). Both items in this project are reversed by unpublishing. Nothing is left in the database.

## Upgrade the project

Import the new version, untick the old one, tick the new one, keep unrelated projects ticked, and publish once.

## Known limitations

1. The value is whatever Acumatica stores in `POReceipt.CuryOrderTotal`. Acumatica's own statement is that it does not reflect line discounts.
2. On returns and transfer receipts the value may be zero or may not represent vendor cost.
3. Classic UI only until the Modern UI check is done.
4. One package per Acumatica release. Republish after every upgrade.
5. If another published project also sets Visible on this control, Acumatica's customization levels decide which wins. This project does not set a level.

## License

Apache License 2.0. See `LICENSE` and `NOTICE`. If you redistribute this project, keep both files. "Variux" and the Variux logo are trademarks of Variux, Inc.; the license covers the code, not the name or logo (Apache 2.0, section 6).

## Support

Open an issue in this repository. There is no service level attached to this project. Variux provides Acumatica services commercially; that is separate from this project.
