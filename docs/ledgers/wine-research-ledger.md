# Wine Research & Agent Ledger

**Append-only log for wine-related research (Egyptian dockets, Linear A/B wine tablets/sealings, scrapers, agents).**
Follows revvel-standards OWNER RULES: never delete, append only, dated entries.

## 2026-11-04 — Initial setup and research summary (Grok team)

### Repos reviewed
- revvel-standards: SSOT standards.
- tartaria-tablets (private): Tărtăria book research.
- linear-a (private): Linear A workspace.
- revvel-hail: this governance/docs home.
- mindmappr / mindmappr-agents / mindmappr-setup / mindmappr-data: existing mindmap/agent infrastructure (REX etc. on Telegram; Telegraph saves noted).

### Egyptian wine dockets summary
Primary sources: Černý 1965 (Tutankhamun labels, pp. 21-22: Year 4/5, irp/nḍm/šdḥ nfr nfr, estates of Aton/Tutankhamun, Western River, vintners Aper-reshep, Nen, Rer, Khaa etc.). Amarna: Petrie 1894 / Pendlebury 1951. Malqata: Hayes 1951. Secondary: Eriksson 2012 DIVA thesis.

### Linear A wine mentions (AB131 / VIN)
From Salgarella 2020 Ktèma 45 and GORILA: HT 9a.1, 13.2, 17.1, 19.2, 23a.2, 27a.8/27b.2.6, 28a.4/28b.3.4.5, 30.2.5, 35.4, 44a.4/44b.3, 60.2, 62[+]73.1, 89.5, 91.4, 98b.2, 99a.2, 100.4, 114a.3, 121.3, 123+124a.3, 130.6 (Haghia Triada); Khania, Zakros (incl. ZA Zb 3 VIN 32), Phaistos, Knossos Zb, Arkhanes, Pyrgos, etc. Full list requires GORILA volumes. HT 13 is a classic wine list tablet.

### Linear B wine mentions
Pylos: Wine Magazine (Rooms 104-105) ~48 sealings (Wr 1358-1361 VIN + e-ti-wa-/me-ri-ti-jo); Vn 20 (large assessment); Un series. Knossos: Gm 840, Fs series, etc. Palmer 1994 Aegaeum 10 is the key monograph (Ch. 7 on nodules).

### Agent / scraper / automation notes
- User requested dedicated wine research agent: LM Studio primary (local), OpenRouter fallback (Venice/Dolphin uncensored preferred; no free model instantiation).
- Scraper for artifacts to database: location TBD (check linear-a data/ledger, revvel-standards, or Notion). To be automated locally first.
- GitHub Actions: billing issues; user has toggled includes/excludes. Need self-hosted or local workaround so function works with/without paid Actions.
- mindmappr: fix to run on local drive; Telegraph saves already handled (no new needed); Rex / googlieeyes_bot Telegram.

**Next actions:** Create/configure WineResearch agent (or extend CorpusBot/Decipherer), implement scraper, log database location, mindmappr local setup, Actions workaround. All further work appends here.

---

## 2026-11-04 — Wine DB bootstrap (Grok Bot executor)
- LM Studio: http://localhost:1234/v1 NOT reachable from the cloud box (curl exit 7). The box can't reach Audrey's localhost, so this says nothing about her machine. Test it locally: `curl -s http://localhost:1234/v1/models`.
- DB: SQLite `artifacts.sqlite` (box: /workspace/wine-research and ~/wine-research). There's no mindmappr-data or linear-a/data path to put it in.
- Loaded: linear_a = 89 documents that have VIN/VINb/𐙇 (AB131). They come from the lineara.xyz dataset (linear-a repo, src/grammar/lineara.xyz/LinearAInscriptions.js). By site: HT 46, KH 12, PH 8, ZA 7, KN 5, ARKH 2, PK 2, PE 2, plus 1 each from Crete, Kea, Pyrgos, Thera and Tylissos. Each record has a GORILA volume and PDF page from the dataset link. Printed pages are not verified. 16 records have no GORILA ref (GAP).
- GAPs: the Salgarella 2020 Tables 1–3 cross-check is not done. Linear B (Palmer 1994; Pylos Wr/Vn, KN Fs/Gm/Uc, TH Gp) has 0 records. egypt_tut/malqata/amarna (Černý 1965; Griffith Institute) have 0 records. Nothing was made up.
- Workflows: linear-a tests.yml runs on push and pull_request, on ubuntu-24.04. revvel-hail has no .github/workflows. Proposal (not applied): change `on:` to workflow_dispatch only, or use runs-on: self-hosted.
- MindMappr: mindmappr-setup and mindmappr-data exist; there is no `agents` repo. mindmappr-queue.sh hardcodes /opt paths. The local setup doc points to LM Studio and reuses Rex/googlieeyes_bot. Nothing new was created.
---

