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
