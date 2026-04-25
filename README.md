# SBS-LLM Experiment

This repository contains a small, reproducible audit pipeline for paired SBS/AHT and forensic vignettes.

As of April 24, 2026, the OpenAI portion of the project is configured for the Responses API and `gpt-5.5`, using Structured Outputs with a strict JSON Schema instead of relying only on prompt wording for JSON formatting.

## Main workflow

Render the analysis documents from the repository root:

```bash
quarto render analysis/run_experiment.qmd
quarto render analysis/parse_results.qmd
quarto render analysis/analyze_results.qmd
quarto render analysis/LLM-experiment.qmd
```

## OpenAI migration notes

- The OpenAI wrapper now calls `POST /v1/responses` rather than Chat Completions.
- The default model is `gpt-5.5`, read from `OPENAI_MODEL`.
- Output structure is enforced with Structured Outputs via `text.format = json_schema`.
- The request is explicitly stateless with `store = FALSE`.
- The wrapper sets `reasoning.effort = "low"` and `text.verbosity = "low"` as a sensible starting point for this audit design.
- Raw text output and the full raw API response are both saved to the raw results file.

## Repository structure

- `analysis/`: Quarto documents for running, parsing, and analyzing the audit
- `results/`: raw and parsed CSV outputs created by the pipeline
- `figures/`: generated plots
- `paper/`: manuscript source and bibliography
- `Data/`: other source data
- `Literature/`: reference papers and notes
