# IOC Extractor & Defanger

![Type](https://img.shields.io/badge/type-client--side-blue)
![Dependencies](https://img.shields.io/badge/dependencies-none-green)
![License](https://img.shields.io/badge/license-MIT-green)

A single-page tool for SOC and DFIR work. Paste any report, alert, or email
and it pulls out every indicator of compromise, de-duplicates them, and
defangs them for safe sharing. Everything runs in the browser — **no data
leaves the page**, which matters when the text you're pasting is from a live
investigation.

It's a companion to quick triage: drop in a messy blob, get clean,
categorized indicators you can paste straight into a ticket, a block list,
or another tool.

## What it extracts

- **IPv4** and **IPv6** addresses (compression-aware)
- **URLs** and **domains**
- **Email addresses**
- **MD5**, **SHA-1**, and **SHA-256** hashes
- **CVE** identifiers

## Features

- **Reads defanged input automatically.** Reports full of `hxxp://`,
  `1.2.3[.]4`, and `user[@]domain` are refanged before extraction, so
  nothing is missed.
- **Defangs output by default.** Copy indicators in `hxxps://evil[.]com`
  form, ready to share without creating a live clickable link.
- **Per-category and bulk copy**, plus **JSON export** for feeding other
  tools.
- **De-duplicated and sorted**, with live counts.
- **No backend, no dependencies, no tracking** — one HTML file.

## Usage

Open `index.html` in any modern browser. That's it.

Or deploy it as a static site (e.g. Vercel, Netlify, GitHub Pages) — there's
no build step, so the single file deploys as-is.

Click **Load sample** to see it work on a realistic incident snippet.

## How it works

Input is first *refanged* (defang notations normalized back to real
indicators), then matched with a set of patterns tuned to cut common noise —
IPv4 octets are range-validated, file extensions like `.pdf` are excluded
from domains, and IPv6 timestamps/MAC fragments are rejected. Output is
optionally *defanged* for safe sharing.

## Limitations

Extraction is pattern-based, so results are **leads to verify, not ground
truth**. A version string like `1.2.3.4` can read as an IPv4 address, and
unusual IPv6 forms (zone IDs, IPv4-mapped addresses) aren't covered. Always
sanity-check before acting on an indicator.

## License

Released under the [MIT License](LICENSE). Defensive and educational use.
