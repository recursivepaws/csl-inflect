# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**csl-inflect** generates Sanskrit declension (nominal) and conjugation (verbal) tables for all words in the MW1899 dictionary, continuing work from the `MWinflect` repository. The output will improve the [inflected forms display](http://www.sanskrit-lexicon.uni-koeln.de/work/fflexphp/web/index.php) on the Cologne web site.

## Architecture

| Directory/File | Purpose |
|---|---|
| `verbs/` | Verb conjugation generation (pysanskrit-based, multiple versions) |
| `nominals/` | Nominal declension generation |
| `web/` | Web display of inflection tables |
| `sqlite/` | SQLite storage for inflection data |
| `huetdata/` | Huet's SLP1 data used as reference for inflection models |
| `redo.sh` | Full pipeline orchestration; computed files prefixed `calc_` are not tracked |

### Pipeline overview

1. Extract stem-model pairs from MW digitization (`csl-orig`)
2. For each stem+model:
   - `ind` (indeclinable): no inflection needed, just collect
   - Nominal models: generate declension table via pySanskrit
   - Verbal models: generate conjugation table via pySanskrit
3. Store results in SQLite; serve via web display

### pySanskrit versions

`verbs/` contains multiple pySanskrit version directories (`pysanskritv1`, `pysanskritv2`, `pysanskrit_work`) reflecting the iterative development of the Sanskrit morphology library.

## Common Commands

### Full rebuild (from repo root)
```bash
sh redo.sh
```

## Dependencies

- **Python 3** (Python 3.4+)
- **pySanskrit** — Sanskrit morphology library
- **csl-orig** sibling repo — MW dictionary source
