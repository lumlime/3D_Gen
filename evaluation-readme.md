# RAG Evaluation System for 3D Shape Generation

This evaluation system tests the effectiveness of Retrieval-Augmented Generation (RAG) in improving code generation for 3D printable models.

## Overview

The evaluation system consists of:

1. **Primary Evaluation**: Tests DeepSeek model with different conditions (baseline, RAG only, review only, full system)
2. **Statistical Analysis**: Simple, clear analysis of results including time metrics
3. **STL Analyzer**: Tool for measuring dimensions of generated 3D models

## Setup

### Prerequisites

```bash
pip install openai numpy pandas matplotlib seaborn scipy sentence-transformers faiss-cpu beautifulsoup4 requests
```

```bash
pip install openai==0.28 requests==2.32.3 beautifulsoup4==4.13.4 sentence-transformers==4.1.0 faiss-cpu==1.10.0 trimesh==4.6.8 numpy==2.2.5 numpy-stl==3.2.0 pyglet==2.15 manifold3d==3.0.1 shapely==2.1.0 pandas==2.2.3 matplotlib==3.10.1 seaborn==0.13.2
```

### Required Files

1. Your original script with embeddings:
   - `tri_docs_embeddings.npy` and `tri_docs_chunks.pkl`
   - `numpy_stl_embeddings.npy` and `numpy_stl_chunks.pkl`
   - `tri_custom_embeddings.npy` and `tri_custom_chunks.pkl`
   - `best_embeddings.npy` and `best_chunks.pkl`

2. The evaluation scripts:
   - `rag_evaluation_system.py`
   - `statistical_analysis.py`
   - `run_evaluation.py`
   - `check_context_files.py`
   - `stl_analyzer.py`

### Checking Context Files

Before running the evaluation, check that all required context files are present:

```bash
python check_context_files.py
```

This will verify all necessary embeddings and chunks files are available.

## Usage

### 1. Run the Evaluation System

```bash
python run_evaluation.py
```

### 2. Select an Option:

The simplified evaluation system offers three options:

1. **Run primary evaluation (DeepSeek)** - Runs the full evaluation with the DeepSeek-V3 model, testing all conditions:
   - Creates STL files for successful generations
   - Measures success rates, execution times, and iterations
   - Generates statistical analysis and visualizations
   - Creates a dashboard of results

2. **Analyze existing results** - Analyzes results from a previous evaluation run:
   - Generates statistical summaries
   - Creates visualizations
   - Produces simple reports

3. **Run STL analyzer** - Launches the STL analyzer tool:
   - Measures dimensions of STL files
   - Compares to expected dimensions
   - Visualizes 3D models

### 3. Configuration

Edit `run_evaluation.py` to set your API key:

```python
DEEPSEEK_API_KEY = "your-api-key-here"
```

### 4. Test Parameters

Default settings:
- 5 shapes (box, cylinder, cone, sphere, pyramid)
- 10 runs per shape for primary evaluation
- 4 conditions tested (baseline, RAG only, review only, full system)

## Output Files

The system creates a timestamped results directory containing:

1. **Raw Data**:
   - `results.csv`: All test results
   - `raw_results.json`: Detailed test data

2. **Analysis**:
   - `simple_report.txt`: Easy-to-understand summary
   - `summary.txt`: Statistical summary

3. **Visualizations**:
   - `dashboard.html`: Interactive results dashboard
   - Various charts including time analysis charts

4. **Generated Files**:
   - STL files for successful generations
   - Python code files for each test

## Evaluation Metrics

1. **Success Rate**: Percentage of tests that generate valid STL files
2. **Iterations**: Number of attempts needed for success
3. **Execution Time**: Time taken from prompt to successful completion
4. **Statistical Significance**: T-test results and effect size (Cohen's d)

## Understanding Results

The system provides several ways to understand your results:

1. **Simple Report**: Summary of findings
2. **Dashboard**: Visual overview of all results including time metrics
3. **Statistical Analysis**: Basic statistics

Key questions answered:
- Does RAG improve code generation?
- Which shapes are hardest to generate?
- How does RAG impact execution time?
- Is the difference statistically significant?

## STL Analyzer

The STL analyzer tool provides detailed measurements of generated 3D models:

1. **Dimensional Analysis**: Measures width, length, and depth
2. **Comparison**: Compares actual dimensions to expected dimensions
3. **Visualization**: Displays 3D models with measurements
4. **Batch Analysis**: Can analyze multiple STL files


## Troubleshooting

1. **Missing context files**: Ensure all embedding files are in the same directory
2. **API errors**: Check your API key and internet connection
3. **Code execution errors**: Ensure trimesh and numpy-stl are installed
