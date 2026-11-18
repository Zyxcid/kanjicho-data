# NOTICE — kanjicho-data

File-to-source mapping and required attributions for every data file in this
repository. Licence texts: `LICENSE` (CC BY-SA 4.0),
`LICENSE-CC-BY-SA-3.0.txt`.

## kanji/n5.json, n4.json, n3.json, n2.json, n1.json

Derived from **KANJIDIC2** (kanjidic2.xml.gz) — © Electronic Dictionary
Research and Development Group — used under
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
Fields taken and transformed: readings (→ `readings.on` / `readings.kun`),
meanings (→ trimmed English glosses), stroke count. NOT copied verbatim:
entries are filtered to modern JLPT kanji, reordered into study units, and
extended with derived fields (`primary_readings`, `romaji_readings`,
`order_index`, `unit`, `jlpt_level`).

`jlpt_level` values are derived from **JLPT_Vocabulary**
(<https://github.com/Bluskyo/JLPT_Vocabulary>) — © 2026 Bluskyo — MIT licence
(see below). Level assignments are factual data.

Kanji ordering and reading selection inside these files was decided using a
**hybrid frequency signal** — the global frequency list from **Jiten**
(<https://jiten.moe/frequency-dictionaries>) — © Jiten —
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/), used as the
primary signal, with JMdict common-word markers (`ke_pri`/`re_pri`) as
fallback — both build-time signals only: **no frequency values appear in
these files** (only decisions informed by them).

## examples/n5_examples.json … n1_examples.json

Derived from **JMdict/EDICT** (JMdict_e.gz) — © Electronic Dictionary
Research and Development Group — used under
[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).
Fields taken and transformed: headword (→ `word`), reading (→ `reading`),
gloss (→ `meaning`, first English sense), sense of on/kun (→ `type`).
NOT copied verbatim: at most two words per kanji, selected through
corpus-frequency and common-use gates (Jiten frequency ranks + JMdict
`ke_pri`/`re_pri` markers); rare-kanji forms (JMdict `rK`/`oK`/`iK`/`sK`
tags) and archaic words are excluded.

## strokes/strokes_n5.json … strokes_n2.json, strokes_n1_idx.json + strokes_n1_p0..p3.json, components/components_n5.json … components_n1.json

Derived from **KanjiVG** (<http://kanjivg.tagaini.net/>) — © Ulrich Apel —
used under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).
`strokes/*` are the SVG path `d` strings per stroke (viewBox 0 0 109 109),
converted to JSON arrays per kanji; the N1 set is split into an index +
four parts exactly as the app lazy-loads it (the parts are a byte-level
split of one merged map — concatenate the part objects to recover the
single file). `components/*` are decomposition equations derived from
KanjiVG stroke-group structure (e.g. 験 = ⾭ + 馬). NOT copied verbatim: only
path data / group ids are kept; the SVG documents, attributes, and
structure are dropped; only JLPT kanji are included.

## id_gloss.json

Indonesian translation overlay: `m` maps 5,205 English kanji meanings
(KANJIDIC2-derived glosses, the same strings used as keys in the app) to
Indonesian, `w` maps 3,960 example words to Indonesian glosses of their
JMdict senses, and `k` (added r81b) holds per-kanji overrides — 99 kanji
where a single English head word must gloss differently on that kanji
(e.g. 現/本 "present" → "saat ini" vs 供呈奉献 → "menyerahkan"). Translating copyrighted glosses creates an adaptation, so
this file is published under **CC BY-SA 4.0** like its sources: meanings —
© Electronic Dictionary Research and Development Group (KANJIDIC2);
glosses — © Electronic Dictionary Research and Development Group (JMdict).
The translations themselves were produced for the Kanjichō app (batch
translation, manual completion, line-by-line audit) and are contributed
under the same licence as the underlying data, as ShareAlike requires.

**2026-11-18 audit (r81):** 51 glosses corrected. Ambiguous English head
words were re-decided by looking at which kanji actually use them (the
`m` map is one-to-one across all kanji, so the majority reading wins):
`present` → "menyerahkan" (供呈奉献, not the gift sense), `party` →
"kelompok" (会党派隊連徒遭, not the celebration sense), `draft` → "draf"
(案稿草, not conscription), `figure` → "sosok" (姿像態, not numerals),
`right` → "kanan" (右), `letter` → "huruf" (字), `train` → "melatih"
(練錬鍛), `crane` → "burung bangau" (鶴), `spring` → "mata air" (泉),
`state` → "negara bagian" (州), `term` → "masa" (任期), `post` →
"jabatan" (職), and similar. Machine-translation slips were fixed
(`gloss` → "kilau" for 練, `forge` → "menempa" for 鍛, `drill` →
"latihan" for 練錬, `brunt` → "terpaan utama" for 衝, `bargain` →
"murah" for 廉), plus KBBI spelling (`anugerah`, `aktivitas`, `menaati`)
and five example-word glosses (勤倹 "rajin dan hemat", 燎原 "api
menjalar di padang", 捧げ銃 "menghormat dengan senjata", 贈呈, 活躍).

**2026-11-18 per-kanji overlay (r81b):** the r81 majority-rule fixes left
minority users of each head word slightly off (現 "present" showed
"menyerahkan"). The new `k` map fixes this without touching the schema of
`m`: 107 overrides across 99 kanji, each chosen from that kanji's actual
KANJIDIC2 sense — 現本 "saat ini"; 宴 "pesta"; 当是 "benar" and 順
"giliran" for `right`; 便 "surat" for `letter`; 述陳 "menyatakan" for
`state`; 辞 "istilah" for `term`; 柱 "tiang" for `post`; 臣 "bawahan
(raja)" for `subject`; 跳 "melompat" for `spring`; 産 "menghasilkan" for
`yield`; 恋 "merindukan" for `miss`; 苦 "penderitaan" for `trial`; 抑然
interjectional "well"; 穂 "malai (padi)" for `ear`; 対 "seimbang" / 平
"rata" for `even`; 使 "memerintahkan" for `order`; 派 "aliran" for
`school`; 岳廉 `point`; 厚惇懇篤 "baik hati/ramah" for `kind`; 諭
`charge`; 皮 "kulit (binatang)" for `hide`; 乗搭載 "naik (kendaraan)" /
局 "dewan" / 賄 "makan (tunjangan)" for `board`; 堤 "tanggul" for `bank`;
社 "perusahaan" for `firm`; 供呈奉献 "mempersembahkan" for `offer`; 倍
"-lipat" for `fold`; 合添 `suit`; 整調 "menyetel" / 節 "bait (lagu)" for
`tune`; 株 "saham" for `stock`; 息 "jeda" for `rest`; 殖育蓄飼 `raise`;
擁誘鉛 `lead` (鉛 "timah"); 忍担負 "menanggung" for `bear`; 行 "perilaku"
for `conduct`; 町 "blok (kota)" for `block`; 番順 "giliran" for `turn`;
代 "tarif" for `rate`; 計 `plot`; 鉢潤目匹奥懐胸衷 `crown/favor/head/heart`;
削翼葉 `plane`; 権稜 `power`; 揺 "menggoyangkan" for `rock`; 儀治王司宰掌監尺綜
`rule`; 尽 "mengabdi" for `serve`; 域 "tahap" for `stage`; 丁井村街
`town/street`; 表譜 "tabel" / 案 "meja" for `table`; 草識 `write`.

## manifest.json

The N5–N1 study-unit structure: which kanji belong to which unit and in
what order. Selection is KANJIDIC2 (© Electronic Dictionary Research and
Development Group, CC BY-SA 4.0); ordering follows the Jiten global
frequency signal (© Jiten, CC BY-SA 4.0) — build-time signal only, no
frequency values appear in the file. Published under **CC BY-SA 4.0**.

## Third-party MIT notice (JLPT level data)

Included per the MIT licence of JLPT_Vocabulary:

> MIT License
>
> Copyright (c) 2026 Bluskyo
>
> Permission is hereby granted, free of charge, to any person obtaining a
> copy of this software and associated documentation files (the "Software"),
> to deal in the Software without restriction, including without limitation
> the rights to use, copy, modify, merge, publish, distribute, sublicense,
> and/or sell copies of the Software, and to permit persons to whom the
> Software is furnished to do so, subject to the following conditions:
>
> The above copyright notice and this permission notice shall be included in
> all copies or substantial portions of the Software.
>
> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
> IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
> FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL
> THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
> LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
> FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
> DEALINGS IN THE SOFTWARE.

## EDRDG acknowledgement (KANJIDIC2 + JMdict)

This product uses the KANJIDIC2 and JMdict dictionary files. These files are
the property of the Electronic Dictionary Research and Development Group,
and are used in conformance with the Group's licence:
<https://www.edrdg.org/edrdg/licence.html>.
