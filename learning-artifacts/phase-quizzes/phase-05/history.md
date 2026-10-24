# Phase 05 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

### Phase05 assessment started — 2026-10-24

English questions; three scored questions per lesson across29 lessons,87 total. Pass requires at least74/87 overall and at least2/3 per lesson. All lessons remain todo until the full phase passes. Phases00–04 remain done. Full Lesson01 docs read before its questions.

### Answer history: p05-l01-concept-v1

ID: p05-l01-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson01 — Text Processing — Tokenization, Stemming, Lemmatization.
Question1/87; lesson question1/3; conceptual.

Which statement correctly distinguishes stemming from lemmatization?

A) Stemming always produces dictionary words; lemmatization only splits text at punctuation.
B) Both methods must return identical outputs because grammatical context never matters.
C) Stemming strips affixes with rules and may produce nonwords; lemmatization uses linguistic knowledge and often part-of-speech context to recover dictionary forms.
D) Lemmatization assigns integer token IDs; stemming learns contextual embeddings from a neural network.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Stemming applies affix-stripping rules and may yield a nonword such as poni. Lemmatization uses linguistic knowledge and often grammatical context to recover dictionary forms, including irregular mappings such as ran to run.
Phase05 running initial score:1/1. Lesson01 attempt1:1/1; incomplete.

### Answer history: p05-l01-application-v1

ID: p05-l01-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson01 — Text Processing — Tokenization, Stemming, Lemmatization.
Question2/87; lesson question2/3; application.

A classical text classifier was trained with lowercasing, tokenization, and stemming. Its deployed service feeds raw user text into feature extraction, and accuracy drops. Which fix best addresses the mismatch?

A) Package the training preprocessing function with the model and apply the same versioned transformation at inference.
B) Remove preprocessing from inference and increase the classifier's confidence threshold.
C) Add lemmatization only at inference while keeping the stemmed training features unchanged.
D) Randomly choose a tokenizer per request so all possible tokenizations eventually appear.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Training and inference need the same preprocessing transformation so extracted features have consistent meanings. Shipping a shared versioned preprocessing function avoids a separately rewritten serving pipeline drifting from training behavior.
Phase05 running initial score:2/2. Lesson01 attempt1:2/2; incomplete.

### Answer history: p05-l01-code-v1

ID: p05-l01-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson01 — Text Processing — Tokenization, Stemming, Lemmatization.
Question3/87; lesson question3/3; code tracing.

What does this deliberately limited suffix-stripping function print? Apply only the rules shown, not the full Porter algorithm.

```python
def stem_step_1a(word):
    if word.endswith('sses'):
        return word[:-2]
    if word.endswith('ies'):
        return word[:-2]
    if word.endswith('ss'):
        return word
    if word.endswith('s') and len(word) > 1:
        return word[:-1]
    return word

print([stem_step_1a(w) for w in ['caresses', 'ponies', 'caress', 'cats']])
```

A) ['caress', 'pony', 'caress', 'cat']
B) ['caresse', 'ponie', 'cares', 'cat']
C) ['caress', 'poni', 'cares', 'cats']
D) ['caress', 'poni', 'caress', 'cat']

Learner answer: D. Correct answer: D. Result: correct.
Explanation: The first matching rule wins. caresses loses es, ponies loses es to become poni, caress is preserved by the ss rule, and cats loses its final s. This limited function does not perform dictionary-form recovery.
Phase05 running initial score:3/3. Lesson01 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson02 docs read before its questions.

### Answer history: p05-l02-concept-v1

ID: p05-l02-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson02 — Bag of Words, TF-IDF, and Text Representation.
Question4/87; lesson question1/3; conceptual.

Two terms occur equally often in one document, but one appears in nearly every document in the corpus while the other is rare across documents. What does IDF weighting do, all else equal?

A) Give the widespread term more weight because its document frequency is larger.
B) Give the rare term more weight because it is more discriminative across documents.
C) Give both terms identical weights because IDF depends only on counts within the current document.
D) Remove both terms because TF-IDF cannot represent repeated words.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: IDF decreases with document frequency, so a term appearing in fewer documents receives greater inverse-document-frequency weight. With equal term frequency, its TF-IDF weight is therefore larger.
Phase05 running initial score:4/4. Lesson02 attempt1:1/1; incomplete.

### Answer history: p05-l02-application-v1

ID: p05-l02-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson02 — Bag of Words, TF-IDF, and Text Representation.
Question5/87; lesson question2/3; application.

Your unigram TF-IDF sentiment classifier struggles with phrases such as "not good". Which feature change most directly preserves this local negation signal?

A) Remove "not" as a stopword so only sentiment adjectives remain.
B) Sort every document's tokens alphabetically before creating features.
C) Replace every document vector with its total number of tokens.
D) Keep negation words and include adjacent word bigrams alongside unigrams.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Keeping negation words preserves their information, and adjacent bigrams create features such as not good. Removing negation or discarding token adjacency loses this local signal. Bigrams improve local order sensitivity without giving full syntactic understanding.
Phase05 running initial score:5/5. Lesson02 attempt1:2/2; incomplete.

### Answer history: p05-l02-code-v1

ID: p05-l02-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson02 — Bag of Words, TF-IDF, and Text Representation.
Question6/87; lesson question3/3; code tracing.

Using the lesson's smoothed IDF and length-normalized TF, what does this code print? No final L2 normalization is applied. log is the natural logarithm.

```python
import math
# Vocabulary order: cat, dog. Corpus: [cat, cat], [cat, dog].
bow = [[2, 0], [1, 1]]
df = [sum(row[j] > 0 for row in bow) for j in range(2)]
idf = [math.log((len(bow) + 1) / (d + 1)) + 1 for d in df]
row = bow[1]
weights = [(count / sum(row)) * value for count, value in zip(row, idf)]
print([round(x, 3) for x in weights])
```

A) [0.5, 0.5]
B) [1.0, 1.405]
C) [0.5, 0.703]
D) [0.0, 0.347]

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Document frequencies are[2,1]. Smoothed IDF values are1 and1+log(3/2), approximately1.405. Both document term frequencies are0.5, yielding[0.5,0.703] after rounding, without L2 normalization.
Phase05 running initial score:6/6. Lesson02 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson03 docs read before its questions.

### Answer history: p05-l03-concept-v1

ID: p05-l03-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson03 — Word Embeddings — Word2Vec from Scratch.
Question7/87; lesson question1/3; conceptual.

Which statement correctly distinguishes Word2Vec's skip-gram and CBOW training tasks?

A) Skip-gram predicts surrounding words from a center word; CBOW predicts the center word from surrounding words.
B) Skip-gram predicts document labels; CBOW reconstructs the original character sequence.
C) Skip-gram predicts the center word from surrounding words; CBOW predicts surrounding words from the center.
D) Both predict only the next word, using a different vector for each occurrence of a word.

Learner answer: C. Correct answer: A. Result: incorrect.
Explanation: Skip-gram uses a center word to predict context words. CBOW uses the surrounding context to predict the center word. Option C reverses their training directions.
Phase05 running initial score:6/7. Lesson03 attempt1:0/1; incomplete. Skip-gram versus CBOW direction added to the review queue.

### Answer history: p05-l03-application-v1

ID: p05-l03-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson03 — Word Embeddings — Word2Vec from Scratch.
Question8/87; lesson question2/3; application.

A skip-gram model has a vocabulary of100,000 words, making a full output softmax expensive for each training pair. What does negative sampling change?

A) It replaces all observed center-context pairs with random pairs and removes positive examples.
B) It computes the full vocabulary softmax but stores only its largest probability.
C) It freezes both embedding tables and learns only a lookup dictionary of word counts.
D) It trains binary positive-versus-sampled-negative pair objectives instead of normalizing over the entire vocabulary.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Negative sampling trains a logistic objective on observed positive center-context pairs and a small number of sampled negative pairs, avoiding a full-vocabulary softmax normalization for each pair. Both embedding tables receive updates.
Phase05 running initial score:7/8. Lesson03 attempt1:1/2; incomplete.

### Answer history: p05-l03-code-v1

ID: p05-l03-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson03 — Word Embeddings — Word2Vec from Scratch.
Question9/87; lesson question3/3; code tracing.

What ordered list of (center, context) pairs does this code produce with a window of1? It excludes the center token itself.

```python
doc = ['red', 'cat', 'sat']
window = 1
pairs = []
for i, center in enumerate(doc):
    for j in range(max(0, i-window), min(len(doc), i+window+1)):
        if i != j:
            pairs.append((center, doc[j]))
print(pairs)
```

A) [('red', 'cat'), ('cat', 'sat')]
B) [('red', 'cat'), ('cat', 'red'), ('cat', 'sat'), ('sat', 'cat')]
C) [('red', 'red'), ('cat', 'cat'), ('sat', 'sat')]
D) [('red', 'cat'), ('red', 'sat'), ('cat', 'red'), ('cat', 'sat'), ('sat', 'red'), ('sat', 'cat')]

Learner answer: B. Correct answer: B. Result: correct.
Explanation: A radius1 window pairs each center with its immediate left and right neighbors where present. The endpoints have one context each; cat has two, giving four ordered pairs and no self-pairs.
Phase05 running initial score:8/9. Lesson03 attempt1 complete:2/3, meeting the lesson minimum. Skip-gram versus CBOW direction remains in the review queue. Lessons remain todo until the full phase passes. Full Lesson04 docs read before its questions.

### Answer history: p05-l04-concept-v1

ID: p05-l04-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson04 — GloVe, FastText, and Subword Embeddings.
Question10/87; lesson question1/3; conceptual.

Which description correctly matches GloVe, fastText, and BPE to their core mechanisms?

A) GloVe reconstructs image patches; fastText assigns document labels only; BPE strips grammatical suffixes.
B) GloVe merges adjacent characters; fastText fits log co-occurrence counts; BPE predicts dictionary lemmas.
C) GloVe fits word vectors to log co-occurrence statistics; fastText composes word vectors from character n-grams; BPE learns tokens through frequent adjacent-pair merges.
D) GloVe needs no corpus statistics; fastText stores only whole-word vectors; BPE creates one token per sentence.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: GloVe learns from weighted log co-occurrence statistics, fastText represents words through character n-gram components, and BPE learns subword units by iteratively merging frequent adjacent token pairs.
Phase05 running initial score:9/10. Lesson04 attempt1:1/1; incomplete.

### Answer history: p05-l04-application-v1

