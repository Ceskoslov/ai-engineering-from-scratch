# Phase 12 review queue

Historical notes are preserved verbatim; some early remediation requests were superseded by later passes. Latest completion status is in [phase progress](progress.md).

- Lesson01, attempt1: 1/3. Review shared patch projection versus position information, and counting CLS plus register tokens in the full sequence. Fresh three-question remediation required; code divisibility question correct.

- Lesson02, attempt1: 2/3. Correct class selection must use maximum cosine similarity; normalized dog score 1 exceeds cat score about 0.707. Lesson minimum met.

- Lesson03, attempt1: 2/3. Review attention shape (query count × patch count) and projection preserving token count while changing width: 8×64 weights, 8×24 outputs. Lesson minimum met.

- Lesson04, attempt1: 2/3. Review most-recent-preceding-image masking: intro sees none; a sees IMG0; b sees IMG1. Lesson minimum met.

- Lesson05, attempt1: 2/3. Distinguish prompt metadata from implemented embedding insertion: build_llava_prompt retains <image> in raw_prompt and records image_tokens separately. Lesson minimum met.

- Lesson07, attempt1: 2/3. Recipe picker filters only llm_b; eligibility does not establish total parameter, VRAM, or latency budget compliance. Lesson minimum met.

- Lesson10, attempt1: 2/3. Independent int(total*fraction) truncation can leave steps unallocated; fractions summing to one do not guarantee integer counts sum to total. Lesson minimum met.

- Lesson12, attempt1: 2/3. Autoregressive image generation predicts discrete visual codes, then a visual decoder renders pixels; it does not predict continuous pixels from a text-only vocabulary. Lesson minimum met.

- Lesson16, attempt1: 1/3. Review disjoint modality ID ranges preventing code collisions and exclusive end offsets: start=32000,size=4096 covers IDs32000–36095; next start36096. Fresh three-question remediation required. Streaming question correct.

- Lesson17, attempt1: 2/3. Temporal grounding localizes when an event occurs using timestamps or intervals, beyond recognizing its presence. Lesson minimum met.

- Lesson24, attempt1: 2/3. The variable confidence is a fused retrieval score, not a calibrated probability or verified answer correctness. Lesson minimum met.

- Lesson01 remediation attempt2:3/3. Shared projection versus positional signal, full sequence count, and projection parameter count answered correctly. Initial evidence preserved; lesson minimum now met.

- Lesson16 remediation attempt2:2/3 replaces1/3; lesson minimum met. Residual review: exclusive end=start+size, last valid ID=end−1. For100 entries starting200, last299 and next300.

Phase12 passed2026-10-28: effective65/75 (86.67%). Earlier missed-topic notes remain useful for later review; no further remediation required for this phase.
