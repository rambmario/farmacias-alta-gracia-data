# On-duty pharmacies in Alta Gracia

Public JSON feed (GitHub Pages) for the Flutter app **Farmacias de Turno Alta Gracia**. The dataset is scraped from [Alta Gracia Viva](https://www.altagraciaviva.com.ar/farmacias-de-turno-en-alta-gracia/) and published here for the app to consume.

**JSON:** https://rambmario.github.io/farmacias-alta-gracia-data/farmacias.json

## Schema

| Field | Meaning |
|---|---|
| `schemaVersion` | Contract version (`1`) |
| `dutyWindow` | Duty runs `08:30`–`08:30` the next day (`America/Argentina/Cordoba`) |
| `source` | Origin site (`id`, `name`, `url`) |
| `entries` | Duty assignments: date, pharmacy name, address, phone |

The document also includes `timezone`, `generatedAt` and `fetchedAt`.

## Update cadence

A private GitHub Actions workflow publishes at **07:00 and 09:00** (Córdoba, UTC−3), around the 08:30 duty rollover.

## Validation

A new dataset is published only when parsing looks healthy:

- **Confidence** (`parseConfidence`): `HIGH`, `MEDIUM` or `LOW`. Low confidence is not published.
- **Warnings**: missing phones, unrecognized text, small calendar gaps. Too many warnings (or a sharp drop vs the previous run) block publication.
- **Previous dataset preserved**: on `NO_CHANGE` or any `FAILED_*` status, the last good `farmacias.json` is left untouched.

Run diagnostics: [`update-report.json`](update-report.json) and [`update-summary.txt`](update-summary.txt). Privacy policy: [privacy.html](https://rambmario.github.io/farmacias-alta-gracia-data/privacy.html).

Android package: `com.marioramb.farmaciasaltagracia` (no public Google Play listing yet).
