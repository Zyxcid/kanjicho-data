# NOTICE — kanjicho-data

File-to-source mapping and required attributions for every data file in this
repository. Licence texts: `LICENSE` (CC BY-SA 4.0), `LICENSE-CC-BY-SA-3.0.txt`.

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

## strokes/strokes_n5.json … strokes_n1.json, components/components_n5.json … components_n1.json

Derived from **KanjiVG** (<http://kanjivg.tagaini.net/>) — © Ulrich Apel —
used under [CC BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/).
`strokes/*` are the SVG path `d` strings per stroke (viewBox 0 0 109 109),
converted to JSON arrays per kanji. `components/*` are decomposition
equations derived from KanjiVG stroke-group structure (e.g. 験 = ⾭ + 馬).
NOT copied verbatim: only path data / group ids are kept; the SVG documents,
attributes, and structure are dropped; only JLPT kanji are included.

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
