# SemEval 2027 Task 2 – DiCo-NLI
## Track 1 – English

This fork contains my individual work for SemEval 2027 Task 2 (DiCo-NLI), Track 1.

The original task repository, datasets, evaluation scripts, and official documentation were provided by the task organizers. My own experiments, notebooks, submissions, and results are documented here.

## Current progress

### 1. Data exploration
Notebook: `notebooks/01_data_exploration.ipynb`

Completed:
- Loaded and inspected the Track 1 training and development datasets
- Examined dataset columns and label distribution
- Investigated `pair_id`, original/flipped pairs, and reversible relations
- Studied the four labels:
  - `EQUIVALENCE`
  - `FORWARD_ENTAILMENT`
  - `BACKWARD_ENTAILMENT`
  - `NEGATIVE_OTHER`
- Examined the relationship between reversed phrase pairs and consistency

### 2. Majority baseline
Notebook: `notebooks/02_majority_baseline.ipynb`

Baseline strategy:
- Predict `FORWARD_ENTAILMENT` for every development instance

Development results:
- Weighted F1: `0.1286987522`
- SoftCons: `0.0`
- HardCons: `0.0`

The local official scorer and the Codabench Development submission produced the same scores.

### 3. First Codabench submission
Track: Track 1 – English

The first development submission was successfully accepted by Codabench.

This submission was used primarily to verify:
- prediction file format
- ZIP packaging
- instance IDs
- label formatting
- agreement between local and Codabench evaluation

## Next steps

- Build stronger baselines
- Learn the transformer/NLI training pipeline
- Fine-tune a pretrained language model
- Evaluate on the development set
- Perform error analysis
- Improve directional consistency
- Submit improved systems to Codabench


### 4. Lexical baseline

Notebook: `notebooks/03_lexical_baseline.ipynb`

Approach:
- Used simple lexical containment features based on word sets
- Predicted `FORWARD_ENTAILMENT` when all words in `text2` were contained in `text1`
- Predicted `BACKWARD_ENTAILMENT` for the reverse case
- Predicted `EQUIVALENCE` when both word sets were identical or when neither subset rule applied

Development results:
- Weighted F1: `0.4592277663`
- SoftCons: `1.0`
- HardCons: `0.5812274368`

The local scorer and Codabench Development submission produced the same scores.

Main observations:
- High precision for directional entailment predictions
- Perfect directional consistency on reversible pairs
- `NEGATIVE_OTHER` was never predicted, so its F1 remained `0`
- The fallback to `EQUIVALENCE` caused many false positives