ID: p05-l04-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson04 — GloVe, FastText, and Subword Embeddings.
Question11/87; lesson question2/3; application.

Your word-vector pipeline encounters an unseen inflected word that shares character n-grams with known words. Why can a subword-aware fastText model still produce a vector where a whole-word lookup table cannot?

A) It can compose a vector from learned character n-gram components even without a stored whole-word entry.
B) It automatically retrieves the word's dictionary definition and encodes it with a language model.
C) It guarantees that every new word has the same meaning as its nearest known spelling.
D) It requires the entire original corpus to be retrained before answering each unseen-word query.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: A subword-aware fastText model can compose an unseen word's vector from learned character n-gram components. This provides coverage beyond stored whole-word entries, but does not guarantee a semantically accurate vector for every new word.
Phase05 running initial score:10/11. Lesson04 attempt1:2/2; incomplete.

### Answer history: p05-l04-code-v1

ID: p05-l04-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson04 — GloVe, FastText, and Subword Embeddings.
Question12/87; lesson question3/3; code tracing.

The following code applies learned BPE merges in their listed order. What does it print? The marker </w> is an end-of-word token.

```python
tokens = ['l', 'o', 'w', 'e', 'r', '</w>']
merges = [('l', 'o'), ('lo', 'w'), ('e', 'r')]
for a, b in merges:
    out = []
    i = 0
    while i < len(tokens):
        if i + 1 < len(tokens) and (tokens[i], tokens[i+1]) == (a, b):
            out.append(a + b)
            i += 2
        else:
            out.append(tokens[i])
            i += 1
    tokens = out
print(tokens)
```

A) ['lower</w>']
B) ['lo', 'w', 'er', '</w>']
C) ['low', 'e', 'r</w>']
D) ['low', 'er', '</w>']

Learner answer: D. Correct answer: D. Result: correct.
Explanation: The merges first form lo, then low, then er. No listed rule merges low with er or er with the end marker, so the final tokens are ['low','er','</w>'].
Phase05 running initial score:11/12. Lesson04 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson05 docs read before its questions.

### Answer history: p05-l05-concept-v1

ID: p05-l05-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson05 — Sentiment Analysis.
Question13/87; lesson question1/3; conceptual.

Why does the lesson add Laplace smoothing when estimating word probabilities for multinomial Naive Bayes?

A) To force positive and negative classes to have identical word distributions.
B) To prevent a vocabulary word unseen in one class from having zero probability in that class.
C) To remove the need for class priors or labelled training documents.
D) To make the classifier model every word-order dependency exactly.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: Laplace smoothing adds a pseudocount to each vocabulary word in each class, preventing zero class-conditional probabilities for words not observed in that class. It does not remove the conditional-independence assumption or the need for class priors.
Phase05 running initial score:12/13. Lesson05 attempt1:1/1; incomplete.

### Answer history: p05-l05-application-v1

ID: p05-l05-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson05 — Sentiment Analysis.
Question14/87; lesson question2/3; application.

A sentiment test set is90% positive. Your model predicts positive for every example and achieves90% accuracy. Which evaluation best exposes its failure on negative reviews?

A) Report only accuracy because90% exceeds the random-guess baseline.
B) Report only micro-F1, which gives equal weight to each class regardless of frequency.
C) Remove negative examples from evaluation because they are uncommon.
D) Inspect per-class precision and recall, macro-F1, and the confusion matrix.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: An always-positive model has zero recall for negative reviews despite90% accuracy. Per-class metrics and the confusion matrix expose this, while macro-F1 gives each class equal weight instead of allowing the majority to dominate.
Phase05 running initial score:13/14. Lesson05 attempt1:2/2; incomplete.

### Answer history: p05-l05-code-v1

ID: p05-l05-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson05 — Sentiment Analysis.
Question15/87; lesson question3/3; code tracing.

What does this simplified negation-scoping function print? Follow only the shown rules; punctuation ends the scope.

```python
tokens = ['not', 'great', ',', 'but', 'funny']
out = []
negate = False
for token in tokens:
    if token in {'.', '!', '?', ',', ';'}:
        negate = False
        out.append(token)
        continue
    if token in {'not', 'no', 'never'}:
        negate = True
        out.append(token)
        continue
    out.append('NOT_' + token if negate else token)
print(out)
```

A) ['NOT_not', 'NOT_great', ',', 'but', 'funny']
B) ['not', 'NOT_great', ',', 'but', 'funny']
C) ['not', 'NOT_great', ',', 'NOT_but', 'NOT_funny']
D) ['not', 'great', ',', 'but', 'funny']

Learner answer: B. Correct answer: B. Result: correct.
Explanation: not is appended unchanged and starts the scope, great becomes NOT_great, and the comma resets the scope before but and funny. The output is ['not','NOT_great',',','but','funny'].
Phase05 running initial score:14/15. Lesson05 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson06 docs read before its questions.

### Answer history: p05-l06-concept-v1

ID: p05-l06-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson06 — Named Entity Recognition.
Question16/87; lesson question1/3; conceptual.

In standard BIO tagging, how should the single entity "New York City" be labelled as GPE, followed by the non-entity token "today"?

A) New:I-GPE, York:I-GPE, City:I-GPE, today:O.
B) New:B-GPE, York:B-GPE, City:B-GPE, today:O.
C) New:B-GPE, York:I-GPE, City:I-GPE, today:O.
D) New:O, York:B-GPE, City:I-GPE, today:I-GPE.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: B-GPE begins the entity at New, I-GPE continues it through York and City, and O marks today as outside the entity. Repeating B-GPE would instead indicate separate entities.
Phase05 running initial score:15/16. Lesson06 attempt1:1/1; incomplete.

### Answer history: p05-l06-application-v1

ID: p05-l06-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson06 — Named Entity Recognition.
Question17/87; lesson question2/3; application.

Your annotation schema requires both "Bank of America" as ORG and the containing phrase "Bank of America Tower" as FACILITY in the same sentence. Which approach can represent both overlapping spans?

A) Use a single BIO label per token and alternate ORG and FACILITY labels inside the phrase.
B) Use a nested/span-based model or separate tagging passes that preserve both sets of boundaries.
C) Increase a flat BIO model's hidden size while keeping exactly one label per token.
D) Keep only the longest span and report that both annotations were recovered.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: A single flat BIO layer assigns only one label to each token and cannot represent both nested entities simultaneously. Span-based/nested models or separate passes can preserve the overlapping ORG and FACILITY spans.
Phase05 running initial score:16/17. Lesson06 attempt1:2/2; incomplete.

### Answer history: p05-l06-code-v1

ID: p05-l06-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson06 — Named Entity Recognition.
Question18/87; lesson question3/3; code tracing.

What span list does this code print? Indices are zero-based, with an exclusive end index. Each B- tag begins a new entity even if its type matches the previous entity.

```python
labels = ['B-ORG', 'I-ORG', 'B-ORG', 'O']
spans = []
current = None
for i, label in enumerate(labels):
    if label.startswith('B-'):
        if current:
            spans.append(current)
        current = (i, i + 1, label[2:])
    elif label.startswith('I-') and current and current[2] == label[2:]:
        current = (current[0], i + 1, current[2])
    else:
        if current:
            spans.append(current)
            current = None
if current:
    spans.append(current)
print(spans)
```

A) [(0, 3, 'ORG')]
B) [(0, 1, 'ORG'), (2, 2, 'ORG')]
C) [(0, 2, 'ORG'), (2, 4, 'ORG')]
D) [(0, 2, 'ORG'), (2, 3, 'ORG')]

Learner answer: D. Correct answer: D. Result: correct.
Explanation: B-ORG at index0 and I-ORG at1 form span(0,2). The B-ORG at2 closes that span and starts a separate entity(2,3), which is closed by O at3.
Phase05 running initial score:17/18. Lesson06 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson07 docs read before its questions.

### Answer history: p05-l07-concept-v1

ID: p05-l07-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson07 — POS Tagging and Syntactic Parsing.
Question19/87; lesson question1/3; conceptual.

Which statement correctly distinguishes POS tagging from dependency parsing?

A) POS tagging groups entire documents by topic; dependency parsing assigns sentiment labels.
B) POS tagging identifies named-entity spans; dependency parsing maps words to dictionary lemmas.
C) POS tagging returns a sentence's translation; dependency parsing learns a subword vocabulary.
D) POS tagging assigns grammatical categories to tokens; dependency parsing identifies head-dependent relations between tokens.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: POS tags assign grammatical categories such as NOUN or VERB to tokens. Dependency parsing adds structure by identifying which words depend on which heads and labelling those relations, such as subject or modifier.
Phase05 running initial score:18/19. Lesson07 attempt1:1/1; incomplete.

### Answer history: p05-l07-application-v1

ID: p05-l07-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson07 — POS Tagging and Syntactic Parsing.
Question20/87; lesson question2/3; application.

Your bigram HMM POS tagger must choose the highest-scoring tag sequence for an entire sentence using transition and emission probabilities. Which decoding approach matches this objective?

A) Pick each word's most frequent tag independently and ignore transitions.
B) Pick the most likely first tag and greedily commit to each next tag without reconsidering earlier choices.
C) Use Viterbi dynamic programming to retain the best prefix ending in each tag, then backtrack the best complete path.
D) Sort all tokens alphabetically and assign tags based only on their new positions.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Viterbi retains the best-scoring prefix ending in each possible current tag. It combines prefix, transition and emission scores and stores backpointers, allowing recovery of the best full path rather than making irreversible greedy choices.
Phase05 running initial score:19/20. Lesson07 attempt1:2/2; incomplete.

### Answer history: p05-l07-code-v1

ID: p05-l07-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson07 — POS Tagging and Syntactic Parsing.
Question21/87; lesson question3/3; code tracing.

This is one Viterbi update for the current tag VERB. All values are log scores, so a larger (less negative) score is better. What does it print?

```python
previous = {'NOUN': -1.0, 'VERB': -0.5}
transition_to_verb = {'NOUN': -0.1, 'VERB': -2.0}
emission = -0.2
candidates = {
    tag: score + transition_to_verb[tag] + emission
    for tag, score in previous.items()
}
best_prev = max(candidates, key=candidates.get)
print(best_prev, round(candidates[best_prev], 1))
```

A) NOUN -1.3
B) VERB -2.7
C) VERB -0.7
D) NOUN -0.3

Learner answer: A. Correct answer: A. Result: correct.
Explanation: The NOUN prefix gives -1.0-0.1-0.2=-1.3, while the VERB prefix gives -0.5-2.0-0.2=-2.7. The larger score is -1.3, so the predecessor selected for the current VERB state is NOUN.
Phase05 running initial score:20/21. Lesson07 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson08 docs read before its questions.

