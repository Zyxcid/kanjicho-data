# kanjicho-data

The open dataset shipped inside **[Kanjichō](https://github.com/Zyxcid/Kanjicho)** —
a JLPT kanji practice PWA (N5–N1) with FSRS-6 spaced repetition.

This repository exists for two reasons:

1. **License compliance.** The dataset is derived from openly-licensed
   sources that use ShareAlike licenses (CC BY-SA). Publishing the derived
   data under the same license is the clean way to satisfy those
   obligations — the app's own code stays proprietary, the data stays open.
2. **Giving back.** Anyone building a kanji study tool can reuse this
   curated, quiz-oriented dataset: kanji entries with selected readings,
   two example words per kanji, stroke-order paths, and component
   decompositions — all JSON, all offline-friendly.

## Contents

| Folder | Files | Contents | License of the file |
|---|---|---|---|
| `kanji/` | `n5.json` … `n1.json` | Per-kanji entries: readings (kana + romaji), meanings, primary readings, stroke count, JLPT level, unit | **CC BY-SA 4.0** (derived from KANJIDIC2) |
| `examples/` | `n5_examples.json` … `n1_examples.json` | Two example words per kanji (word, reading, meaning, on/kun) | **CC BY-SA 4.0** (derived from JMdict) |
| `strokes/` | `strokes_n5.json` … `strokes_n1.json` | Per-kanji stroke paths (viewBox 0 0 109 109, one path array per stroke) for drawing animations | **CC BY-SA 3.0** (derived from KanjiVG) |
| `components/` | `components_n5.json` … `components_n1.json` | Component decomposition equations (e.g. 験 = ⾭ + 馬) from stroke-group structure | **CC BY-SA 3.0** (derived from KanjiVG) |

Root files: `LICENSE` (CC BY-SA 4.0) and `LICENSE-CC-BY-SA-3.0.txt` hold the
full legal texts. `NOTICE.md` maps every file to its source and attribution.

**Dataset size:** 2,211 kanji (N5 79 · N4 166 · N3 367 · N2 367 · N1 1232),
3,614 primary readings, 2 example words per kanji (N1 name kanji that have no
common example words are honestly wordless rather than filled with junk).

## Sources and attribution

| Source | What was taken | License |
|---|---|---|
| [KANJIDIC2](https://www.edrdg.org/wiki/KANJIDIC_Project.html) © Electronic Dictionary Research and Development Group | Kanji readings, meanings, stroke counts | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
| [JMdict](https://www.edrdg.org/jmdict/edict_doc_depr.html) © Electronic Dictionary Research and Development Group | Example words, readings, glosses | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |
| [KanjiVG](http://kanjivg.tagaini.net/) © Ulrich Apel | Stroke paths, component decomposition | [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/) |
| [JLPT_Vocabulary](https://github.com/Bluskyo/JLPT_Vocabulary) © Bluskyo | JLPT level assignments (N5–N1) | MIT |
| [Jiten frequency lists (global)](https://jiten.moe/frequency-dictionaries) © Jiten | Build-time frequency signal (primary layer of the hybrid; see below) | [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) |

**KANJIDIC2/JMdict acknowledgement:** This dataset uses data from the
KANJIDIC2 and JMdict/EDICT dictionary files in accordance with the licence
terms of the Electronic Dictionaries Research and Development Group, and is
used in accordance with the licence stated at
<https://www.edrdg.org/edrdg/licence.html>.

### About the frequency signal (read this before forking the pipeline)

Reading order and example-word selection are decided by a **hybrid
build-time frequency signal**:

1. **Jiten global frequency list** (jiten.moe, CC BY-SA 4.0) — primary
   layer: word+reading pairs attested in the top 10,000 media-corpus ranks
   (3.18 B characters across 16,272 Japanese media titles) drive reading
   ranking, example slots, and primary readings.
2. **JMdict common-word markers** (`ke_pri`/`re_pri`) — fallback layer for
   words not attested above the cutoff (editorial/newspaper register).

The frequency *numbers* never enter the published files — only the
*decisions* informed by them (which reading is primary, which two example
words fill the slots). Keep it that way: if you extend the pipeline, use
frequency as a signal, do not copy the list into the output.

### Changes made to the source data (required notice for CC BY-SA)

We did not redistribute the sources verbatim. Data was selected, filtered,
re-ranked, and restructured: only kanji with modern JLPT levels are kept;
readings are split into on/kun with a derived "primary" subset (see the
pipeline description below); meanings are trimmed; each kanji gets at most
two example words, chosen with corpus-frequency and common-use (JMdict
`ke_pri`/`re_pri`) gates so that rare or archaic dictionary forms (e.g.
馬験, 対い) are excluded; stroke paths are converted from KanjiVG SVG groups
into compact JSON arrays; component equations are derived from KanjiVG
stroke-group structure. See `NOTICE.md` and the app repository for the full
pipeline description.

## Provenance / how to regenerate

The generator pipeline lives in the private Kanjichō app repository
(`scripts/`): `convert_kanji.py` (KANJIDIC2 + levels → `kanji/`),
`rerank_readings.py` + `build_examples.py` (JMdict + Jiten hybrid gates →
`examples/` and primary readings), `build_strokes.py` (KanjiVG SVG →
`strokes/`), `build_components.py` (KanjiVG stroke groups → `components/`).
Raw sources are downloaded from the links above. The data in this repository
is synced from the app's `src/data/` on every release — file names match the
app's internal names exactly (`n1.json`, `n1_examples.json`,
`strokes_n1.json`, `components_n1.json`, …).

## Licence summary (not legal advice)

Everything in this repository is available under the licences listed in the
table above; the ShareAlike obligation means that if you build a derived
*dataset* from these files, that dataset must carry the same CC BY-SA
licence and its attribution chain. Using the data inside an app (open or
commercial) is fine as long as attribution is kept — the Kanjichō app shows
it in its Help → "Data sources" panel.
