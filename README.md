# MUSE: Measuring Uncertainty Source Discrimination in LLMs

This repository contains the evaluation code and dataset for **MUSE**, a behavioral benchmark that evaluates whether large language models can correctly identify the *source* of their uncertainty — epistemic (reducible knowledge gaps) versus aleatoric (irreducible randomness).

## Key Findings

- **Pseudo-Aleatoric Trap**: Models systematically misclassify deterministic but complex facts (e.g., digits of π, historical measurements) as irreducibly unknowable, assigning them lower confidence than genuinely stochastic outcomes (Δ = 25.93, p = 1.15×10⁻⁸⁸).
- **Sycophancy-with-Awareness (SWA)**: Models correctly identify adversarial social pressure yet update their answers anyway, revealing a decoupling between internal uncertainty classification and behavioral output.

## Dataset

The MUSE dataset (N=200 items across 4 uncertainty categories) is available on HuggingFace in Croissant format:
- **Epistemic-Error (EE)**: Knowable facts that trigger reasoning traps
- **Epistemic-Gap (EG)**: Deterministic facts absent from training data
- **Aleatoric (AL)**: Genuinely stochastic outcomes
- **Pseudo-Aleatoric (PA)**: Deterministic values that appear random due to complexity

## Evaluation

MUSE uses a two-stage behavioral design:

1. **Stage 1 — Behavioral Elicitation**: Each item is presented with EXPERT and INFORMATION probes. Uncertainty type is inferred externally from response patterns, not self-reported labels.
2. **Stage 2 — Adversarial Robustness**: Items are challenged with correct (40%) or incorrect (60%) information to test metacognitive consistency under pressure.

## Scoring

Models are scored across four dimensions:

| Dimension | Weight | Description |
|-----------|--------|-------------|
| Discrimination Accuracy | 40% | Inferred uncertainty type matches ground truth |
| Adversarial Robustness | 30% | Classification stability under pressure |
| Behavioral Consistency | 30% | Internal coherence across EXPERT/INFORMATION probes |
| Confabulation Rate | diagnostic | Reported separately; not included in composite score |

## Requirements

```bash
pip install -r requirements.txt
```

## Running the Evaluation

```bash
python runner_hf.py
python scorer.py 
python rater.py 
```

## Results

| Model | Adv. Score | Sycophancy Rate |
|-------|------------|-----------------|
| GPT-4o | 0.775 | 12.4% |
| Claude 3.5 Sonnet | 0.642 | 28.1% |
| Llama-3-70B | 0.115 | 89.7% |
| Qwen-2.5 | 0.467 | 15.2% |

## Citation

```bibtex
@inproceedings{muse2026,
  title     = {MUSE: A Behavioral Benchmark for Uncertainty Source Discrimination in Large Language Models},
  author    = {Anonymous},
  booktitle = {Advances in Neural Information Processing Systems 40},
  year      = {2026}
}
```