### Answer history: p05-l08-concept-v1

ID: p05-l08-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson08 — CNNs and RNNs for Text.
Question22/87; lesson question1/3; conceptual.

In a TextCNN, what does a width3 convolution over token embeddings followed by global max pooling primarily do?

A) Average all word embeddings before inspecting any local token order.
B) Learn local three-token pattern detectors and retain each filter's strongest activation across positions.
C) Maintain a recurrent hidden state that updates once per token.
D) Compute unrestricted self-attention between every pair of tokens.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: A width3 filter spans three consecutive token embeddings and learns local ordered patterns. Global max pooling keeps each filter's strongest response over the sequence, giving a fixed-size representation while discarding the exact winning position.
Phase05 running initial score:21/22. Lesson08 attempt1:1/1; incomplete.

### Answer history: p05-l08-application-v1

ID: p05-l08-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson08 — CNNs and RNNs for Text.
Question23/87; lesson question2/3; application.

You need an RNN-based text classifier that updates as each token arrives, without seeing future tokens. Which setup respects that streaming constraint?

A) Use a bidirectional LSTM and assume its backward states are available before later tokens arrive.
B) Reverse the complete sequence before processing it, while requiring immediate outputs for its first token.
C) Wait for the full document and use right-context features while calling the output strictly online.
D) Use a forward-only LSTM or GRU and carry its recurrent state between incoming tokens.

Learner answer: A. Correct answer: D. Result: incorrect.
Explanation: A bidirectional LSTM's backward state depends on later tokens, so it is unavailable under the stated strict no-future-token streaming constraint. A forward-only LSTM or GRU can update its recurrent state using only the observed prefix.
Phase05 running initial score:21/23. Lesson08 attempt1:1/2; incomplete. Bidirectional future-context dependency added to the review queue.

### Answer history: p05-l08-code-v1

ID: p05-l08-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson08 — CNNs and RNNs for Text.
Question24/87; lesson question3/3; code tracing.

What shape does this TextCNN feature-extraction code print? Both convolutions use stride1 and no padding.

```python
import torch
from torch import nn
x = torch.zeros(2, 6, 8)  # batch, tokens, embedding dimensions
x = x.transpose(1, 2)
convs = [nn.Conv1d(8, 4, kernel_size=k) for k in (2, 3)]
pooled = [conv(x).max(dim=2).values for conv in convs]
h = torch.cat(pooled, dim=1)
print(tuple(h.shape))
```

A) (2, 6, 8)
B) (2, 4)
C) (2, 8)
D) (2, 9)

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Transpose gives shape(2,8,6). The width2 and width3 convolutions produce(2,4,5) and(2,4,4). Max pooling over sequence length makes each(2,4); concatenating along features yields(2,8).
Phase05 running initial score:22/24. Lesson08 attempt1 complete:2/3, meeting the lesson minimum. Bidirectional future-context dependency remains in the review queue. Lessons remain todo until the full phase passes. Full Lesson09 docs read before its questions.

### Answer history: p05-l09-concept-v1

ID: p05-l09-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson09 — Sequence-to-Sequence Models.
Question25/87; lesson question1/3; conceptual.

In a basic RNN encoder-decoder without attention, why can translation quality degrade as source sentences get longer?

A) The decoder must output exactly as many tokens as the encoder receives.
B) The encoder assigns one separate hidden-state dimension to every vocabulary word.
C) All source information available to the decoder is compressed into a fixed-size final encoder state, which can lose detail.
D) Teacher forcing makes the encoder ignore every source token except punctuation.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: In the basic no-attention encoder-decoder, the decoder receives source information through a fixed-size final encoder state. Longer inputs make retaining all useful details harder; attention provides direct access to encoder states across source positions.
Phase05 running initial score:23/25. Lesson09 attempt1:1/1; incomplete.

### Answer history: p05-l09-application-v1

ID: p05-l09-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson09 — Sequence-to-Sequence Models.
Question26/87; lesson question2/3; application.

A decoder trains using the correct previous target token at every step, but at inference it must consume its own predictions. Errors then compound over long outputs. Which explanation and training adjustment match the lesson?

A) This is exposure bias; scheduled sampling sometimes feeds model predictions during training instead of always using ground-truth previous tokens.
B) This is a vocabulary-size error; use the ground-truth test targets as decoder inputs at inference.
C) This proves attention weights are missing; increasing teacher forcing guarantees error-free inference.
D) This is label smoothing; remove the source sentence and train only the decoder's class priors.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Exposure bias is the mismatch between training on ground-truth prefixes and generating from model-produced prefixes. Scheduled sampling exposes the decoder to some of its own predicted previous tokens during training; it is a proposed mitigation, not a guarantee of error-free generation.
Phase05 running initial score:24/26. Lesson09 attempt1:2/2; incomplete.

### Answer history: p05-l09-code-v1

ID: p05-l09-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson09 — Sequence-to-Sequence Models.
Question27/87; lesson question3/3; code tracing.

What list of tokens actually fed into the decoder does this training-loop trace print? Model predictions are supplied explicitly for this exercise.

```python
target = ['je', 'cours', '<EOS>']
predictions = ['tu', 'marche', '<EOS>']
use_teacher = [True, False, True]
input_token = '<BOS>'
seen_inputs = []
for t in range(len(target)):
    seen_inputs.append(input_token)
    input_token = target[t] if use_teacher[t] else predictions[t]
print(seen_inputs)
```

A) ['je', 'cours', '<EOS>']
B) ['<BOS>', 'tu', 'marche']
C) ['<BOS>', 'je', 'marche']
D) ['<BOS>', 'je', 'cours']

Learner answer: C. Correct answer: C. Result: correct.
Explanation: The first input is BOS. Teacher forcing at step0 supplies je for step1; the model prediction marche at step1 supplies step2 because use_teacher[1] is false. The last selected EOS would only be consumed by a further iteration.
Phase05 running initial score:25/27. Lesson09 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson10 docs read before its questions.

### Answer history: p05-l10-concept-v1

ID: p05-l10-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson10 — Attention Mechanism — The Breakthrough.
Question28/87; lesson question1/3; conceptual.

How does encoder-decoder attention address the fixed-context bottleneck of basic seq2seq?

A) It replaces every encoder state with the same constant vector before decoding.
B) It computes a query-dependent weighted sum of encoder states at each decoder step, letting the context change across output positions.
C) It forces source and target sequences to have identical length and vocabulary.
D) It selects one source token once and permanently ignores all other encoder states.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: Attention scores all encoder positions using the current decoder query and normalizes them into weights. Their weighted sum supplies a context that can change at each output step instead of relying only on one fixed final encoder state.
Phase05 running initial score:26/28. Lesson10 attempt1:1/1; incomplete.

### Answer history: p05-l10-application-v1

ID: p05-l10-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson10 — Attention Mechanism — The Breakthrough.
Question29/87; lesson question2/3; application.

Your batch pads source sequences to the same length. You want padding positions to receive zero attention weight while weights over real source positions sum to1. Assuming every sequence has at least one real token, which method is appropriate?

A) Set padded attention scores to0 before softmax, since exp(0) is0.
B) Apply softmax over the batch dimension instead of the source-position dimension.
C) Replace padded value vectors with zeros but leave their attention scores unmasked.
D) Mask padded scores with negative infinity before softmax over source positions.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Negative-infinity masked scores contribute exp(-inf)=0, so softmax over source positions assigns no probability mass to padding and normalizes over real positions. A score of0 contributes exp(0)=1; zero values alone do not remove padding from the normalization.
Phase05 running initial score:27/29. Lesson10 attempt1:2/2; incomplete.

### Answer history: p05-l10-code-v1

ID: p05-l10-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson10 — Attention Mechanism — The Breakthrough.
Question30/87; lesson question3/3; code tracing.

What context vector does this code print? The two encoder positions have attention scores0 and log(3), normalized with softmax.

```python
import math
states = [[2.0, 0.0], [0.0, 4.0]]
scores = [0.0, math.log(3.0)]
exp_scores = [math.exp(s) for s in scores]
weights = [e / sum(exp_scores) for e in exp_scores]
context = [sum(w * h[j] for w, h in zip(weights, states))
           for j in range(2)]
print([round(x, 2) for x in context])
```

A) [1.0, 2.0]
B) [1.5, 1.0]
C) [0.5, 3.0]
D) [2.0, 4.0]

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Exponentiating scores gives1 and3, so attention weights are0.25 and0.75. The context is0.25*[2,0]+0.75*[0,4]=[0.5,3.0].
Phase05 running initial score:28/30. Lesson10 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson11 docs read before its questions.

### Answer history: p05-l11-concept-v1

ID: p05-l11-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson11 — Machine Translation.
Question31/87; lesson question1/3; conceptual.

Which statement correctly distinguishes BLEU and chrF as translation evaluation metrics?

A) BLEU primarily uses word/token n-gram precision with a brevity penalty; chrF uses character n-gram precision and recall combined as an F-score.
B) BLEU measures only output fluency without a reference; chrF measures the model's parameter count.
C) BLEU guarantees semantic equivalence; chrF guarantees correct target-language selection.
D) BLEU counts character substitutions only; chrF computes exact whole-sentence match accuracy only.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: BLEU uses reference n-gram precision with a penalty for overly short hypotheses. chrF combines character n-gram precision and recall, providing complementary sensitivity to morphological overlap. Neither guarantees semantic correctness.
Phase05 running initial score:29/31. Lesson11 attempt1:1/1; incomplete.

### Answer history: p05-l11-application-v1

ID: p05-l11-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson11 — Machine Translation.
Question32/87; lesson question2/3; application.

Your UI translation system renders the same product term differently across screens, despite fluent sentences. You have an approved bilingual glossary. Which intervention most directly addresses this terminology drift?

A) Increase sampling randomness so each screen explores more synonyms.
B) Evaluate only sentence fluency and ignore whether glossary terms are preserved.
C) Use glossary-aware constrained decoding or validated terminology post-editing, then check glossary compliance on held-out UI strings.
D) Remove the product terms from source strings before translation and never restore them.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Glossary-aware decoding constraints or validated terminology post-editing directly address inconsistent approved terms. Held-out glossary checks assess whether the intervention improves consistency without relying on fluency alone.
Phase05 running initial score:30/32. Lesson11 attempt1:2/2; incomplete.

