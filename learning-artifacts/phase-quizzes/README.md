# Comprehensive quiz recording protocol

Learner preferences: Phase00–13 inclusive, every lesson covered, English questions, one question at a time, normal done/todo progress. Preserve these preferences when resuming in a new conversation.

## Minimal resume reads

1. Read `active.json` first. It is the authoritative quiz cursor and pending-question pointer/content.
2. If no question is pending, read the active lesson's full `docs/en.md` once before preparing its questions. Use the active phase's `progress.md` only when lesson scores/checklist context is needed.
3. Do not routinely load completed phase histories, the global lesson checklist, all review notes, or all of LEARNING.md. `progress.md` here is the phase index; each `phase-NN/` owns its own records.
4. Old questions, corrections, and remediation are in `phase-NN/history.md`; use targeted ID lookup and a bounded read only when needed. Review notes are in `phase-NN/review.md`.

## Lesson question preparation

- Read each full lesson once per set, checking toy code behavior rather than repeating inaccurate prose. Prepare three concise original scored questions: concept, application, code tracing/debugging. Keep distractors plausible and comparable in length.
- Optionally save the three questions with source path/hash and private answer keys in `phase-NN/current-lesson.json`. This is the `lesson_cache` pointer in active.json. It is private tutor data: do not print its answer keys, bulk-read it into user-facing output, or expose future answers. Read only the current question's fields as needed. Reuse the lesson understanding between its three turns; reread only for uncertainty or source change.
- Put only the question actually presented in `active.json.pending_question` (ID, text, options). Keep its grading key in the private lesson cache. Never advance until the learner answers. Do not create a pending question at a phase boundary until it is presented.
- Use exactly `Reply with one letter: <A|B|C|D>.` Keep English feedback brief for correct answers; explain missed concepts briefly. Do not add unscored reviews unless requested. Default retakes remain scored full three-question sets.

## Writes on an answer

- Grade only the pending question. Append its exact question/options, learner response, correct answer, result, and explanation once to the active phase's history. Record revisions/invalid input without double scoring. Never rewrite the full archive to append a turn.
- Update the small active.json cursor, running score, and pending question. Completed phase records stay untouched.
- Update the active phase lesson checklist on lesson completion; partial scores/cursor live in active.json. Update the global index and LEARNING.md at lesson/phase boundaries or pauses rather than duplicating every-question counters in three places. On resume, active.json takes precedence over older summary checkpoints.
- If using a lesson cache, retain the completed set in the phase archive or a durable question file before clearing/replacing the cache; no answer history is discarded.

## Scores and completion

- Pass the phase at ≥85% overall AND every lesson ≥2/3. A complete fresh retake replaces that lesson's effective score even if worse. Incomplete sets do not change effective scores. Preserve all initial and retake evidence. Phase01's historical targeted-correction exception is restricted to Phase01.
- Before phase pass, all lesson status rows stay todo. At pass, mark every phase lesson done, mark LEARNING.md Path Done, record initial/effective/cumulative scores, and retain missed topics for later review.
- Add one normal dated per-lesson progress row to `phase-NN/progress.md`, with quiz-based mastery credit and explicit `implementation lab not performed in this assessment`. LEARNING.md's Progress log links to these phase logs; avoid duplicating the full rows there.
- At phase boundary, save the next phase/lesson cursor with no pending question. Do not imply implementation labs ran. Never alter reference lessons or ROADMAP.md to record personal progress.

## Fresh conversations

A new conversation at a phase boundary can avoid carrying the entire previous quiz transcript. The learner can say: "Continue the comprehensive quiz from learning-artifacts/phase-quizzes/active.json; follow its README.md." This changes neither scores nor coverage. File splitting reduces future file reads; it does not remove text already present in the current conversation.
