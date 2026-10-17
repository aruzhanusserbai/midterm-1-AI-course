# Midterm 1: answers

GitHub username:aruzhanusserbai
Session code:zebra-28
Fingerprint:9c58e91a

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

(About half a page: which assistants or tools you used and for what. If you used none, say so.)

I used ChatGPT to calculate recall@k, MRR@10, Wilson confidence intervals, annual costs and per-language results. It also helped calculate the numerical answers in Part 3. The calculations used the synthetic values supplied in my generated exam files.

I used ChatGPT to explain the metrics and formulas through examples, including how retrieval ranks determine recall and how the position of the correct chunk affects MRR. It also helped interpret uncertainty, compare costs against the budget, and identify differences between language groups.

For the written sections, I made the final decisions and developed my own arguments. I used ChatGPT to correct grammatical errors and help express my thoughts clearly in English within the word limits.

## Part 1: Retrieval and cost decision

### 1a. Metrics (all 60 questions)

| config | recall@1 | recall@3 | recall@5 | MRR@10 |
|---|---|---|---|---|
| A |0.500000 |0.716667 |0.750000 | 0.598677|
| B |0.283333 |0.416667 | 0.633333| 0.388214|

### 1b. Recall and 95 % Wilson interval of each candidate (recall at its own k)

| candidate | recall@k | lower | upper |
|---|---|---|---|
| A, k=3 |0.716667 | 0.592325| 0.814933|
| A, k=5 | 0.750000| 0.627677| 0.842236|
| B, k=3 |0.416667 |0.300641 |0.542721 |
| B, k=5 |0.633333 |0.506828 | 0.743793|

### 1c. Annual model cost in USD

| candidate | annual cost |
|---|---|
| A, k=3 | 9810.88|
| A, k=5 |13496.97 |
| B, k=3 |5801.75 |
| B, k=5 |6815.09 |

### 1d. Decision (at most 150 words)

Chosen candidate:

(Decision, using your intervals and the budget. Give the recall of your choice for EN, RU and KK separately.)

I recommend A, k=3: annual model cost is $9,810.88, below the $11,700 budget, with recall 43/60 = 71.67% (95% Wilson interval 59.23–81.49%). A, k=5 exceeds the budget. Both A candidates have intervals above B, k=3's 30.06–54.27%, without overlap, supporting higher recall under the course rule. However, A, k=3 overlaps B, k=5 (50.68–74.38%); this sample does not establish a winner between them. The two A intervals also overlap. I choose the highest observed recall within budget, accepting higher cost than B, k=5. For my choice, EN recall is 17/20 = 85%, RU is 13/20 = 65%, and KK is 13/20 = 65%. RU and KK are jointly worst served; the overall recall hides this gap. Retrieval recall measures finding the correct chunk, not final answer correctness.

### 1e. Next measurement (at most 60 words)

Run A, k=3 and B, k=5 on the same 600 new questions, with 200 per language. Blind-score grounded answer correctness and report per-language Wilson intervals. If the cheaper B, k=5 matches A's answer quality, especially for RU and KK, choose B; a clear A advantage would justify its additional cost.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H |0.872222 |RU, degraded; KK, degraded (tie) |0.800000 | 0.626940|0.904950 |7539.08 |
| L |0.788889 |KK, degraded |0.700000 |0.521239 |0.833354 |7200.00 |

Personal-data pages per year sent abroad under H:87600

### 2b. Memo (at most 300 words)
To: Head of Operations
Choose L, with human verification before extracted fields trigger financial actions. H scores 157/180 = 87.22% overall; L scores 142/180 = 78.89%. H's weakest cells are degraded RU and KK, both 24/30 = 80% (95% Wilson 62.69–90.50%). L's weakest is degraded KK, 21/30 = 70% (52.12–83.34%). Overall accuracy hides these weaker groups. Small cells give wide, overlapping intervals, so the observed weakest groups are not proven uniquely worse, nor is H proven better in the weakest-cell comparison.
H costs $7,539.08 annually; L costs $7,200 for one server, whose 6,000-page daily capacity exceeds the 3,000-page workload. These estimates exclude human review and additional operational costs.
For H: where does the scan go? A foreign data centre, including 87,600 pages annually containing names and ИИН. Who stores it, and for how long? The supplied data does not say. Establish vendor/subprocessor access, storage and backup locations, retention, deletion and training use before considering deployment. An ИИН is covered by Kazakhstan's personal-data law; a vendor assurance alone is not a compliance review.
For L: inference runs on the bank's server in Kazakhstan. Verify who administers scans, whether logs, telemetry or backups copy them elsewhere, and actual retention. Local inference alone does not settle compliance.
Require documented compliance review, role-based access with audit logs, encryption, outbound-network restrictions tested using traffic logs, and an approved retention schedule tested by deletion and backup-expiry checks. Keep names and ИИН out of diagnostic logs. Audit errors by language and scan condition.
L avoids the stated foreign API transfer and costs less, but has lower observed extraction accuracy. Residual risks include incorrect fields, especially degraded KK, internal misuse and unverified backup handling. Human review mitigates errors but adds workload and cost.

## Part 3: Explain your own numbers

### Q1

Number:
Why (at most 40 words):

### Q2

Number:
Why (at most 40 words):

### Q3

Number:
Why (at most 40 words):

### Q4

Number:
Why (at most 40 words):

### Q5

Number:
Why (at most 40 words):