## 2026-11-04 (America/Denver): Linear B, Egyptian jar labels, Salgarella cross-check
- DB: ~/wine-research/artifacts.sqlite (rebuilt from cached sources; previous file kept, nothing deleted). Totals: linear_a 99 (89 lineara.xyz + 10 Salgarella-only GAP rows), linear_b 61, egypt_tut 34, amarna 201, malqata 0.
- linear_b: 54 VIN docs found by crawling DAMOS (damos.hf.uio.no/ajaxitem/1–6600, about 5932 live items, CC BY-NC-SA 4.0). Each row has a DAMOS permalink. By site: PY 17, KN 17, TH 24, MY 3 (including 7 Salgarella-only GAP rows). Palmer 1994 pages are not verified (GAP).
- Salgarella 2020 (Ktèma 45, author PDF repository.cam.ac.uk, DOI 10.17863/cam.52619), Tables 1–3:
  - Linear A: 49 of 59 docs matched. 10 are missing from lineara.xyz and were inserted as gap rows: ARKH2, ARKH3a, ARKH5, KH5, KH18, KH60, KH61, KH85, PH Wy421, ZA10b. 40 lineara.xyz VIN docs are not in Tables 1–2.
  - Linear B: 53 of 60 matched. Not in DAMOS VIN results: PY C-7063 (DAMOS has KN C 7063, so this is probably a site error in my transcription; check), TH Gp165, 167, 186, 197, 231, 233.
  - Pages are cited by PDF folio; the printed Ktèma pages are a GAP.
- egypt_tut: Griffith Institute Carter archive pages (griffith.ox.ac.uk/gri/carter/NNN.html, 620 crawled at 1 req/s): 32 pages mention wine. Merged with "The Wine Jars Speak" (Uppsala thesis, DiVA diva2:528049) catalogue Tut 1–26, which gives Černý 1965 page and No., regnal year, estate and vintner. 26 rows cite Černý; 8 rows have no verified page (GAP).
- amarna: 201 labels from the same thesis catalogue, citing Fairman & Černý 1951 / Petrie 1894 plates. They are secondary transcriptions; the primary plates were not checked (GAP).
- malqata: 0. The Hayes 1951 JNES PDFs (imalqata.wordpress.com) only have labels in figures and the OCR is unusable (GAP). Nothing was fabricated.
- Scripts: scrape_linear_b_damos.py, scrape_tut_griffith.py, load_wine_jars_speak.py, crosscheck_salgarella.py, run.sh (all cached, polite delays).
---

## 2026-11-04 evening (America/Denver): verification pass, Malqata Met scrape, wine_facts, source library
- Schema (additive only): artifacts.verification_status|verified_source|verified_page|verified_at|verification_notes; tables wine_facts and source_files. Original columns never overwritten; nothing deleted.
- Counts now: linear_a 103; linear_b 67; egypt_tut 34; amarna 201; malqata 98. wine_facts 16. source_files 6651 (~51 MB under library/).
- Verification (verified / partial / unverified):
  - linear_a: 7 / 83 / 13. SigLA+CEFAEL confirmed ARKH2, ARKH3a, ARKH5, KH18, KH60, KH61, KH85, ZA10b (GORILA EtCret 21.3 scan pages). Salgarella Ktèma 45 printed pages mapped via Persée to 161–171 (Tables 1–3 = pp.163–165). 13 still unverified (mostly newer finds / no second source). GORILA printed pagination still GAP (scans not stored; linear-a policy). PHWY421 ↔ PHWy42 partial crosswalk; SigLA 404 for PH Wy 421.
  - linear_b: 7 / 60 / 0. TH Gp 165,167,186,197,231,233 verified in DAMOS with dotted VIN (earlier scraper miss). PY C-7063 retained as Salgarella gap; DAMOS has KN C-7063 with VIN (probable table site error). Palmer 1994 full text still not open (GAP); chapter TOC facts only.
  - egypt_tut: 26 verified (Černý page present) / 8 partial (Griffith wine-jar cards without Černý; Beinlich on 432, 536).
  - amarna: 201 partial (thesis catalogue; primary plates not re-checked).
  - malqata: 98 partial from Met Collection API wine jar labels (17.10.x). Hayes 1951 PDFs cached; figure OCR still unusable for per-label text (GAP).
- New scripts: verify.py, extract_wine_facts.py, library_index.py, scrape_met_malqata.py, scrape_sigla.py; Linear A/B scrapers fixed (wine glosses; dotted VIN). run.sh chains them. Library mirrored under ~/wine-research/library and /workspace.
---