### Answer history: p05-l11-code-v1

ID: p05-l11-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson11 — Machine Translation.
Question33/87; lesson question3/3; code debugging.

This NLLB-style call is intended to translate English into French, but its target-language setting is wrong. Assume both language codes map to valid token IDs. Which change fixes the target-language selection?

```python
source_language = 'eng_Latn'
requested_target = 'fra_Latn'
inputs = tokenizer(english_text, return_tensors='pt')
output = model.generate(
    **inputs,
    forced_bos_token_id=tokenizer.convert_tokens_to_ids(source_language),
    num_beams=5,
)
```

A) Increase num_beams to10 while keeping the forced language token unchanged.
B) Use requested_target instead of source_language when setting forced_bos_token_id.
C) Reverse the English input string before tokenization.
D) Change only the output filename to include a French language suffix.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: The forced language token must identify the requested target language, fra_Latn, rather than the English source. This corrects the target-language setting; increasing beam width does not change the selected language token.
Phase05 running initial score:31/33. Lesson11 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson12 docs read before its questions.

### Answer history: p05-l12-concept-v1

ID: p05-l12-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson12 — Text Summarization.
Question34/87; lesson question1/3; conceptual.

Which statement correctly distinguishes extractive and abstractive summarization?

A) Extractive summarization generates new sentences; abstractive summarization only copies source sentences.
B) Both must reproduce every source sentence in its original order and length.
C) Extractive summarization selects source sentences; abstractive summarization generates a condensed rewrite that may introduce unsupported claims.
D) Extractive summarization guarantees every selected sentence is accurate and meaningful without context; abstractive summarization cannot change facts.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Extractive summarization selects text from the source, while abstractive methods generate new wording. Generated summaries can introduce unsupported claims; extracted sentences can also mislead when stripped of necessary context, so neither approach guarantees factual adequacy.
Phase05 running initial score:32/34. Lesson12 attempt1:1/1; incomplete.

### Answer history: p05-l12-application-v1

ID: p05-l12-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson12 — Text Summarization.
Question35/87; lesson question2/3; application.

An abstractive summary has strong ROUGE overlap with a reference but changes "rejected the offer" to "accepted the offer". What evaluation change best detects this failure?

A) Add source-grounded factuality checks, such as entailment or question-answer consistency, alongside overlap metrics.
B) Increase the ROUGE threshold and assume high lexical overlap guarantees factual consistency.
C) Check only whether the summary contains the same named entities as the source.
D) Reward fluent wording regardless of whether the source supports the summary's claims.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: A polarity flip can preserve much of a sentence's wording and entities while reversing its meaning. Source-grounded entailment or QA consistency checks target factual support, complementing lexical-overlap metrics such as ROUGE.
Phase05 running initial score:33/35. Lesson12 attempt1:2/2; incomplete.

### Answer history: p05-l12-code-v1

ID: p05-l12-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson12 — Text Summarization.
Question36/87; lesson question3/3; code tracing.

After sentence scoring, the lesson selects the top2 sentences and then restores source order. What does this code print?

```python
sentences = ['Opening.', 'Evidence.', 'Conclusion.']
scores = [0.2, 0.8, 0.9]
ranked = sorted(range(len(sentences)),
                key=lambda i: scores[i], reverse=True)[:2]
ranked.sort()
print([sentences[i] for i in ranked])
```

A) ['Conclusion.', 'Evidence.']
B) ['Opening.', 'Evidence.']
C) ['Evidence.', 'Conclusion.']
D) ['Opening.', 'Conclusion.']

Learner answer: A. Correct answer: C. Result: incorrect.
Explanation: Ranking by score first selects indices[2,1], but ranked.sort() then restores ascending source indices[1,2]. The returned sentences are ['Evidence.','Conclusion.'], not descending score order.
Phase05 running initial score:33/36. Lesson12 attempt1 complete:2/3, meeting the lesson minimum. Selection by importance versus final source order added to the review queue. Lessons remain todo until the full phase passes. Full Lesson13 docs read before its questions.

### Answer history: p05-l13-concept-v1

ID: p05-l13-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson13 — Question Answering Systems.
Question37/87; lesson question1/3; conceptual.

Which description correctly distinguishes extractive QA, retrieval-augmented QA, and closed-book generative QA?

A) Extractive QA generates unrestricted new text; retrieval-augmented QA never uses documents; closed-book QA always cites retrieved passages.
B) All three require the same supplied passage and output only its start and end token indices.
C) Extractive QA trains a search index; retrieval-augmented QA assigns POS tags; closed-book QA only translates questions.
D) Extractive QA selects an answer span from a passage; retrieval-augmented QA first fetches evidence; closed-book QA answers from model parameters without retrieval.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Extractive readers return spans from supplied passages. Retrieval-augmented QA adds evidence retrieval before an extractive or generative reader. Closed-book generation uses model parameters without an external retrieval step.
Phase05 running initial score:34/37. Lesson13 attempt1:1/1; incomplete.

### Answer history: p05-l13-application-v1

ID: p05-l13-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson13 — Question Answering Systems.
Question38/87; lesson question2/3; application.

Your QA reader answers correctly when given the gold passage, but the end-to-end system often fails because its top5 retrieved passages omit the evidence. Which next step most directly addresses the diagnosed bottleneck?

A) Measure and improve retrieval recall@5 while retaining abstention when the retrieved context lacks sufficient evidence.
B) Fine-tune only the reader on the same gold passages and assume missing retrieval evidence is now fixed.
C) Instruct the reader to answer confidently even when no retrieved passage supports the answer.
D) Report only reader accuracy on gold passages as the end-to-end system's accuracy.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Strong performance with gold evidence isolates retrieval as the diagnosed failure. Retrieval recall@5 measures whether the needed evidence reaches the reader. Reader-only evaluation does not establish end-to-end accuracy, and insufficient context should still permit abstention.
Phase05 running initial score:35/38. Lesson13 attempt1:2/2; incomplete.

### Answer history: p05-l13-code-v1

ID: p05-l13-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson13 — Question Answering Systems.
Question39/87; lesson question3/3; code tracing.

This toy extractive reader scores every valid passage span by start_logit+end_logit. End indices are inclusive, spans must have at most2 tokens, and no-answer handling is omitted here. What does it print?

```python
tokens = ['in', 'New', 'York', 'today']
start = [0, 4, 1, 0]
end = [0, 0, 5, 1]
candidates = [(start[s] + end[e], s, e)
              for s in range(4)
              for e in range(s, min(4, s + 2))]
_, s, e = max(candidates)
print(' '.join(tokens[s:e+1]))
```

A) New
B) York
C) New York
D) New York today

Learner answer: C. Correct answer: C. Result: correct.
Explanation: The valid span from index1 to inclusive index2 has score4+5=9, the largest candidate score. Slicing tokens[1:3] prints New York. The three-token span is excluded by the length constraint.
Phase05 running initial score:36/39. Lesson13 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson14 docs read before its questions.

### Answer history: p05-l14-concept-v1

ID: p05-l14-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson14 — Information Retrieval and Search.
Question40/87; lesson question1/3; conceptual.

Why is Reciprocal Rank Fusion useful when combining BM25 and dense retrieval results?

A) It requires both retrievers to output identical raw score ranges before merging.
B) It replaces both retrievers with a classifier trained only on document length.
C) It discards ranking positions and adds raw BM25 scores directly to cosine similarities.
D) It combines evidence from rank positions without assuming the retrievers' raw scores share a common scale.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: RRF assigns contributions based on each document's rank, avoiding direct comparison of BM25 and dense similarity scores with different scales. Documents can accumulate evidence across ranked lists.
Phase05 running initial score:37/40. Lesson14 attempt1:1/1; incomplete.

### Answer history: p05-l14-application-v1

ID: p05-l14-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson14 — Information Retrieval and Search.
Question41/87; lesson question2/3; application.

You search a million-document corpus and can afford a cross-encoder only on a small candidate set. Which pipeline uses it appropriately?

A) Jointly encode the query with every document before doing any candidate retrieval.
B) Retrieve with BM25 and a dense bi-encoder, fuse their rankings, then jointly score query-document pairs from the shortlist.
C) Precompute each document's cross-encoder score once without a query and reuse that relevance score for every search.
D) Rerank only the single final answer after generation, without scoring candidate documents.

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: BM25 and a dense bi-encoder efficiently retrieve candidates; fusion combines their evidence. A cross-encoder then jointly processes the query with each shortlisted document, limiting expensive pairwise scoring to a small set.
Phase05 running initial score:38/41. Lesson14 attempt1:2/2; incomplete.

### Answer history: p05-l14-code-v1

ID: p05-l14-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson14 — Information Retrieval and Search.
Question42/87; lesson question3/3; code tracing.

This toy RRF example uses k=0 for easy arithmetic, with one-based ranks. Which document ranks first, and what is its fused score?

```python
rankings = [['A', 'B'], ['B', 'C']]
k = 0
scores = {}
for ranking in rankings:
    for rank, doc in enumerate(ranking, start=1):
        scores[doc] = scores.get(doc, 0.0) + 1 / (k + rank)
best = max(scores, key=scores.get)
print(best, scores[best])
```

A) A 1.0
B) B 1.0
C) B 1.5
D) C 1.5

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: B contributes1/2 from the first ranking and1 from the second, totaling1.5. A scores1 and C scores0.5, so B ranks first.
Phase05 running initial score:39/42. Lesson14 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson15 docs read before its questions.

### Answer history: p05-l15-concept-v1

ID: p05-l15-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson15 — Topic Modeling — LDA and BERTopic.
Question43/87; lesson question1/3; conceptual.

In Latent Dirichlet Allocation (LDA), what do a document's topic vector and a topic's word vector represent?

A) A document has one mandatory class label, and each topic contains only one word.
B) Both vectors are unnormalized counts of document lengths, unrelated to topic meaning.
C) A document's topic vector lists token positions, and a topic's word vector gives POS tags.
D) A document has a probability mixture over topics, and each topic has a probability distribution over vocabulary words.

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: LDA models each document as a mixture of latent topics and each topic as a distribution over words. Normalized document-topic and topic-word rows each sum to1, enabling mixed membership rather than requiring one topic per document.
Phase05 running initial score:40/43. Lesson15 attempt1:1/1; incomplete.

### Answer history: p05-l15-application-v1

ID: p05-l15-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson15 — Topic Modeling — LDA and BERTopic.
Question44/87; lesson question2/3; application.

