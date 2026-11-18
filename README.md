# kanjicho-data

The open dataset shipped inside **Kanjichō** — a JLPT kanji practice
app (N5–N1) with FSRS-6 spaced repetition (source code not public).

> **Latest sync: 2026-11-18 (r81b)** — every file in this repository is
> byte-identical to the app's `src/data/` (sha256-verified at sync time).
> This sync carries the **Indonesian gloss audit (r81) + per-kanji overlay
> (r81b)**:
>
> - **r81 — 51 corrections** in `id_gloss.json`: polysemy fixes decided
>   per-kanji evidence (`present` → "menyerahkan" for 供呈奉献, `party` →
>   "kelompok" for 会党派隊, `draft` → "draf" for 案稿草, `train` →
>   "melatih" for 練錬鍛, `crane` → "burung bangau" for 鶴), KBBI spelling
>   (`anugerah`, `aktivitas`, `menaati`), mistranslations (`gloss` →
>   "kilau", `forge` → "menempa", `drill` → "latihan"), and 5 example-word
>   glosses (勤倹 "rajin dan hemat", 燎原 "api menjalar di padang", …).
> - **r81b — new map `k` (per-kanji overrides, 99 kanji / 107 pairs)**:
>   one English head word can mean different things on different kanji,
>   and a single global `m` map cannot express that. `k[kanji][en]`
>   overrides `m[en]` for that kanji only: 現/本 `present` → "saat ini"
>   while 供呈奉献 keep "menyerahkan"; 宴 `party` → "pesta" while 会党派隊
>   keep "kelompok"; 右 `right` → "kanan" but 当是 → "benar"; 鉛 `lead` →
>   "timah" while 率督連 keep "memimpin"; 皮 `hide` → "kulit (binatang)";
>   堤 `bank` → "tanggul"; 株 `stock` → "saham"; 息 `interest (on money)` →
>   "bunga" (redundant with `m`, kept in `m` only); 倍 `fold` → "-lipat";
>   表譜 `table` → "tabel" while 卓机案 → "meja"; and similar. Resolution
>   order in the app: `k[kanji][en]` → `m[en]` → English fallback.
>
> Kanji/examples/strokes/components/manifest are unchanged from the
> 2026-09-15 rebuild (79 primary readings corrected, 159 example-word sets
> cleaned).

This repository exists for two reasons:

1. **License compliance.** The dataset is derived from openly-licensed
   sources that use ShareAlike licenses (CC BY-SA). Publishing the derived
   data under the same license is the clean way to satisfy those
   obligations — the app's own code stays proprietary, the data stays open.
2. **Giving back.** Anyone building a kanji study tool can reuse this
   curated, quiz-oriented dataset: kanji entries with selected readings,
   up to two example words per kanji, stroke-order paths, component
   decompositions, and an Indonesian translation overlay — all JSON, all
   offline-friendly.

## Contents

| Path | Files | Contents | License of the file |
|---|---|---|---|
| `kanji/` | `n5.json` … `n1.json` | Per-kanji entries: readings (kana + romaji), meanings, primary readings, stroke count, JLPT level, unit | **CC BY-SA 4.0** (derived from KANJIDIC2) |
| `examples/` | `n5_examples.json` … `n1_examples.json` | Up to two example words per kanji (word, reading, meaning, on/kun) | **CC BY-SA 4.0** (derived from JMdict) |
| `strokes/` | `strokes_n5.json` … `strokes_n2.json`, `strokes_n1_idx.json` + `strokes_n1_p0..p3.json` | Per-kanji stroke paths (viewBox 0 0 109 109, one path array per stroke) for drawing animations. N1 is split into an index + 4 parts exactly as the app lazy-loads it; merge = concatenate the four part objects (the index maps kanji → part). | **CC BY-SA 3.0** (derived from KanjiVG) |
| `components/` | `components_n5.json` … `components_n1.json` | Component decomposition equations (e.g. 験 = ⾭ + 馬) from stroke-group structure | **CC BY-SA 3.0** (derived from KanjiVG) |
| `id_gloss.json` | — | Indonesian overlay: `m` (5,205 English kanji meanings → Indonesian), `w` (3,960 example words → Indonesian glosses), and `k` (per-kanji overrides, r81b: 99 kanji where one English head word needs a different Indonesian gloss on that kanji). Missing keys fall back to English; resolution order `k[kanji][en]` → `m[en]` → English. | **CC BY-SA 4.0** (translations of KANJIDIC2 meanings + JMdict glosses — a translation is an adaptation) |
| `manifest.json` | — | N5–N1 unit structure (which kanji belong to which study unit, in what order) | **CC BY-SA 4.0** (selection/ordering derived from KANJIDIC2 + the Jiten frequency signal) |

Root files: `LICENSE` (CC BY-SA 4.0) and `LICENSE-CC-BY-SA-3.0.txt` hold the
full legal texts. `NOTICE.md` maps every file to its source and attribution.

**Dataset size:** 2,211 kanji (N5 79 · N4 166 · N3 367 · N2 367 · N1 1232),
3,639 primary readings, up to 2 example words per kanji (44 N1 name kanji
have no common example words and are honestly wordless rather than filled
with junk).

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
`ke_pri`/`re_pri`) gates so that rare, archaic, or irregular dictionary
forms (e.g. 候由, 理り, 識る) are excluded while corpus-attested modern words
(e.g. 発つ) are kept; stroke paths are converted from KanjiVG SVG groups
into compact JSON arrays; component equations are derived from KanjiVG
stroke-group structure. The Indonesian overlay (`id_gloss.json`) is a
translation layer produced for the app (batch translation, manual
completion, and a line-by-line audit), published here because translating
CC BY-SA glosses creates a CC BY-SA adaptation. See `NOTICE.md` and the app
repository for the full pipeline description.

## Provenance / how to regenerate

The generator pipeline lives in the private Kanjichō app repository
(`scripts/`): `convert_kanji.py` (KANJIDIC2 + levels → `kanji/`),
`rerank_readings.py` + `build_examples.py` (JMdict + Jiten hybrid gates →
`examples/` and primary readings), `build_strokes.py` (KanjiVG SVG →
`strokes/`), `build_components.py` (KanjiVG stroke groups → `components/`),
and `scripts/id_translation/` (translation chain → `id_gloss.json`). Raw
sources are downloaded from the links above. The data in this repository is
synced from the app's `src/data/` on every release — file names match the
app's internal names exactly (`n1.json`, `n1_examples.json`,
`strokes_n1_idx.json` + `strokes_n1_p0..p3.json`, `components_n1.json`,
`id_gloss.json`, `manifest.json`, …).

## Licence summary (not legal advice)

Everything in this repository is available under the licences listed in the
table above; the ShareAlike obligation means that if you build a derived
*dataset* from these files, that dataset must carry the same CC BY-SA
licence and its attribution chain. Using the data inside an app (open or
commercial) is fine as long as attribution is kept — the Kanjichō app shows
it in its Help → "Data sources" panel.
