# Midterm 1: answers

GitHub username:aruzhanusserbai
Session code:zebra-28
Fingerprint:9c58e91a

> Fill in the three lines above from `my_data/DATA.md`. Do not rename headings or table columns: a script reads the numbers.
> Write only in the empty cells and lines. Percentages as 0.78 or 78 %, money as plain numbers.

## AI-use declaration

I used ChatGPT to calculate recall@k, MRR@10, Wilson confidence intervals, annual costs and per-language results. It also helped calculate the numerical answers in Part 3. The calculations used the synthetic values supplied in my generated exam files.
ChatGPT was also used to explain the metrics and formulas through examples, including how retrieval ranks determine recall and how the position of the correct chunk affects MRR. It also helped interpret uncertainty, compare costs against the budget, and identify differences between language groups.
ChatGPT also helped draft the written sections, which I discussed and revised to reflect my final choices and understanding.
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

Chosen candidate: A, k=3

(Decision, using your intervals and the budget. Give the recall of your choice for EN, RU and KK separately.)

I recommend A, k=3 because its annual cost of $9,810.88 fits the $11,700 budget and it achieved the highest observed recall among the affordable candidates: 71.67%. I consider the additional cost worthwhile because it also achieved higher recall in each language than the other affordable options.

Its 95% Wilson interval is 59.23–81.49%. B, k=5 had lower observed recall and a slightly wider interval, but the intervals overlap, so these results do not establish that A, k=3 is truly better.
A, k=3 also outperforms B, k=3 under the course rule because their intervals do not overlap.
For A, k=3, recall was 85% for EN, 65% for RU and 65% for KK. Russian and Kazakh were therefore the worst-served languages, although their observed results were higher than under the other affordable candidates.
### 1e. Next measurement (at most 60 words)

Run A, k=3 and B, k=5 on the same 600 new questions, with 200 per language. Blind-score grounded answer correctness and report per-language Wilson intervals. If the cheaper B, k=5 matches A's answer quality, especially for RU and KK, choose B. A clear A advantage would justify its additional cost.

## Part 2: A document pipeline you can defend

### 2a. Numbers

| pipeline | overall accuracy | weakest cell (language, condition) | accuracy there | lower | upper | annual cost |
|---|---|---|---|---|---|---|
| H |0.872222 |RU, degraded; KK, degraded (tie) |0.800000 | 0.626940|0.904950 |7539.08 |
| L |0.788889 |KK, degraded |0.700000 |0.521239 |0.833354 |7200.00 |

Personal-data pages per year sent abroad under H:87600

### 2b. Memo (at most 300 words)
To: Head of Operations

I recommend L because the scans contain personal data, and we do not know enough about how H stores it abroad. I would require human verification before using extracted fields for financial actions.

H achieved 87.22% accuracy, compared with L’s 78.89%. H’s weakest groups were degraded RU and KK scans, both at 80% (95% Wilson interval: 62.69–90.50%). L’s weakest group was degraded KK at 70% (52.12–83.34%). Overall accuracy hides these weaker results. Each group contained only 30 documents, so the intervals are wide and overlap; this comparison does not establish a clear difference between the weakest groups.

H costs $7,539.08 annually, while L costs $7,200. One L server can handle 6,000 pages daily, enough for the 3,000-page workload. Human review would add costs.

H sends scans to a foreign data centre, including 87,600 pages with names and ИИН annually. The information provided does not explain who stores them, who can access them or how long they remain, including in backups. These details would require verification and a compliance review. A vendor’s statement alone would not be enough.

L processes scans on the bank’s server in Kazakhstan. However, we still need to check administrator access, storage and backup locations, retention periods and whether telemetry sends data elsewhere. Local processing alone does not guarantee compliance.

I would require encryption, access limited by role, access logs and rules keeping personal data out of diagnostic logs. Network logs should confirm outbound restrictions, and deletion checks should verify retention rules, including backup expiry.

I accept L’s lower observed accuracy in exchange for local processing. Remaining risks include extraction errors, especially on degraded KK scans, internal misuse and mistakes during human review.

## Part 3: Explain your own numbers

### Q1

Number: 1.21 (KK/EN characters = 1.1752; bytes = 2.3025; tokens = 2.7966; token ratio / byte ratio = 1.2146).
Why (at most 40 words): The value 1.21 shows that the token increase is not explained by UTF-8 byte size alone. The tokenizer also contributes by splitting the Kazakh text into finer pieces.
### Q2

Number: 13.5 %
Why (at most 40 words): Only English is truncated because its estimated length exceeds the 512-token limit. Russian and Kazakh fit. The cut part may contain important information, which will not be represented in the embedding and could affect retrieval.

### Q3

Number: 66.5 %
Why (at most 40 words): Top-p excludes low-probability tokens from the selection pool. Lowering temperature makes high-probability tokens more likely, but does not itself exclude the other tokens.

### Q4

Number: 27.6 % (weighted bound: (193 × 0.30 + 295 × 0.26) / 488).
Why (at most 40 words): I excluded arithmetic sequences and multiplication because rules allow generalisation to new examples. Account numbers and birthdays require specific facts. The instruction “never invent a fact” does not provide missing information, so it does not change the bound.

### Q5

Number: 45878
Why (at most 40 words): The first message is paid for 28 times because it is resent as part of the history on every turn. Prompt caching can reduce the cost of repeated input, but does not make it free.