You have long reports covering several themes and need an explicit topic-mixture distribution per report using the full text. Which setup most directly matches this requirement in the lesson?

A) Truncate each report to the embedding model's first few tokens and assume nothing important is lost.
B) Fit LDA on document word-count vectors and inspect each report's normalized document-topic distribution.
C) Use only BERTopic's hard topic label and interpret that single integer as a full multi-topic distribution.
D) Cluster reports by character count and call each document-length bucket a semantic topic.

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: LDA consumes word-count vectors and outputs a normalized topic mixture for each document, naturally matching long documents with multiple themes. A hard cluster ID alone is not a mixture distribution, and truncating text can discard relevant themes.
Phase05 running initial score:41/44. Lesson15 attempt1:2/2; incomplete.

### Answer history: p05-l15-code-v1

ID: p05-l15-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson15 — Topic Modeling — LDA and BERTopic.
Question45/87; lesson question3/3; code tracing.

The lesson excludes BERTopic's outlier label -1 when listing discovered topics. What does this code print?

```python
topic_ids = [-1, 0, 1, 2]
document_counts = [12, 30, 20, 18]
valid = [(topic, count)
         for topic, count in zip(topic_ids, document_counts)
         if topic != -1]
print(len(valid), sum(count for _, count in valid))
```

A) 4 80
B) 3 80
C) 4 68
D) 3 68

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: Filtering out topic-1 removes12 outlier documents and leaves topics0,1,and2. There are3 valid topics, with30+20+18=68 assigned documents in those topics.
Phase05 running initial score:42/45. Lesson15 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson16 docs read before its questions.

### Answer history: p05-l16-concept-v1

ID: p05-l16-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson16 — Text Generation Before Transformers — N-gram Language Models.
Question46/87; lesson question1/3; conceptual.

What is the central zero-count problem that smoothing addresses in an n-gram language model?

A) An unseen n-gram gets zero maximum-likelihood probability, making any sequence containing it have zero probability and infinite negative log-likelihood.
B) Every observed n-gram receives probability1, so all possible sentences are equally likely.
C) A trigram model requires the entire document as context before predicting any word.
D) Counting n-grams automatically changes the tokenizer each time the model is evaluated.

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: A zero-probability conditional event makes the product sequence probability zero and its negative log-likelihood infinite. Smoothing reallocates probability mass so unseen in-vocabulary events can receive nonzero probability.
Phase05 running initial score:43/46. Lesson16 attempt1:1/1; incomplete.

### Answer history: p05-l16-application-v1

ID: p05-l16-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson16 — Text Generation Before Transformers — N-gram Language Models.
Question47/87; lesson question2/3; application.

In a training corpus, "Francisco" occurs very often but almost exclusively after "San". Another word appears less often overall but after many different preceding words. What does Kneser-Ney's lower-order continuation model emphasize?

A) Raw token frequency only, so Francisco must have the greater continuation probability.
B) Word length, so the longer spelling always gets more probability.
C) The number of distinct preceding contexts, so the broadly distributed word can receive greater continuation probability.
D) Alphabetical order, so later words receive the probability mass removed by discounting.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: Kneser-Ney's continuation distribution counts distinct preceding contexts rather than only raw word occurrences. A word common only in one fixed phrase can therefore have lower continuation probability than a less frequent word seen in many contexts.
Phase05 running initial score:44/47. Lesson16 attempt1:2/2; incomplete.

### Answer history: p05-l16-code-v1

ID: p05-l16-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson16 — Text Generation Before Transformers — N-gram Language Models.
Question48/87; lesson question3/3; code tracing.

The model assigns the following probabilities to two held-out token events. What perplexity does the code print? Natural logarithms are used, and only these two events are scored.

```python
import math
probabilities = [0.5, 0.125]
mean_nll = -sum(math.log(p) for p in probabilities) / len(probabilities)
perplexity = math.exp(mean_nll)
print(round(perplexity, 2))
```

A) 0.31
B) 2.0
C) 16.0
D) 4.0

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: The joint probability of the two scored events is0.5*0.125=1/16. Per-token perplexity is(1/16)^(-1/2)=4, equivalently exp(mean negative natural log probability).
Phase05 running initial score:45/48. Lesson16 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson17 docs read before its questions.

### Answer history: p05-l17-concept-v1

ID: p05-l17-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson17 — Chatbots — Rule-Based to Neural to LLM Agents.
Question49/87; lesson question1/3; conceptual.

What distinguishes the lesson's tool-using agent loop from a chatbot that only generates a single text response?

A) It can claim an external action succeeded solely because its generated response sounds confident.
B) It treats every retrieved document as an instruction that overrides the user's task.
C) It emits tool calls that the runtime executes, observes their results, and uses those observations to decide subsequent steps.
D) It replaces all tool results with canned responses and never updates its conversation state.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: The runtime executes structured tool calls and returns observations to the model, which can decide whether to call another tool or produce a final response. Text claiming completion alone is not evidence that an external action occurred.
Phase05 running initial score:46/49. Lesson17 attempt1:1/1; incomplete.

### Answer history: p05-l17-application-v1

ID: p05-l17-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson17 — Chatbots — Rule-Based to Neural to LLM Agents.
Question50/87; lesson question2/3; application.

A support bot handles both "What is your return policy?" and "Delete my account permanently." Which hybrid routing design matches the lesson?

A) Use curated-answer retrieval for the FAQ and a structured, authenticated confirmation flow for account deletion.
B) Retrieve the nearest FAQ for both requests and treat the returned text as proof the account was deleted.
C) Let free-form generated text directly execute deletion whenever it mentions the word delete.
D) Send every request through an unbounded tool loop without checking action outcomes.

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: Curated retrieval fits informational FAQs, while authenticated structured confirmation flows control irreversible account actions. Completing an action requires successful execution and outcome verification, not merely a generated or retrieved sentence.
Phase05 running initial score:47/50. Lesson17 attempt1:2/2; incomplete.

### Answer history: p05-l17-code-v1

ID: p05-l17-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson17 — Chatbots — Rule-Based to Neural to LLM Agents.
Question51/87; lesson question3/3; code tracing.

In this simplified agent loop, llm always requests the valid lookup tool and lookup returns normally. What happens with max_steps=3?

```python
def run(llm, lookup, max_steps=3):
    history = []
    for _ in range(max_steps):
        response = llm(history)
        if response.get('tool_call'):
            result = lookup()
            history.append(result)
        else:
            return response['content']
    return 'Step budget exhausted.'
```

A) lookup runs once, then run automatically returns its result as the final answer.
B) lookup never runs because requesting a tool immediately exhausts the budget.
C) lookup runs three times, then run returns 'Step budget exhausted.'
D) lookup runs indefinitely because every successful result resets the for loop.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: range(3) allows exactly three model calls, each followed by one lookup because every response requests it. No final-text branch runs, so the function exits with Step budget exhausted after three lookups.
Phase05 running initial score:48/51. Lesson17 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson18 docs read before its questions.

### Answer history: p05-l18-concept-v1

ID: p05-l18-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson18 — Multilingual NLP.
Question52/87; lesson question1/3; conceptual.

Which scenario is zero-shot cross-lingual transfer for a classification task?

A) Train a separate classifier from scratch on labelled examples in every target language.
B) Fine-tune a multilingual model on English task labels, then evaluate the same task in a supported target language without using target-language task labels for training.
C) Fine-tune on500 labelled target-language examples, then describe the setup as having no target-language supervision.
D) Replace the multilingual tokenizer with an unrelated vocabulary while keeping all model weights unchanged.

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: Zero-shot cross-lingual transfer applies task supervision from a source language to a supported target language without target-language task labels in training. The multilingual model may still have seen unlabelled target-language text during pretraining.
Phase05 running initial score:49/52. Lesson18 attempt1:1/1; incomplete.

### Answer history: p05-l18-application-v1

ID: p05-l18-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson18 — Multilingual NLP.
Question53/87; lesson question2/3; application.

A multilingual classifier has high pooled accuracy on a test set dominated by English, but users report poor performance in two low-resource languages. Which evaluation most directly investigates this?

A) Increase the number of English test examples and report only pooled accuracy again.
B) Remove low-resource languages from the test set so the aggregate matches the main traffic.
C) Compare only model parameter counts across languages because task accuracy is language-independent.
D) Report held-out metrics separately for each language and check consistency on meaning-equivalent examples across languages.

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: Per-language held-out metrics reveal failures hidden by English-heavy pooled evaluation. Cross-lingual consistency tests assess whether meaning-equivalent inputs receive consistent predictions, complementing per-language task metrics.
Phase05 running initial score:50/53. Lesson18 attempt1:2/2; incomplete.

### Answer history: p05-l18-code-v1

ID: p05-l18-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson18 — Multilingual NLP.
Question54/87; lesson question3/3; code tracing.

This diagnostic defines tokenizer fertility as subword tokens per word. Two samples each contain10 words; special tokens are excluded. What does it print, and which sample consumes more context positions per word?

```python
word_counts = {'en': 10, 'target': 10}
subword_counts = {'en': 12, 'target': 36}
fertility = {lang: subword_counts[lang] / word_counts[lang]
             for lang in word_counts}
ratio = fertility['target'] / fertility['en']
print(fertility['en'], fertility['target'], ratio)
```

A) 1.2 3.6 3.0; the target sample uses three times as many tokens per word.
B) 1.2 3.6 0.33; the target sample uses fewer tokens per word.
C) 12.0 36.0 3.0; fertility counts whole-sample tokens rather than tokens per word.
D) 1.2 1.2 1.0; equal word counts guarantee equal tokenizer fertility.

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: English fertility is12/10=1.2 and target fertility is36/10=3.6. The ratio3.6/1.2=3 means the target sample consumes three times as many subword positions per word.
Phase05 running initial score:51/54. Lesson18 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson19 docs read before its questions.

### Answer history: p05-l19-concept-v1

ID: p05-l19-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson19 — Subword Tokenization — BPE, WordPiece, Unigram, SentencePiece.
Question55/87; lesson question1/3; conceptual.

Which statement correctly contrasts the vocabulary-learning strategies of BPE and Unigram tokenization?

A) BPE starts with full sentences and deletes rare words; Unigram merges only punctuation pairs.
B) Both assign exactly one token to every word and cannot split unseen spellings.
C) BPE grows units through frequent adjacent-pair merges; Unigram starts with a large candidate vocabulary and prunes pieces using a likelihood-based objective.
D) BPE requires grammatical POS tags; Unigram replaces every word with its dictionary lemma.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: BPE constructs larger units by merging frequent adjacent pairs. Unigram begins with many candidate pieces and removes pieces according to a likelihood-based objective, retaining a probabilistic segmentation model.
Phase05 running initial score:52/55. Lesson19 attempt1:1/1; incomplete.

