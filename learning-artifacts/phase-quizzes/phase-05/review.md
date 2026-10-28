# Phase 05 — nlp-foundations-to-advanced Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-25; coverage: **29 lessons**.
- Initial score: **83/87**; final effective score: **83/87 (95.40%)**.
- Cumulative responses: 87, with 83 correct; **4 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- L03: skip-gram predicts context from the center word; CBOW predicts the center word from context.
- L08: backward states in a bidirectional LSTM require future inputs. Strict streaming requires a forward-only model that carries its state.
- L12: TextRank selects sentences by score, then restores source order using their indices. L22: MaxSim takes each query-token row maximum, then sums across query tokens.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Text Processing — Tokenization, Stemming, Lemmatization](../../../phases/05-nlp-foundations-to-advanced/01-text-processing/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Bag of Words, TF-IDF, and Text Representation](../../../phases/05-nlp-foundations-to-advanced/02-bag-of-words-tfidf/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Word Embeddings — Word2Vec from Scratch](../../../phases/05-nlp-foundations-to-advanced/03-word-embeddings-word2vec/docs/en.md) | attempt1: 2/3 | 2/3 |
| [GloVe, FastText, and Subword Embeddings](../../../phases/05-nlp-foundations-to-advanced/04-glove-fasttext-subword/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Sentiment Analysis](../../../phases/05-nlp-foundations-to-advanced/05-sentiment-analysis/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Named Entity Recognition](../../../phases/05-nlp-foundations-to-advanced/06-named-entity-recognition/docs/en.md) | attempt1: 3/3 | 3/3 |
| [POS Tagging and Syntactic Parsing](../../../phases/05-nlp-foundations-to-advanced/07-pos-tagging-parsing/docs/en.md) | attempt1: 3/3 | 3/3 |
| [CNNs and RNNs for Text](../../../phases/05-nlp-foundations-to-advanced/08-cnns-rnns-for-text/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Sequence-to-Sequence Models](../../../phases/05-nlp-foundations-to-advanced/09-sequence-to-sequence/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Attention Mechanism — The Breakthrough](../../../phases/05-nlp-foundations-to-advanced/10-attention-mechanism/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Machine Translation](../../../phases/05-nlp-foundations-to-advanced/11-machine-translation/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Text Summarization](../../../phases/05-nlp-foundations-to-advanced/12-text-summarization/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Question Answering Systems](../../../phases/05-nlp-foundations-to-advanced/13-question-answering/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Information Retrieval and Search](../../../phases/05-nlp-foundations-to-advanced/14-information-retrieval-search/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Topic Modeling — LDA and BERTopic](../../../phases/05-nlp-foundations-to-advanced/15-topic-modeling/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Text Generation Before Transformers — N-gram Language Models](../../../phases/05-nlp-foundations-to-advanced/16-text-generation-pre-transformer/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Chatbots — Rule-Based to Neural to LLM Agents](../../../phases/05-nlp-foundations-to-advanced/17-chatbots-rule-to-neural/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Multilingual NLP](../../../phases/05-nlp-foundations-to-advanced/18-multilingual-nlp/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Subword Tokenization — BPE, WordPiece, Unigram, SentencePiece](../../../phases/05-nlp-foundations-to-advanced/19-subword-tokenization/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Structured Outputs & Constrained Decoding](../../../phases/05-nlp-foundations-to-advanced/20-structured-outputs-constrained-decoding/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Natural Language Inference — Textual Entailment](../../../phases/05-nlp-foundations-to-advanced/21-nli-textual-entailment/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Embedding Models — The 2026 Deep Dive](../../../phases/05-nlp-foundations-to-advanced/22-embedding-models-deep-dive/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Chunking Strategies for RAG](../../../phases/05-nlp-foundations-to-advanced/23-chunking-strategies-rag/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Coreference Resolution](../../../phases/05-nlp-foundations-to-advanced/24-coreference-resolution/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Entity Linking & Disambiguation](../../../phases/05-nlp-foundations-to-advanced/25-entity-linking/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Relation Extraction & Knowledge Graph Construction](../../../phases/05-nlp-foundations-to-advanced/26-relation-extraction-kg/docs/en.md) | attempt1: 3/3 | 3/3 |
| [LLM Evaluation — RAGAS, DeepEval, G-Eval](../../../phases/05-nlp-foundations-to-advanced/27-llm-evaluation-frameworks/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Long-Context Evaluation — NIAH, RULER, LongBench, MRCR](../../../phases/05-nlp-foundations-to-advanced/28-long-context-evaluation/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Dialogue State Tracking](../../../phases/05-nlp-foundations-to-advanced/29-dialogue-state-tracking/docs/en.md) | attempt1: 3/3 | 3/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p05-l03-concept-v1

Which statement correctly distinguishes Word2Vec's skip-gram and CBOW training tasks?

- Learner answer: C — Skip-gram predicts the center word from surrounding words; CBOW predicts surrounding words from the center.
- Correct answer: A — Skip-gram predicts surrounding words from a center word; CBOW predicts the center word from surrounding words.
- Explanation: Skip-gram uses a center word to predict context words. CBOW uses the surrounding context to predict the center word. Option C reverses their training directions.

### p05-l08-application-v1

You need an RNN-based text classifier that updates as each token arrives, without seeing future tokens. Which setup respects that streaming constraint?

- Learner answer: A — Use a bidirectional LSTM and assume its backward states are available before later tokens arrive.
- Correct answer: D — Use a forward-only LSTM or GRU and carry its recurrent state between incoming tokens.
- Explanation: A bidirectional LSTM's backward state depends on later tokens, so it is unavailable under the stated strict no-future-token streaming constraint. A forward-only LSTM or GRU can update its recurrent state using only the observed prefix.

### p05-l12-code-v1

After sentence scoring, the lesson selects the top2 sentences and then restores source order. What does this code print?

```python
sentences = ['Opening.', 'Evidence.', 'Conclusion.']
scores = [0.2, 0.8, 0.9]
ranked = sorted(range(len(sentences)),
                key=lambda i: scores[i], reverse=True)[:2]
ranked.sort()
print([sentences[i] for i in ranked])
```

- Learner answer: A — ['Conclusion.', 'Evidence.']
- Correct answer: C — ['Evidence.', 'Conclusion.']
- Explanation: Ranking by score first selects indices[2,1], but ranked.sort() then restores ascending source indices[1,2]. The returned sentences are ['Evidence.','Conclusion.'], not descending score order.

### p05-l22-code-v1

Rows of sim correspond to query tokens; columns correspond to document tokens. The lesson's MaxSim sums each query token's best document-token similarity. What does the code print?

```python
sim = [[0.2, 0.9, 0.1],
       [0.8, 0.3, 0.4]]
score = sum(max(row) for row in sim)
print(round(score, 2))
```

- Learner answer: B — 1.5
- Correct answer: D — 1.7
- Explanation: MaxSim takes the maximum in each query-token row:0.9 and0.8. Their sum is1.7. It does not maximize over columns, whose maxima would sum to2.1.
