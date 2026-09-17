# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
Our 23 documents are informal student advice threads where critical answers often appear in single-sentence replies rather than thread titles. While standard questions should match well, setting the threshold to 4 rather than 5 accounts for the difficulty of retrieving short, dense details (such as a single "$20" or "12-minute" mention) that might score lower against broader conversational embeddings.

---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
Every ingested chunk originates from a distinct, named .txt file representing a specific advice thread. Because our retrieval pipeline automatically attaches file metadata to every retrieved chunk, any answer generated from retrieved context will have access to a source document unless the retrieval step fails completely.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.


**Why this target:**
The corpus is strictly bounded to 23 student-life advice topics, so out-of-scope questions (such as campus dining hours or local politics) should have noticeable semantic separation. Aiming for 4 of 5 reflects the expectation that most unrelated queries will be stopped by the distance threshold, while leaving a realistic margin for borderline embedding matches before exact cutoffs are calibrated.

---

## 4. Something about your chunks

When 5 random chunks are inspected, at least 4 of 5 must contain both the thread title line (THREAD: ...) and at least one full reply (--- reply ... --- followed by complete sentences) without text being cut off mid-sentence at either boundary.



**Why this target:**
Our average chunk size is 487 characters, which is large enough to contain an entire short thread, but our minimum was only 2 characters. Setting a 4-of-5 target accounts for occasional structural edge cases (like trailing lines or isolated vote tallies) while ensuring an evaluator can easily verify that the vast majority of chunks hold standalone conversational context.


---

## 5. Your choice

For at least 4 of my 5 test questions, the generated response must explicitly contain the exact string defined in that question's expects field in questions.py (e.g., "$20", "16GB", "February and March").



**Why this target:**
An advice tool is only useful if it delivers the specific numeric and temporal facts students need. Evaluating against the exact expects field provides an automated, binary pass/fail test that removes subjectivity and verifies the generator extracts target entities rather than returning vague summaries.


---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