### Answer history: p05-l19-application-v1

ID: p05-l19-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson19 — Subword Tokenization — BPE, WordPiece, Unigram, SentencePiece.
Question56/87; lesson question2/3; application.

A model was trained with tokenizer A. Tokenizer B has the same vocabulary size but maps text pieces to different token IDs. You want to deploy the existing checkpoint without changing its weights. What should you do?

A) Use B because matching vocabulary sizes guarantees equivalent embedding meanings.
B) Randomly switch between A and B at inference to improve vocabulary coverage.
C) Sort B's output IDs numerically before passing them into the model.
D) Deploy the checkpoint's matching tokenizer A, pin its vocabulary and configuration, and verify representative encodings.

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: Token IDs select specific learned embedding rows and output vocabulary entries. Equal vocabulary size does not ensure equal token semantics. Serving the matching pinned tokenizer preserves the mapping expected by the unchanged checkpoint.
Phase05 running initial score:53/56. Lesson19 attempt1:2/2; incomplete.

### Answer history: p05-l19-code-v1

ID: p05-l19-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson19 — Subword Tokenization — BPE, WordPiece, Unigram, SentencePiece.
Question57/87; lesson question3/3; code tracing.

Which adjacent pair does this BPE training step choose for its first merge? Counts are weighted by each word's corpus frequency, and there is no tie for the winning pair.

```python
from collections import Counter
corpus = {'ab': 5, 'ac': 2, 'db': 1}
pairs = Counter()
for word, frequency in corpus.items():
    symbols = list(word) + ['</w>']
    for a, b in zip(symbols, symbols[1:]):
        pairs[(a, b)] += frequency
print(pairs.most_common(1)[0])
```

A) (('a', 'b'), 5)
B) (('b', '</w>'), 6)
C) (('a', 'c'), 2)
D) (('d', 'b'), 1)

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: The pair(b,</w>) occurs in ab with frequency5 and db with frequency1, totaling6. This exceeds(a,b) at5 and is the first merge selected by frequency-weighted pair counting.
Phase05 running initial score:54/57. Lesson19 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson20 docs read before its questions.

### Answer history: p05-l20-concept-v1

ID: p05-l20-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson20 — Structured Outputs & Constrained Decoding.
Question58/87; lesson question1/3; conceptual.

How does grammar-constrained decoding restrict output during generation, and what does schema compliance alone leave unverified?

A) It edits completed text after sampling and guarantees every remaining claim is factually correct.
B) It masks invalid next-token logits according to grammar state; a schema-compliant completion can still contain unsupported or incorrect field values.
C) It removes all low-probability tokens regardless of grammar and guarantees the highest-probability answer is true.
D) It relies only on a polite JSON prompt and verifies every claim against the source automatically.

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: Constrained decoding masks tokens that would violate the active grammar. Schema validity concerns output structure and permitted values; it does not prove that generated values are supported by the source or factually correct.
Phase05 running initial score:55/58. Lesson20 attempt1:1/1; incomplete.

### Answer history: p05-l20-application-v1

ID: p05-l20-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson20 — Structured Outputs & Constrained Decoding.
Question59/87; lesson question2/3; application.

An extraction schema requires an event_date string matching YYYY-MM-DD, but some source documents contain no date. You want the model to represent missing evidence without inventing a date. Which schema design best supports this?

A) Keep the date mandatory and non-nullable; syntactic validity guarantees a supported date exists.
B) Substitute today's date whenever the source is silent and present it as extracted evidence.
C) Allow an explicit null or unknown state and validate non-null dates against source evidence.
D) Increase sampling temperature while requiring a date-shaped string for every document.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: A null or explicit unknown state lets the extraction express that no date is supported. Non-null values still need evidence checks; requiring a date-shaped string alone cannot ensure the source contains a date.
Phase05 running initial score:56/59. Lesson20 attempt1:2/2; incomplete.

### Answer history: p05-l20-code-v1

ID: p05-l20-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson20 — Structured Outputs & Constrained Decoding.
Question60/87; lesson question3/3; code tracing.

The current grammar state allows only token IDs1 and3. Which token ID does this constrained greedy step select?

```python
logits = [9.0, 2.0, 7.0, 4.0]
valid_token_ids = [1, 3]
masked = [float('-inf')] * len(logits)
for tid in valid_token_ids:
    masked[tid] = logits[tid]
next_id = max(range(len(masked)), key=masked.__getitem__)
print(next_id)
```

A) 0
B) 1
C) 2
D) 3

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: The masked logits are[-inf,2,-inf,4]. Token3 has the highest allowed logit, so constrained greedy decoding selects3 even though invalid token0 had the largest original logit.
Phase05 running initial score:57/60. Lesson20 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson21 docs read before its questions.

### Answer history: p05-l21-concept-v1

ID: p05-l21-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson21 — Natural Language Inference — Textual Entailment.
Question61/87; lesson question1/3; conceptual.

Premise: "A dog is sleeping on the sofa." Hypothesis: "The dog is hungry." Under the premise alone, which NLI label fits?

A) Entailment, because every sleeping dog must be hungry.
B) Contradiction, because sleeping rules out hunger.
C) Neutral, because the premise neither establishes nor rules out hunger.
D) Entailment, because the premise and hypothesis both mention a dog.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: The premise establishes sleeping and location, not hunger or its absence. Shared words do not establish entailment, and absence of evidence is not contradiction. The relationship is neutral.
Phase05 running initial score:58/61. Lesson21 attempt1:1/1; incomplete.

### Answer history: p05-l21-application-v1

ID: p05-l21-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson21 — Natural Language Inference — Textual Entailment.
Question62/87; lesson question2/3; application.

You use NLI to check a generated answer against retrieved evidence. Which setup best tests source support without confusing unsupported claims with proven falsehoods?

A) Split the answer into atomic claims, use evidence as premise and each claim as hypothesis, and flag neutral or contradictory claims as unsupported by that evidence.
B) Use each claim as the premise and the whole source as hypothesis, treating every neutral result as proof the claim is false.
C) Check only word overlap and mark any claim sharing source words as entailed.
D) Ignore neutral results because every claim not explicitly contradicted must be supported.

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: Source support is directional: the evidence is the premise and the answer claim is the hypothesis. Neutral means the evidence does not establish or rule out the claim, whereas contradiction means it rules out the claim. Neither is an entailed claim; NLI predictions remain fallible.
Phase05 running initial score:59/62. Lesson21 attempt1:2/2; incomplete.

### Answer history: p05-l21-code-v1

ID: p05-l21-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson21 — Natural Language Inference — Textual Entailment.
Question63/87; lesson question3/3; code tracing.

This toy support checker accepts a claim only when its entailment probability is strictly greater than0.5. What does it print? Treat these scores as supplied model outputs, not ground-truth proof.

```python
entailment_scores = [0.9, 0.5, 0.2, 0.8]
threshold = 0.5
supported = [score > threshold for score in entailment_scores]
support_rate = sum(supported) / len(supported)
print(supported, support_rate)
```

A) [True, True, False, True] 0.75
B) [True, False, False, True] 0.5
C) [True, False, True, True] 0.75
D) [False, False, False, True] 0.25

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: Only0.9 and0.8 exceed0.5. A score equal to0.5 fails the strict comparison, so supported=[True,False,False,True] and support_rate=2/4=0.5.
Phase05 running initial score:60/63. Lesson21 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson22 docs read before its questions.

### Answer history: p05-l22-concept-v1

ID: p05-l22-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson22 — Embedding Models — The 2026 Deep Dive.
Question64/87; lesson question1/3; conceptual.

Which description correctly distinguishes dense, learned-sparse, and late-interaction multi-vector text retrieval representations?

A) Dense stores one vector per passage; learned-sparse stores mostly-zero vocabulary weights; multi-vector stores token vectors and aggregates query-to-document token similarities.
B) Dense stores only exact word counts; learned-sparse stores a single class label; multi-vector generates answer text without an index.
C) All three store exactly one scalar per passage and differ only in how document IDs are sorted.
D) Multi-vector requires query and document text to be identical, while dense and sparse methods never encode queries.

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: Dense passage retrieval typically stores one fixed-width vector per passage. Learned sparse vectors assign weights to a small subset of vocabulary dimensions. Late-interaction multi-vector methods retain token vectors and aggregate token-level similarities at scoring time.
Phase05 running initial score:61/64. Lesson22 attempt1:1/1; incomplete.

### Answer history: p05-l22-application-v1

ID: p05-l22-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson22 — Embedding Models — The 2026 Deep Dive.
Question65/87; lesson question2/3; application.

Your embedding index exceeds its storage budget. The encoder was explicitly trained with a Matryoshka objective supporting shorter prefix embeddings. Which change best uses that property?

A) Remove arbitrary dimensions from gallery vectors only, leaving full-size query vectors unchanged.
B) Assume any encoder can be truncated to any width with no accuracy loss.
C) Truncate query and gallery embeddings to the same supported prefix width, re-normalize nonzero vectors for cosine scoring, and measure retrieval quality on held-out domain queries.
D) Replace every vector with its first coordinate and report the original full-width benchmark score.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: Matryoshka training makes supported embedding prefixes useful as smaller representations. Both query and gallery must use matching dimensions; re-normalization supports cosine scoring. Domain evaluation measures the actual quality-storage tradeoff rather than assuming lossless truncation.
Phase05 running initial score:62/65. Lesson22 attempt1:2/2; incomplete.

### Answer history: p05-l22-code-v1

ID: p05-l22-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson22 — Embedding Models — The 2026 Deep Dive.
Question66/87; lesson question3/3; code tracing.

Rows of sim correspond to query tokens; columns correspond to document tokens. The lesson's MaxSim sums each query token's best document-token similarity. What does the code print?

```python
sim = [[0.2, 0.9, 0.1],
       [0.8, 0.3, 0.4]]
score = sum(max(row) for row in sim)
print(round(score, 2))
```

A) 0.9
B) 1.5
C) 2.7
D) 1.7

Learner answer: B. Correct answer: D. Result: incorrect. Recorded2026-10-25.
Explanation: MaxSim takes the maximum in each query-token row:0.9 and0.8. Their sum is1.7. It does not maximize over columns, whose maxima would sum to2.1.
Phase05 running initial score:62/66. Lesson22 attempt1 complete:2/3, meeting the lesson minimum. MaxSim row-wise aggregation added to the review queue. Lessons remain todo until the full phase passes. Full Lesson23 docs read before its questions.

