# Saracura PT-BR 4B

[felhen-ai/saracura-ptbr-4b](https://huggingface.co/felhen-ai/saracura-ptbr-4b) (Apache-2.0) is a Kev-recipe decision
model for Brazilian Portuguese: a LoRA adapter and pointer head on `Qwen/Qwen3.5-4B-Base`, initialized from
`jaredpalmer/kev-4b` and fine-tuned on Portuguese typed decisions with Kev's published trainer. It is served by Kev's
System One-compatible server and does not generate text.

| | |
|---|---|
| Decision Index 0.2.1 | **37.91** (Kev 4B on the board: 34.64) |
| Raw index | 53.25 |
| Area skill | knowledge 25.0 · language 41.5 · retrieval 46.2 · tools 53.9 · arts 16.0 |
| Requests | 150,759, all `ok`, none unsupported, no errors |
| Results | [felhen-ai/decision-index-results](https://huggingface.co/datasets/felhen-ai/decision-index-results/tree/4dfa19e0e63a44103310d54afc660ad381f3867d/runs/saracura-ptbr-4b) (compact, no suite text) |

## Running it

```sh
git clone https://github.com/jaredpalmer/kev && cd kev && uv sync --extra serve
uv run --extra serve python -m kev.serve --run felhen-ai/saracura-ptbr-4b --port 8019

python -m decision_index pipeline --engine http \
    --option base_url=http://127.0.0.1:8019 --option model=kev-latest --out runs/saracura-ptbr-4b
```

The run was stored full and compacted afterwards (`payload` and `raw_output` dropped, as `--compact` does);
re-scoring the compact `results.jsonl.gz` gives the same 37.91.

## Training data

Fine-tuning data is Portuguese only: the train splits of the PT-BR typed-decisions benchmark
([felhen-ai/ptbr-typed-decisions-bench](https://huggingface.co/datasets/felhen-ai/ptbr-typed-decisions-bench):
OLID-BR, FACTCK.BR, FaQuAD-NLI, SciELO, JurisTCU, Câmara dos Deputados), the `pt` config of
`telepatia-ai/typed-decisions-pt-es`, internal Brazilian documents and marketplace listings, and synthetic Portuguese
cases labeled by open-weight Qwen models. None of these sources is a suite benchmark. We did not audit what
`telepatia-ai/typed-decisions-pt-es` was built from, and the starting checkpoint `jaredpalmer/kev-4b` carries
whatever its own card lists.
