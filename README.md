Large Language Models frequently generate hallucinated responses — factually incorrect information presented with high confidence. This project proposes EAAR (Error-Aware Adaptive Re-Reasoning), a novel framework that detects and corrects hallucinations in LLM outputs adaptively without relying on external knowledge sources.
The system works in 4 stages:

Stage 1 — Answer Generation
  Llama-3-8B-Instruct generates initial answer
  to the input question (Pass-1, greedy decoding)

Stage 2 — Dual Signal Hallucination Detection

        Signal 1 : Scratch Transformer classifier
                   predicts Factual or Hallucinated
                   flags if hallucination probability > 0.6

        Signal 2 : Semantic Entropy scorer
                   flags if entropy score > 0.6

Stage 3 — Adaptive Gate
  If either signal flags hallucination
  gate triggers Chain-of-Verification
  If both signals say factual
  Pass-1 answer accepted as final answer

  Key contributions:
  1. Lightweight Scratch Transformer
     built and trained from scratch as hallucination gate
     achieving 65-70% F1 on HaluEval validation set

  2. Dual-signal gating combining classifier prediction
   and semantic entropy for improved detection reliability

  3. Integration of Chain-of-Verification into an adaptive
   gated pipeline triggered only when hallucination detected

  4. Self-contained framework requiring no external
   knowledge base or retrieval system


Results:

Semantic Accuracy          : improved ~15-25% over Pass-1

Hallucination Rate         : reduced after EAAR + CoVe

Consistency Score          : ~0.75-0.90

Prompt Sensitivity         : low (~0.07) indicating robustness
