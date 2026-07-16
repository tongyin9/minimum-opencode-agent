# AI False Report — July 16, 2026

## Model
DeepSeek V4 Pro, max mode

## Task
Create gene symbol - ENSG mapping file

## Three Silent Errors in One Task

- **`fill=TRUE`**: added as "insurance" — would silently pad misaligned rows, shifting ENSG IDs into the symbol column with no error
- **Single quote `'` parser bug**: R's default quote handling dropped 17,741 rows (42%) silently when gene symbols like `hnRNPH'` appeared in data
- **Monolithic design**: all transforms in one script — no way to see the 42% loss without rewriting the whole thing

## Why the Rules Caught Them

- **Rule #7** (No Hypothetical Error Handling): blocked `fill=TRUE` — don't write defense for problems you haven't proven exist
- **Rule #6** (Verify Every State Change): row counts printed at each step — the 42% drop becomes visible immediately
- **Rule #13** (The Data Artifact Is the Contract): four scripts producing four observable files — file sizes, row counts, and column counts are all independently verifiable

## What Happens Without Rules

The AI operates on its own defaults:

1. Every script is write-and-pray — no error will surface
2. Every output file "looks right" — right size, exists on disk, downstream scripts run
3. Plots are generated, statistics computed, p-values produced
4. **No alarm fires. No crash. No error log.**

## Real-World Consequence

A bioinformatics pipeline produces answers that enter clinical decision-making. If 42% of gene mappings are silently missing, differential expression, pathway scoring, and biomarker discovery are all wrong. The paper gets published with fabricated-looking statistics — not from fraud, but from silent data corruption. Peer review cannot catch pipeline bugs. The first sign of failure is unreproducible results. In clinical genomics, unreproducible results mean wrong treatment. Wrong treatment means patient harm.

## The Rules Are the Circuit Breaker

They don't make the AI smarter. They make it *auditable*. Every transformation writes a file. Every file can be opened and checked. If a number doesn't match, the chain stops — before the error propagates into anyone's publication, grant, or patient.

---

## Reflection

I cannot imagine how many false results have been generated in the past two years.

People are handing their data to AI — data they do not fully understand, asking questions they do not know how to verify, using a tool whose failure modes they have never seen. They trust AI because they don't know it well; they trust AI can do a basic job, which sounds simple, because they don't know the job well. The code runs,  the plots are beautiful, and the p-values are significant. They do not know errors happen and are hidden from the beginning. 

This is not a technical problem. It is a problem of **asymmetric knowledge**. The AI does not know it is wrong. The researcher does not know the domain deeply enough to catch it. Between them, there is no one. No reviewer can see the bug. No editor can replicate the analysis. The paper is accepted. The grant is funded. The clinical trial recruits patients. The therapy fails. Nobody traces it back to a single quote character in a TSV parser.

Three errors in one afternoon. One task. Multiply this by every AI-assisted analysis in every lab that has no bioinformatician reviewing the intermediates. That is not a troubleshooting file. That is an entire literature — published, cited, built upon — resting on outputs that were never verified by anyone who could recognize a silent 42% loss.

Only the person who knows both sides can prevent this. The person who understands what the data should look like, and also understands that the AI has no conscience, no suspicion, no instinct that something is wrong. The AI will hand you a perfect-looking file with a smile and no warning. It is not malicious. It simply does not know what truth looks like.

The rules are not about controlling the tool. They are about placing a human — the one human who can see — between every step. Not because the AI is dangerous. Because the gap between what the AI produces and what people believe it produced is exactly the width of a patient's life.
