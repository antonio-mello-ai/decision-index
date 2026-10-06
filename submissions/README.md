# Model submissions

| Model | Edition | Decision Index | Complete results | Engine / commit | Hardware | Declared limits |
|---|---|---:|---|---|---|---|
| [Saracura PT-BR 4B](https://huggingface.co/felhen-ai/saracura-ptbr-4b) | 0.2.1 | 37.91 | [scores.json](https://huggingface.co/datasets/felhen-ai/decision-index-results/blob/4dfa19e0e63a44103310d54afc660ad381f3867d/runs/saracura-ptbr-4b/scores.json) | `http` → `kev.serve` ([jaredpalmer/kev](https://github.com/jaredpalmer/kev)); runner/scorer `87d4650` | 1× NVIDIA RTX 5090 32 GB, bf16, one request at a time | `SERVE_MAX_STATE=65536` (Kev default); no truncation, 0 unsupported |
