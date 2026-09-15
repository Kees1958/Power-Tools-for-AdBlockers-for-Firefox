# Third-party licenses and attribution

This project (uBlock-Stripped-Dynamic) is licensed under the GNU General
Public License v3.0 — see `LICENSE.txt`. The following components are
derived from third-party sources under their own, different licenses.
Each is documented here as the single canonical source — not scattered
across code comments — per this project's own "declared, not
reconstructed from memory" convention (see e.g. `RULESET_COMPANIONS`).

---

## `vendor/autoconsent/` — MIXED provenance, resolved (per-entry sourced)

- **Files:** `vendor/autoconsent/eval-snippets.js`,
  `vendor/autoconsent/rules/rules.json`
- **`vendor/autoconsent/LICENSE`** (MPL-2.0, fetched verbatim from
  `duckduckgo/autoconsent`'s own repo) applies to part of this
  directory's content — confirmed via `rules.json`'s own `_provenance`
  field, which was more detailed than its top-level `_comment` and
  resolves what first looked like a contradiction between the two files:

  - **22 of 45 rule entries** (`rules.json`, was 11 of 26, not 12 —
    see correction note below) carry `_source: "ddg-autoconsent
    (<filename>.json)"` — genuinely **adapted (not copy-pasted)** from
    `duckduckgo/autoconsent`'s own real, tested rule definitions.
    Original 11 read from a pinned commit (`9e4e640d...`); batch 4's
    11 additional entries (8.4.9) read from the `main` branch instead
    — dated, not commit-pinned, since GitHub's commit API was
    rate-limited at fetch time. Two further candidates (Transcend,
    Sirdata) were deliberately deferred — see CHANGELOG for why.
    **MPL-2.0 applies to all 22.**
  - **15 of 45 rule entries** carry `_source` starting with
    `"hand-authored"` — genuinely independently written against each
    CMP's own public documentation/markup, confirmed via live-site
    inspection or (Silktide specifically) multiple independent real
    production deployments plus that project's own public config
    schema — no DDG code involved in any of these 15. **MPL-2.0 does
    not apply to these.** (Corrected from an earlier 23/14 split —
    Silktide's `_source` string carries extra verification detail
    beyond the plain word "hand-authored" and was miscounted in an
    earlier pass; verified directly against `rules.json` before this
    release, not recalculated from memory.)
  - **8 new entries (added 8.4.7/8.4.8, three batches)** carry
    `_source: "consent-o-matic (<filename>.json)"` — adapted the same
    way, from `cavi-au/Consent-O-Matic`'s own real rule definitions.
    **MIT applies to these — see below**, not MPL-2.0.
  - `eval-snippets.js`'s top-of-file "NOT a fork" claim is accurate as a
    whole-file/whole-project statement (this directory is not a fork of
    duckduckgo/autoconsent), but doesn't capture that a genuine subset
    of individual entries within it were adapted from DDG's code —
    `rules.json`'s more detailed `_provenance` field is the accurate,
    complete picture; the file-level `_comment` undersold it.

  **Per-file MPL-2.0 notices aren't practical here** (mixed at the
  individual-rule level within both files) — MPL-2.0 §3.1 itself
  anticipates exactly this: *"If it is not possible or desirable to put
  the [license] notice in a particular file, then You may include the
  notice in a location (such as a LICENSE file in a relevant
  directory)"* — which is what `vendor/autoconsent/LICENSE` now does.

- **`js/scripting/autodeny-snippets.generated.js`** is compiled at
  build time from both files above (see `tools/build-autodeny-bundle.mjs`)
  and inherits the same mixed status — the MPL-2.0-derived portion
  flows through into the generated file along with the hand-authored
  and MIT-derived portions.

---

## Consent-O-Matic (8 rule entries, added 8.4.7/8.4.8, three batches)

