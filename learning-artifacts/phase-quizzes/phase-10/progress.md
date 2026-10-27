# Phase 10 — llms-from-scratch

Status: **done**. Lessons: 24. Scored responses: 78.

Score: initial 59/72 (81.94%); effective 63/72 (87.50%); cumulative 65/78. Passed on 2026-10-27. Lessons03 and12 retakes: 3/3 each. All 24 lesson minima met.

[All phases](../progress.md) · [Detailed attempts](history.md) · [Review notes](review.md)

## Lesson checklist

| Lesson | Title | Status | Initial score | Latest score | Completion basis |
|---|---|---|---|---|---|
| 10-llms-from-scratch/01-tokenizers | Tokenizers: BPE, WordPiece, SentencePiece | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/02-building-a-tokenizer | Building a Tokenizer from Scratch | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/03-data-pipelines | Data Pipelines for Pre-Training | done | 1/3 | 3/3 (attempt2) | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/04-pre-training-mini-gpt | Pre-Training a Mini GPT (124M Parameters) | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/05-scaling-distributed | Scaling: Distributed Training, FSDP, DeepSpeed | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/06-instruction-tuning-sft | Instruction Tuning (SFT) | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/07-rlhf | RLHF: Reward Model + PPO | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/08-dpo | DPO: Direct Preference Optimization | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/09-constitutional-ai-self-improvement | Constitutional AI and Self-Improvement | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/10-evaluation | Evaluation: Benchmarks, Evals, LM Harness | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/11-quantization | Quantization: Making Models Fit | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/12-inference-optimization | Inference Optimization | done | 1/3 | 3/3 (attempt2) | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/13-building-complete-llm-pipeline | Building a Complete LLM Pipeline | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/14-open-models-architecture-walkthroughs | Open Models: Architecture Walkthroughs | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/15-speculative-decoding-eagle3 | Speculative Decoding and EAGLE-3 | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/16-differential-attention-v2 | Differential Attention (V2) | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/17-native-sparse-attention | Native Sparse Attention (DeepSeek NSA) | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/18-multi-token-prediction | Multi-Token Prediction (MTP) | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/19-dualpipe-parallelism | DualPipe Parallelism | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/20-deepseek-v3-walkthrough | DeepSeek-V3 Architecture Walkthrough | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/21-jamba-hybrid-ssm-transformer | Jamba — Hybrid SSM-Transformer | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/22-async-hogwild-inference | Async and Hogwild! Inference | done | 2/3 | 2/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/25-speculative-decoding | Speculative Decoding and EAGLE | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |
| 10-llms-from-scratch/34-gradient-checkpointing | Gradient Checkpointing and Activation Recomputation | done | 3/3 | 3/3 | quiz-based mastery; implementation lab not performed in this assessment |

## Progress log

| Date | Lesson | Quiz | Note |
|---|---|---|---|

| 2026-10-27 | 10-llms-from-scratch/01-tokenizers | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/02-building-a-tokenizer | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/03-data-pipelines | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial 1/3; fresh retake 3/3. Earlier misses preserved in review notes. |
| 2026-10-27 | 10-llms-from-scratch/04-pre-training-mini-gpt | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/05-scaling-distributed | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/06-instruction-tuning-sft | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/07-rlhf | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/08-dpo | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/09-constitutional-ai-self-improvement | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/10-evaluation | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/11-quantization | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/12-inference-optimization | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial 1/3; fresh retake 3/3. Earlier misses preserved in review notes. |
| 2026-10-27 | 10-llms-from-scratch/13-building-complete-llm-pipeline | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/14-open-models-architecture-walkthroughs | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/15-speculative-decoding-eagle3 | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/16-differential-attention-v2 | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/17-native-sparse-attention | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/18-multi-token-prediction | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/19-dualpipe-parallelism | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/20-deepseek-v3-walkthrough | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/21-jamba-hybrid-ssm-transformer | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/22-async-hogwild-inference | 2/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. Initial set 2/3; missed topic retained in review notes. |
| 2026-10-27 | 10-llms-from-scratch/25-speculative-decoding | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
| 2026-10-27 | 10-llms-from-scratch/34-gradient-checkpointing | 3/3 | Quiz-based mastery credit; implementation lab not performed in this assessment. |
