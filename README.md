# Causal Information Extraction Using Large Language Models

This repository contains the code, datasets, and results for the bachelor's thesis "Causal Information Extraction Using Large Language Models". The research investigates the ability of state-of-the-art large language models to extract cause-effect pairs from text and evaluates their performance across various challenging scenarios.

## Project Overview

This project evaluates eight flagship large language models from leading AI organizations on their causal information extraction capabilities. The study employs a purpose-designed multi-domain dataset with controlled causal relations embedded in contexts of varying complexity. A comprehensive evaluation framework combines both human assessment and model-based semantic scoring to provide detailed insights into model performance.

## Repository Structure

- **`/auto`**: Core automation scripts
  - `run_llms.py`: Script for running extraction tests across multiple LLMs
  - `judge_llm_extractions.py`: Evaluation script for LLM-as-judge assessment

- **`/datasets`**: Contains the test datasets and dataset generation utilities
  - `/dataset-hard`: Four dataset variants with increasing difficulty:
    - Base dataset (`dataset.csv`)
    - Masked variant with neutralized causal cues (`dataset_masked.csv`)
    - Shuffled variant with reassigned pairs (`dataset-shuffled.csv`)
    - Combined masked-shuffled variant (`dataset-shuffled-masked.csv`)
  - Domain-specific cause-effect pairs (`econ-finance-pairs.txt`, `env-climate-pairs.txt`, `tech-cs-pairs.txt`)
  - Dataset transformation scripts:
    - `mask_causal_cues_friendly.py`: Neutralizes explicit causal indicators
    - `shuffle_pairs_by_domain.py`: Reassigns cause-effect pairs

- **`/charts`**: Generated visualizations of model performance
  - Cross-dataset performance comparisons
  - Cause vs. effect extraction metrics
  - Precision, recall, and F1 score charts

- **`/runs`**: Raw extraction results across all datasets and models
  - Organized by dataset variant and model
  - Both CSV and JSONL formats for all results

- **`/result-summary`**: Processed results and performance metrics
  - `/f1-metrics`: Precision, recall, and F1 scores
  - `/human-eval`: Human evaluation results and summaries

## Models Evaluated

- OpenAI GPT-o3
- Anthropic Claude 3.7 Sonnet
- xAI Grok-3
- Google Gemini 2.5 Pro
- Meta Llama 4 Maverick
- DeepSeek-R1
- Mistral-Small-3-24B-Instruct
- Qwen3-30B-A3B

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/koodikirjutaja/CIE.git
   cd CIE
   ```

2. Set up a Python virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Running Extraction Tests

To run the extraction pipeline on a specific dataset with all models:

```bash
python auto/run_llms.py --dataset datasets/dataset-hard/dataset.csv --output runs/custom-run
```

### Evaluating Extractions

To evaluate model extractions using the LLM-as-judge approach:

```bash
python auto/judge_llm_extractions.py --input runs/custom-run --output runs/grades/custom-grades
```

### Generating Summary Metrics

To calculate F1 metrics from the evaluation results:

```bash
python calculate_f1_metrics.py --input runs/grades/custom-grades --output result-summary/f1-metrics/custom_metrics.csv
```

### Visualizing Results

To generate charts from the evaluation results:

```bash
python generate_charts.py --metrics result-summary/f1-metrics/custom_metrics.csv --output charts/custom_charts
```

## Dataset Construction

The datasets were constructed through a multi-step process:
1. Generation of domain-specific cause-effect pairs
2. Embedding pairs into coherent paragraphs without explicit causal markers
3. Applying transformations to test model resilience:
   - Masking causal cues to test reliance on linguistic markers
   - Shuffling pairs to test dependence on pre-trained associations

## Evaluation Framework

The evaluation uses a twin assessment approach:
1. **Human Evaluation**: Human assessment of extraction quality using a three-point scale
2. **LLM-as-Judge**: Automated evaluation where LLMs score other models' extractions

Performance is measured using:
- Semantic similarity scores (0-1)
- Traditional metrics (precision, recall, F1)
- Cross-dataset resilience

## Key Findings

- Modern LLMs demonstrate strong capability in extracting causal information
- Leading models (GPT-o3, Claude 3.7 Sonnet, Grok-3) consistently outperform smaller models
- Models show semantic understanding beyond reliance on explicit linguistic markers
- Performance correlation with general knowledge benchmarks (GPQA) suggests transferable reasoning capabilities


## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Keywords

**Võtmesõnad (Estonian):**
- Põhjuslik informatsiooni ekstraheerimine
- Suured keelemudelid
- Loomuliku keele töötlus
- Tehisintellekt
- Nullõppe hindamine

**Keywords (English):**
- Causal information extraction
- Large language models
- Natural language processing
- Artificial intelligence
- Zero-shot evaluation

## CERCS Code
**CERCS:** P176 Tehisintellekt (Artificial Intelligence)
