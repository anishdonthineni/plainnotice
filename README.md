# PlainNotice

Turn confusing official letters (lease notices, benefits decisions, medical bills) into plain-English deadlines, warnings, and a to-do list. Built for EvoHacks 2.0, theme: Projects for Social Good.

**Live demo:** https://claude.ai/artifact/4sbvGfjmVdjyXL3RiesKa6 (or open `index.html` locally)

## Run it
No install, no build, no API keys, no accounts.
1. Open `index.html` in any modern browser (works offline).
2. Click **Try a sample** to see the full workflow, or paste the text of your own letter and click **Decode this notice**.

## What it does
- **Deadlines:** finds dates (`December 3, 2026`, `12/15/2026`) and relative deadlines (`within 10 days`), sorts them, shows days remaining with color-coded urgency.
- **What you must do:** extracts instruction sentences ("must", "shall", "remit", "respond").
- **Watch out:** flags eviction, termination, added fees, garnishment, court hearings, waived rights, and the right to dispute or appeal. Each flag shows the sentence that triggered it.
- **Money mentioned:** dollar amounts with their source sentence.
- **Plain-English version:** legal jargon is highlighted and explained in place.
- **Reading level:** Flesch-Kincaid grade estimate.
- **Accessibility:** read-aloud (Web Speech API), larger-text toggle, keyboard focus styles, screen-reader live region, light/dark theme.
- **Privacy:** everything runs in the browser. Nothing is uploaded and no network requests are made.

## How the code works (for reviewers)
Single file, plain HTML/CSS/JS, no libraries.
- `run()` is the main pipeline: normalize text, split into sentences, then run each detector.
- `dates()` uses one regex for month-name and numeric dates and validates each parsed date.
- `when()` compares a date to today and returns days left plus an urgency level.
- `RISKS` is a table of `[regex, message, severity]` rules; the first matching sentence is shown as evidence.
- `GLOSS` is the jargon glossary; one longest-match-first regex applies it.
- `sy()` is a syllable heuristic feeding the Flesch-Kincaid formula.
- `speak()` / `copyList()` handle read-aloud and clipboard, with fallbacks and error messages.

## Design choices
Rules instead of a hosted AI model, on purpose: results are predictable and explainable, every flag points to its source sentence, and sensitive documents never leave the device.

## Limitations
It is a reading aid, not legal advice. Pattern matching can miss context, dates written in unusual formats, and non-English letters. The reading grade is an estimate. Always check the original letter and ask a trusted person or legal aid (US: dial 211, lawhelp.org).

## Built during the event / AI credit
All code and text were created during EvoHacks 2.0. No pre-existing code, templates, assets, or external libraries. AI helped plan and debug the code

## Roadmap
Photo/PDF input with on-device OCR, calendar export, more languages and a community-reviewed glossary, letter-type templates, and testing with legal aid clinics.
