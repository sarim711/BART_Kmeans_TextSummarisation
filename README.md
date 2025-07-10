# Medical Text Summarization

## Overview
This project develops a text summarization system for medical notes, leveraging a combination of **statistical methods**, **BART** (a transformer-based model), and **KMeans clustering with BERT embeddings**. The goal is to generate concise summaries that capture critical information from clinical documentation, such as patient conditions and care plans, to assist healthcare professionals. The entire project was executed in Google Colab and processes a dataset of 20,000 medical notes.

**Key Features:**
- Text cleaning and preprocessing pipeline
- Statistical summarization using word frequency-based sentence scoring
- Abstractive summarization with BART
- Sentence clustering with KMeans and BERT embeddings
- Progress tracking with `tqdm` for large datasets
- GPU-accelerated processing in Google Colab

## Dataset
**Medical Notes Dataset (`mg_small.csv`)**  
- **Description**: Contains 20,000 medical notes, primarily nursing progress notes, documenting patient details such as respiratory status, feeding/nutrition, parenting interactions, and developmental observations.
- **Columns**:
  - `text`: Raw medical note text
- **Dataset Statistics**:
  - 20,000 records
  - No predefined train/validation/test split (processed as a whole for summarization)
- **Format**: CSV

## Text Preprocessing
The preprocessing pipeline ensures the text is clean and suitable for summarization:
- **Regex-based Cleaning**:
  - Removes non-alphanumeric characters (except periods and spaces)
  - Normalizes multiple spaces to a single space
  - Ensures proper sentence separation with periods and single spaces
- **Custom Cleaning Function**: Applied across all notes for consistency

## Approaches Used
### 1. Statistical Approach (Word Frequency-based)
- **Description**: Extracts key sentences based on word frequency scoring.
- **Implementation**:
  - Tokenizes text and calculates normalized word frequencies
  - Scores sentences by summing word frequencies, normalized by sentence length (for sentences >5 words)
  - Selects the top-3 sentences as the summary

### 2. BART (Transformers)
- **Description**: Uses a pre-trained BART model for abstractive summarization, producing fluent and concise summaries.
- **Implementation**:
  - Leverages Hugging Face's `transformers` library to load BART
  - Tokenizes input text and generates summaries

### 3. KMeans with BERT
- **Description**: Clusters sentences based on semantic similarity using BERT embeddings and KMeans, identifying key themes or representative content.
- **Implementation**:
  - Embeds sentences using BERT
  - Applies KMeans clustering to group embeddings

## Evaluation
- **Metrics**: No quantitative metrics (e.g., ROUGE) were used due to the lack of reference summaries.
- **Qualitative Evaluation**: Summaries were evaluated for relevance, coherence, and informativeness.
- - **Processing Time**: The statistical approach processed 20,000 notes in ~12 seconds on Google Colab.
- **Key Results**:
  - Statistical summaries are quick and lightweight, effectively highlight patient status and interventions but lack coherence and completeness.
  - BART produces most coherent and detailed summaries but more processing time is required.
  - Domain specific BERT embeddings with KMeans clustering reveals semantically rich summaries but lack slight coherence.Balanced quality and processing time


## Installation
This project runs entirely in **Google Colab**, requiring no local setup. All dependencies are installed within the Colab environment.

**Steps**:
1. Open the Text_Summarisation.ipynb notebook in Google Colab using this badge: [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/sarim711/BART_Kmeans_TextSummarisation/blob/main/Text_Summarisation.ipynb)
2. Upload the `mg_small.csv` dataset to your Colab session.
3. Run all notebook cells to install dependencies and execute the pipeline.

## Future Work
- Experiment with advanced models like T5 or Pegasus for summarization.
- Implement quantitative metrics (e.g., ROUGE) if reference summaries become available.
- Enhance the statistical approach with weights for medical terminology.
- Optimize for larger datasets using parallel processing.

## License
This project is licensed under the MIT License.