- **Source:** https://github.com/cavi-au/Consent-O-Matic
- **License:** [MIT License](https://github.com/cavi-au/Consent-O-Matic/blob/master/LICENSE)
- **Copyright:** © 2019-2022 Janus Bager Kristensen and Rolf Bagge, CAVI —
  Centre for Advanced Visualization and Interaction, Aarhus University

**Attribution:**

> Cookie-consent detection/reject logic for TYPO3 Cookieman,
> tarteaucitron.js, Piwik PRO Consent Manager, GDPR Modal, Drupal EU
> Cookie Compliance, Evidon, ST CMP v2, and a Thai-market DPDPA-style
> consent popup adapted from Consent-O-Matic by CAVI, Aarhus
> University, licensed under the MIT License. This copyright notice is
> the only term MIT requires to be preserved — no copyleft, no
> non-commercial restriction, unlike the two entries above.

Candidates using build-hash-dependent CSS-in-JS class names (batch 1:
Admiral, Mediavine's save-button selector; batch 2: Schibsted; batch 3:
google_cwiz — Google's own opaque MDC classnames plus position-
dependent nth-child selectors, a fragility type the earlier automated
scan didn't catch, found only on manual inspection) were deliberately
excluded across all three batches as too fragile to translate
faithfully — see CHANGELOG for the full reasoning. ~190 CMPs remain in
Consent-O-Matic's own rule set beyond these three pilot batches.

---

<!-- RETIRED (v9.1.7, pre-dates this Firefox port — found while checking
     this document's Disconnect entries after the 1.0.1 ruleset_
     disconnect_other removal, not something this port caused)
     — "Disconnect ConsentManagers (1 domain, added 8.5.4)"
     (transcend.io, Disconnect's services.json ConsentManagers category,
     CC BY-NC-SA 4.0) removed entirely along with
     buildWorryFreeExtraBlocklistSourceText() and its only caller,
     ruleset_worryfree_extra — see that function's own retirement
     comment in tools/build-rulesets.mjs ("the 'adult-site ad servers +
     transcend.io' blocklist and its underlying five/one-source merge
     machinery are gone, per explicit request, not rescoped"). This
     entry was never removed from this document at the time — a
     pre-existing gap, not a new one. No attribution entry needed since
     nothing in the shipped extension derives from Disconnect's
     ConsentManagers category anymore. -->

---

## DuckDuckGo Tracker Radar (compacted dataset) — re-added this release

BRAVE VARIANT — this dataset and its lookup module were ported verbatim
from uBlock-Stripped-Dynamic v9.2.6 (the last version to bundle them
before the parent project deleted both entirely in v9.3.0). Re-added
here per explicit request, for a new "known tracker" Y/N column in the
Matrix panel — a simpler feature than the "breakage risk" column this
data originally fed in that parent project, which doesn't exist in this
variant at all.

- **File:** `js/data/tracker-radar-data.js` (ported, not regenerated —
  `tools/build-tracker-radar.mjs` has not been ported to this variant's
  own tools/ yet, so this dataset can't be refreshed here until it is)
- **Source:** https://github.com/duckduckgo/tracker-radar
- **License:** [Creative Commons Attribution-NonCommercial-ShareAlike 4.0
  International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
- **Copyright:** © Duck Duck Go, Inc.

**Attribution (TASL — Title, Author, Source, License):**

> "Tracker Radar" data by Duck Duck Go, Inc., available at
> https://github.com/duckduckgo/tracker-radar, licensed under
> [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
> This project's own compacted subset (`js/data/tracker-radar-data.js`)
> is a derivative work and is itself distributed under the same
> CC BY-NC-SA 4.0 terms — see that file's own header for the exact build
> parameters (region/prevalence filtering) applied to produce it.

**What CC BY-NC-SA 4.0 means in practice for this specific file only**
(does not extend to the rest of the GPL-3.0-licensed extension — this
is a bundled, separately-licensed data file, not a derivative of the
extension's own code):
- **Attribution** — this notice, kept up to date, satisfies that term.
- **NonCommercial** — this specific dataset may not be used for
  commercial purposes without a separate license from Duck Duck Go, Inc.
  (they explicitly offer commercial licensing — see their repo).
- **ShareAlike** — any further redistribution of this compacted dataset
  (not the extension as a whole) must carry the same CC BY-NC-SA 4.0
  terms.

---

## Bundled libraries (`lib/`, `css/fonts/`) — found undocumented, added this release

These four ship their own `LICENSE` file directly in the tree but were
never referenced in this document at all — a pre-existing gap (confirmed
identical in the original pre-Brave-variant source, not introduced by
this fork) found during an accuracy audit. All four are permissive and
GPL-3.0-compatible; none require anything beyond the standard
copyright-notice preservation their own LICENSE files already state.

- **`lib/csstree/`** — MIT License. Copyright (C) 2016-2022 Roman
  Dvornov. Source: https://github.com/csstree/csstree
- **`lib/codemirror/`** (`codemirror.LICENSE`) — MIT License. Copyright
  (C) 2018-2021 Marijn Haverbeke and others. Source:
  https://codemirror.net/
- **`lib/codemirror/`** (`codemirror-quickstart.LICENSE`) — MIT License.
  Copyright (c) 2025 Bryan Gillespie. A separate, distinctly-licensed
  component bundled alongside the CodeMirror core above — two LICENSE
  files in the same directory because they're two different works, not
  one accidentally duplicated file.
- **`lib/regexanalyzer/regex.js`** — The Unlicense (public domain
  dedication) — foo123's RegexAnalyzer, confirmed via that project's own
  GitHub repository (https://github.com/foo123/RegexAnalyzer), which
  ships an `UNLICENSE` file and displays "Unlicense license" on its own
  repo page. No LICENSE file ships in `lib/regexanalyzer/` itself in
  this project — noted here as the canonical record instead, per this
  document's own "single canonical source" convention.
- **`css/fonts/Inter/`** — SIL Open Font License, Version 1.1. Copyright
  (c) 2016-2020 The Inter Project Authors (https://github.com/rsms/inter).

---

<!-- RETIRED (this Firefox port, v1.0.1) — "Disconnect (Cryptomining,
     Fingerprinting)" (ruleset_disconnect_other, one static ruleset,
     Disconnect's services.json Cryptomining/FingerprintingInvasive/
     FingerprintingGeneral categories, CC BY-NC-SA 4.0) removed entirely.
     Not a content decision — Firefox ships this same tracking-protection
     coverage natively via Enhanced Tracking Protection, so shipping it
     again as a DNR ruleset was redundant on Firefox specifically (see
     CHANGELOG's 1.0.1 entry). The Chrome build this was forked from
     still ships it under the same license terms this entry used to
     document. History before this removal (five lists reduced to one,
     safety-filter removal, etc.) is preserved in the Chrome-side
     codebase's own THIRD_PARTY_LICENSES.md, not repeated here. No
     attribution entry needed in THIS document since nothing in this
     Firefox build derives from Disconnect's Cryptomining/Fingerprinting
     categories anymore. -->

---

<!-- RETIRED (v9.1.7) — "Worry-free social media block list (Disconnect
     + Ghostery)" removed entirely, per explicit request, along with the
     "Enable extra blocklist" grouped checkbox and the EasyList adult
     ad-servers + transcend.io list it also used to cover. Neither
     ruleset_worryfree_social nor ruleset_worryfree_extra exist anymore
     — see js/core/dnr-budgets.js's WORRY_FREE_SOCIAL_RULES_BASE_ID /
     WORRY_FREE_EXTRA_RULES_BASE_ID retirement comments for the full
     history. No attribution entry needed here since nothing in the
     shipped extension derives from Disconnect's Social category or
     Ghostery's social_media category anymore. -->
