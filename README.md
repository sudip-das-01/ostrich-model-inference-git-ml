# ostrich-model-inference-git-ml — Loan Default Dataset (loan_default branch)

This branch contains a trained scikit-learn classification model for **loan default prediction**. It is used as a reference repository for the Ostrich `git` inference type.

## Repository Structure

```
.
├── dataset/
│   └── input.csv          # Input features (no target column)
├── model/
│   └── model.pkl          # Trained scikit-learn classifier (pickle)
├── inference.py           # Inference entrypoint
├── schema.json            # Required input feature column names
├── requirements.txt       # Python dependencies
└── Dockerfile             # Container definition
```

## Input Features

Defined in `schema.json` under `input_parameters_name` (33 features):

| Feature | Description |
|---|---|
| `ID` | Unique loan application identifier |
| `year` | Application year |
| `loan_limit` | Loan limit category |
| `Gender` | Applicant gender |
| `approv_in_adv` | Pre-approval status |
| `loan_type` | Type of loan |
| `loan_purpose` | Purpose of the loan |
| `Credit_Worthiness` | Credit worthiness indicator |
| `open_credit` | Open credit lines |
| `business_or_commercial` | Business/commercial flag |
| `loan_amount` | Requested loan amount |
| `rate_of_interest` | Interest rate |
| `Interest_rate_spread` | Spread over benchmark rate |
| `Upfront_charges` | Upfront fees |
| `term` | Loan term (months) |
| `Neg_ammortization` | Negative amortisation flag |
| `interest_only` | Interest-only flag |
| `lump_sum_payment` | Lump sum payment flag |
| `property_value` | Collateral property value |
| `construction_type` | Property construction type |
| `occupancy_type` | Occupancy type |
| `Secured_by` | Security type |
| `total_units` | Number of units |
| `income` | Applicant income |
| `credit_type` | Credit scoring model used |
| `Credit_Score` | Applicant credit score |
| `co-applicant_credit_type` | Co-applicant credit type |
| `age` | Applicant age band |
| `submission_of_application` | Application submission channel |
| `LTV` | Loan-to-value ratio |
| `Region` | Geographic region |
| `Security_Type` | Security classification |
| `dtir1` | Debt-to-income ratio |

## Output

Running inference produces `output/output.csv` with a single `target` column containing predicted default labels (1 = default, 0 = no default).

## Running Locally

```bash
pip install -r requirements.txt
python inference.py
# output written to output/output.csv
```

## Running with Ostrich git Inference Generator

The Ostrich inference generator can generate an `inference.py` that clones this branch to a temp directory, reads `dataset/input.csv`, validates all 33 features via `schema.json`, runs predictions, and pushes `output/output.csv` back:

```bash
python inference_py_generator.py \
  --payload-json sample_payload_git.json \
  --repo-type git
```

Pass `"branch": "loan_default"` in the `git_config` section of the payload, or override at runtime with `--branch loan_default`.