### Answer history: p05-l23-concept-v1

ID: p05-l23-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson23 — Chunking Strategies for RAG.
Question67/87; lesson question1/3; conceptual.

What distinguishes late chunking from independently embedding chunks split before encoding?

A) Late chunking sorts documents by their lengths and discards all token-level representations.
B) Late chunking encodes the document with cross-chunk context first, then pools contextualized token representations into chunk vectors.
C) Late chunking retrieves whole documents without computing any embeddings.
D) Late chunking only adds overlap after retrieval and never changes how chunk embeddings are produced.

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: Late chunking pools token representations after context-aware document encoding, so a chunk vector can reflect information beyond the chunk's boundaries. Independent pre-split encoding lacks that direct cross-chunk context and must respect the encoder's context limit.
Phase05 running initial score:63/67. Lesson23 attempt1:1/1; incomplete.

### Answer history: p05-l23-application-v1

ID: p05-l23-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson23 — Chunking Strategies for RAG.
Question68/87; lesson question2/3; application.

Small chunks retrieve the right clause, but answering requires surrounding definitions from the same section. Which parent-document design addresses this while avoiding repeated context?

A) Retrieve small child chunks, expand matches to their parent sections, and deduplicate parent IDs before assembling context.
B) Concatenate all documents before chunking so definitions from unrelated sources can share one chunk.
C) Return the same parent once for every matching child, regardless of repeated content or context budget.
D) Delete parent links and ask the reader to infer all missing definitions from the child text alone.

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: Child chunks provide focused retrieval matches, while expanding to parents restores surrounding definitions. Deduplicating by parent ID avoids repeatedly adding the same section when several children match; context budgets still need enforcement.
Phase05 running initial score:64/68. Lesson23 attempt1:2/2; incomplete.

### Answer history: p05-l23-code-v1

ID: p05-l23-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson23 — Chunking Strategies for RAG.
Question69/87; lesson question3/3; code tracing.

Retrieved children are already in descending relevance order. What parent ID list does this code return after deduplication?

```python
retrieved_parent_ids = [2, 2, 0, 2, 1]
seen = set()
parents = []
for parent_id in retrieved_parent_ids:
    if parent_id not in seen:
        parents.append(parent_id)
        seen.add(parent_id)
print(parents)
```

A) [0, 1, 2]
B) [2, 2, 0, 2, 1]
C) [2, 0, 1]
D) [2, 1, 0]

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: The loop appends each parent only on its first occurrence, preserving first-seen retrieval order. Parent2 is added once, then0, then1, producing[2,0,1]. The set is used only for membership, not output ordering.
Phase05 running initial score:65/69. Lesson23 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson24 docs read before its questions.

### Answer history: p05-l24-concept-v1

ID: p05-l24-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson24 — Coreference Resolution.
Question70/87; lesson question1/3; conceptual.

In "Maya founded Acme. She later sold the company", assume She refers to Maya and the company refers to Acme. What should coreference resolution produce?

A) One cluster containing every noun and pronoun because they occur in the same document.
B) Two clusters: {Maya, She} and {Acme, the company}, linking mentions of the same entity.
C) Four unrelated entity IDs because each surface string is different.
D) One grammatical POS tag for the entire sentence, without linking any mentions.

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: Coreference groups mentions that refer to the same entity, even when their surface strings differ. Under the stated referents, Maya and She form one cluster, while Acme and the company form another.
Phase05 running initial score:66/70. Lesson24 attempt1:1/1; incomplete.

### Answer history: p05-l24-application-v1

ID: p05-l24-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson24 — Coreference Resolution.
Question71/87; lesson question2/3; application.

An LLM returns coreference clusters for a long document. Some reported mentions are absent from the text, and several distinct people have been merged. Which validation most directly targets these failures?

A) Accept every cluster if its JSON parses, since schema validity proves correct reference linking.
B) Assign all pronouns to the nearest capitalized name without checking context.
C) Evaluate only how many clusters were returned and ignore their contents.
D) Verify mention spans and offsets against the source, and evaluate mention coverage and linking quality against annotated examples, including over-merges.

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: Span-offset checks detect reported mentions that do not match the source. Annotated mention coverage and linking evaluation detect missed mentions and wrong merges; valid JSON or the number of clusters alone does not verify entity identity.
Phase05 running initial score:67/71. Lesson24 attempt1:2/2; incomplete.

### Answer history: p05-l24-code-v1

ID: p05-l24-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson24 — Coreference Resolution.
Question72/87; lesson question3/3; code tracing.

These mention links are accepted as coreference predictions. The code merges linked clusters transitively. What does it print? The task is to trace clustering, not judge the supplied predictions.

```python
clusters = [{0}, {1}, {2}, {3}]
for a, b in [(0, 2), (2, 3)]:
    left = next(c for c in clusters if a in c)
    right = next(c for c in clusters if b in c)
    if left is not right:
        left.update(right)
        clusters.remove(right)
print(sorted(sorted(c) for c in clusters))
```

A) [[0, 2], [1], [3]]
B) [[0, 2, 3], [1]]
C) [[0], [1], [2, 3]]
D) [[0, 1, 2, 3]]

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: Linking0 with2 produces{0,2}; linking2 with3 merges3 into that same cluster. Mention1 remains separate, giving[[0,2,3],[1]].
Phase05 running initial score:68/72. Lesson24 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson25 docs read before its questions.

### Answer history: p05-l25-concept-v1

ID: p05-l25-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson25 — Entity Linking & Disambiguation.
Question73/87; lesson question1/3; conceptual.

What does entity linking add after NER has identified "Paris" as an entity mention?

A) It assigns a grammatical POS tag to each character in the mention.
B) It groups every place name in the document into one entity regardless of identity.
C) It maps the mention, using context, to a particular knowledge-base entry such as Paris, France or Paris, Texas, or identifies no matching entry.
D) It translates the surface string into every supported language without choosing an identity.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: Entity linking resolves a detected mention to a specific knowledge-base identity using context and candidates. If no entry represents the entity, the system should support a NIL result rather than forcing an incorrect link.
Phase05 running initial score:69/73. Lesson25 attempt1:1/1; incomplete.

### Answer history: p05-l25-application-v1

ID: p05-l25-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson25 — Entity Linking & Disambiguation.
Question74/87; lesson question2/3; application.

The correct entity exists in your KB but is absent from the candidate list for many mentions. Your disambiguator chooses correctly whenever the gold entry is supplied. Which change directly targets the bottleneck?

A) Improve alias coverage or candidate retrieval, and measure candidate recall separately from disambiguation accuracy.
B) Train only the disambiguator and assume it can select a gold entry absent from its candidate set.
C) Mark every missing candidate as NIL even though the correct entity exists in the KB.
D) Report accuracy only on mentions whose gold entries were supplied, as if it were end-to-end accuracy.

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: The failure is candidate generation, so alias coverage or retrieval recall needs improvement. A candidate-restricted disambiguator cannot select a missing gold entry; conditional disambiguation accuracy alone hides that end-to-end limitation. NIL means no matching KB entry, not merely retrieval failure.
Phase05 running initial score:70/74. Lesson25 attempt1:2/2; incomplete.

### Answer history: p05-l25-code-v1

ID: p05-l25-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson25 — Entity Linking & Disambiguation.
Question75/87; lesson question3/3; code tracing.

This toy disambiguator ranks supplied candidates by Jaccard overlap with context words. What does it print?

```python
context = {'apple', 'released', 'phone'}
descriptions = {
    'COMPANY': {'apple', 'technology', 'phone'},
    'FRUIT': {'apple', 'fruit', 'tree'},
}
scores = {
    entity: len(context & words) / len(context | words)
    for entity, words in descriptions.items()
}
best = max(scores, key=scores.get)
print(best, round(scores[best], 2))
```

A) FRUIT 0.2
B) COMPANY 0.67
C) COMPANY 0.5
D) FRUIT 0.5

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: COMPANY shares apple and phone with the context, giving intersection size2 and union size4, so Jaccard=0.5. FRUIT shares only apple with union size5, so its score is0.2. COMPANY wins.
Phase05 running initial score:71/75. Lesson25 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson26 docs read before its questions.

### Answer history: p05-l26-concept-v1

ID: p05-l26-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson26 — Relation Extraction & Knowledge Graph Construction.
Question76/87; lesson question1/3; conceptual.

An extractor finds both entity names in a sentence and outputs a subject-relation-object triple. Why are matching entity spans alone insufficient to establish that the triple is supported?

A) Finding both names guarantees that every possible relation between them is true.
B) Entity spans only matter for tokenization and cannot be recorded as provenance.
C) Closed-ontology relation IDs make the source sentence irrelevant.
D) Both entities may occur without the asserted relation; verification must check the source's relationship, direction, and relevant qualifiers as well as the spans.

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: Matching names anchors entity mentions but does not prove the predicate, argument direction, or temporal and other qualifiers. Relation verification must check the asserted relationship in source context, including negation, rather than merely entity co-occurrence.
Phase05 running initial score:72/76. Lesson26 attempt1:1/1; incomplete.

### Answer history: p05-l26-application-v1

ID: p05-l26-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson26 — Relation Extraction & Knowledge Graph Construction.
Question77/87; lesson question2/3; application.

A source states, "Maya worked at Acme from2019 to2022." You are adding this fact to a graph used for historical queries. Which representation best preserves its meaning and auditability?

A) Store only (Maya, worksAt, Acme) and treat it as a permanent current relationship.
B) Store canonical entity/relation IDs with start2019, end2022, and source document/span provenance.
C) Store (Acme, worksAt, Maya) without dates because relation direction does not matter.
D) Replace the employment fact with today's date and discard the original source.

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: Canonical IDs identify the entities and relation consistently, temporal qualifiers preserve when employment held, and document/span provenance supports auditing the assertion. Omitting time or reversing arguments changes the intended fact.
Phase05 running initial score:73/77. Lesson26 attempt1:2/2; incomplete.

### Answer history: p05-l26-code-v1

ID: p05-l26-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson26 — Relation Extraction & Knowledge Graph Construction.
Question78/87; lesson question3/3; code debugging.

Your target ontology defines foundedBy as (organization, foundedBy, person). The source triple is ('Maya','founded','Acme'). Which replacement for the return line preserves the relation's meaning?

```python
def canonicalize(subject, relation, obj):
    if relation == 'founded':
        return (subject, 'foundedBy', obj)  # fix this line
```

A) return (obj, 'foundedBy', subject)
B) return (subject, 'foundedBy', obj)
C) return (subject, 'foundedBy', subject)
D) return (obj, 'foundedBy', obj)

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: The ontology defines foundedBy with organization as subject and person as object. Inverting the extracted founded relation therefore requires swapping arguments, yielding(Acme,foundedBy,Maya).
Phase05 running initial score:74/78. Lesson26 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson27 docs read before its questions.

### Answer history: p05-l27-concept-v1

ID: p05-l27-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson27 — LLM Evaluation — RAGAS, DeepEval, G-Eval.
Question79/87; lesson question1/3; conceptual.

An answer addresses the user's question directly but includes a claim not supported by the retrieved context. Which distinction matters when evaluating it?

A) Answer relevance and faithfulness are identical, so a relevant answer must be fully grounded.
B) Faithfulness measures only writing fluency; answer relevance measures source entailment.
C) It may have high answer relevance but lower faithfulness, because addressing the question differs from supporting every claim with context.
D) Unsupported claims automatically prove that none of the retrieved passages are relevant.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: Relevance asks whether an answer addresses the question; faithfulness asks whether claims are supported by retrieved context. An on-topic answer may still include unsupported claims, so the dimensions should be assessed separately.
Phase05 running initial score:75/79. Lesson27 attempt1:1/1; incomplete.

### Answer history: p05-l27-application-v1

ID: p05-l27-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson27 — LLM Evaluation — RAGAS, DeepEval, G-Eval.
Question80/87; lesson question2/3; application.

Your average LLM-judge score rises after you change both the QA system and the judge model. Which procedure best separates actual system improvement from judge drift?

A) Attribute the entire score increase to the QA system without rerunning the old outputs.
B) Keep only examples where the new judge agrees with the improvement claim.
C) Drop failed judge responses from the aggregate without reporting their frequency.
D) Rescore old and new system outputs with the same pinned judge and rubric on a versioned test set, and compare judge decisions with human labels.

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: Evaluating both system versions with one pinned judge, rubric, and dataset controls the measurement change. Human-label calibration checks whether judge scores track desired quality rather than merely stylistic preferences; failed evaluations must remain visible.
Phase05 running initial score:76/80. Lesson27 attempt1:2/2; incomplete.

### Answer history: p05-l27-code-v1

ID: p05-l27-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson27 — LLM Evaluation — RAGAS, DeepEval, G-Eval.
Question81/87; lesson question3/3; code tracing.

The evaluation gate requires both mean score>=0.85 and no individual score below0.5. What does this code print?

```python
scores = [0.95, 0.95, 0.95, 0.95, 0.45]
mean_score = sum(scores) / len(scores)
passed = mean_score >= 0.85 and min(scores) >= 0.5
print(round(mean_score, 2), passed)
```

A) 0.85 False
B) 0.85 True
C) 0.95 False
D) 0.45 True

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: The mean rounds to0.85, but the minimum score is0.45, below0.5. The conjunction is false regardless of the mean, so the gate exposes an individual low-scoring failure hidden by the aggregate.
Phase05 running initial score:77/81. Lesson27 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson28 docs read before its questions.

### Answer history: p05-l28-concept-v1

ID: p05-l28-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson28 — Long-Context Evaluation — NIAH, RULER, LongBench, MRCR.
Question82/87; lesson question1/3; conceptual.

A model reliably retrieves one explicitly planted fact from a long prompt. Why is that insufficient evidence that it can reason accurately over multiple dispersed facts at the same length?

A) Single-fact retrieval and multi-hop reasoning test different capabilities; success on one does not establish success on the other.
B) Passing retrieval automatically guarantees all reasoning tasks, so no additional evidence is needed.
C) Long-context reasoning accuracy depends only on the advertised maximum token count.
D) A planted fact test measures model parameter count rather than whether the model can use the input.

Learner answer: A. Correct answer: A. Result: correct. Recorded2026-10-25.
Explanation: Retrieving a single fact does not establish the ability to combine dispersed facts, trace dependencies, or aggregate many values. Effective retrieval and reasoning lengths should be measured separately on tasks matching the workload.
Phase05 running initial score:78/82. Lesson28 attempt1:1/1; incomplete.

### Answer history: p05-l28-application-v1

ID: p05-l28-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson28 — Long-Context Evaluation — NIAH, RULER, LongBench, MRCR.
Question83/87; lesson question2/3; application.

You must evaluate a model for answering questions over long reports, where evidence may appear anywhere and require several reasoning steps. Which evaluation plan best fits?

A) Test one short prompt with the answer at the beginning, then extrapolate to the advertised context limit.
B) Use only the vendor's maximum token count as the acceptance criterion.
C) Sweep context lengths and evidence depths, include single-fact retrieval plus domain multi-hop tasks, and report accuracy and latency separately by task.
D) Test only exact keyword lookup at the middle position and report its score as multi-hop accuracy.

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: Length and depth sweeps expose position- and scale-dependent failures. Adding domain multi-hop tasks distinguishes reasoning from retrieval, while task-specific accuracy and latency reflect practical capacity more directly than an advertised token limit.
Phase05 running initial score:79/83. Lesson28 attempt1:2/2; incomplete.

### Answer history: p05-l28-code-v1

ID: p05-l28-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson28 — Long-Context Evaluation — NIAH, RULER, LongBench, MRCR.
Question84/87; lesson question3/3; code tracing.

For this exercise, effective length is the largest tested length with accuracy>=0.9. What does this code print for retrieval and reasoning, respectively? Lengths are in thousands of tokens.

```python
lengths = [4, 16, 64, 128]
retrieval = [0.99, 0.98, 0.95, 0.91]
reasoning = [0.96, 0.92, 0.75, 0.40]
def effective_length(scores):
    return max(length for length, score in zip(lengths, scores)
               if score >= 0.9)
print(effective_length(retrieval), effective_length(reasoning))
```

A) 128 128
B) 64 16
C) 16 128
D) 128 16

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: Retrieval stays above0.9 at all tested lengths, including128k. Reasoning meets0.9 only at4k and16k, so its largest passing tested length is16k. These are task-specific observed cutoffs, not proof about untested lengths.
Phase05 running initial score:80/84. Lesson28 attempt1 complete:3/3. Lessons remain todo until the full phase passes. Full Lesson29 docs read before its questions.

### Answer history: p05-l29-concept-v1

ID: p05-l29-concept-v1
Phase05 — NLP — Foundations to Advanced; Lesson29 — Dialogue State Tracking.
Question85/87; lesson question1/3; conceptual.

What does Joint Goal Accuracy (JGA) measure in dialogue state tracking?

A) The fraction of individual slot values that are correct, averaged independently across all slots.
B) The fraction of turns where at least one slot is correct, regardless of the remaining state.
C) The similarity of the generated reply's wording to a reference reply.
D) The fraction of evaluated turns where the entire predicted slot-value state matches the gold state.

Learner answer: D. Correct answer: D. Result: correct. Recorded2026-10-25.
Explanation: Joint Goal Accuracy gives credit for a turn only when every slot in the predicted state matches the gold state. It differs from independent per-slot accuracy, which can remain high despite at least one wrong slot on many turns.
Phase05 running initial score:81/85. Lesson29 attempt1:1/1; incomplete.

### Answer history: p05-l29-application-v1

ID: p05-l29-application-v1
Phase05 — NLP — Foundations to Advanced; Lesson29 — Dialogue State Tracking.
Question86/87; lesson question2/3; application.

The current booking state is {cuisine: italian, area: north, price: cheap, people:4}. The user says, "Actually make it moderate, and never mind the cuisine." What state update respects the user's correction and preserves untouched slots?

A) Clear every slot because a correction starts a completely new conversation.
B) Set price to moderate, clear cuisine, and preserve area north and people4.
C) Append moderate to cheap and keep italian because filled slots cannot change.
D) Change people to moderate and clear area because those slots were mentioned earlier.

Learner answer: B. Correct answer: B. Result: correct. Recorded2026-10-25.
Explanation: A correction overwrites the price, explicit removal clears cuisine, and unmentioned area and people values remain unchanged. State updates must distinguish missing updates from explicit clearing.
Phase05 running initial score:82/86. Lesson29 attempt1:2/2; incomplete.

### Answer history: p05-l29-code-v1

ID: p05-l29-code-v1
Phase05 — NLP — Foundations to Advanced; Lesson29 — Dialogue State Tracking.
Question87/87; lesson question3/3; code tracing.

What Joint Goal Accuracy does this code print? Dictionary equality requires every slot value to match for the turn to count as correct.

```python
gold = [
    {'area': 'north', 'price': 'cheap'},
    {'area': 'north', 'price': 'moderate'},
    {'area': 'south', 'price': 'moderate'},
    {'area': 'south', 'price': None},
]
predicted = [
    {'area': 'north', 'price': 'cheap'},
    {'area': 'north', 'price': 'cheap'},
    {'area': 'south', 'price': 'moderate'},
    {'area': 'south', 'price': 'moderate'},
]
correct = sum(p == g for p, g in zip(predicted, gold))
print(correct / len(gold))
```

A) 0.75
B) 1.0
C) 0.5
D) 0.25

Learner answer: C. Correct answer: C. Result: correct. Recorded2026-10-25.
Explanation: Only turns1 and3 match every gold slot. Turns2 and4 have incorrect price values, giving Joint Goal Accuracy2/4=0.5.
Phase05 initial assessment complete:83/87 (95.40%). Lesson29 attempt1 complete:3/3. All29 lessons meet the minimum2/3; the phase passes without retakes.

### Phase05 mastery completion — 2026-10-25

- Passed:83/87 (95.40%), exceeding required74/87; all29 lessons meet minimum2/3. No retakes required.
- All87 questions, learner answers, correct answers and explanations preserved.
- Lessons03,08,12,22 scored2/3 each; all other25 lessons scored3/3.
- Residual review: skip-gram versus CBOW direction(L03,Q7), bidirectional future-context dependence(L08,Q23), restoring source sentence order after selection(L12,Q36), row-wise MaxSim aggregation(L22,Q66).
- All29 lessons done by quiz-based mastery; implementation labs not performed in this assessment. One normal progress log entry per lesson added to LEARNING.md.
- Next: Phase06 — Speech & Audio, Lesson01, question1/51, not yet presented. No pending answer.
