# 📘 Impact of Financial Stability on Mental Health

*A data-driven analysis using Reddit (r/mentalhealth) posts*

This repository contains all code, models, and exploratory notebooks used in the project **Exploring the Impact of Financial Stability on Mental Health through Reddit Data**. The study examines how financial stress shows up emotionally in a large mental-health community and uses a fine-tuned emotion model (MentalBERT + GoEmotions) to compare finance-related and non-finance posts.

The repo is organised as a step-by-step workflow so anyone can follow the full pipeline from raw data cleaning to emotion modelling, analysis, and topic exploration.

---

## 🗂 Repository Structure

### **01_data_cleaning_and_finance_classification.ipynb**

Cleans the Pushshift r/mentalhealth data, prepares text, merges title + body, creates time fields, and applies the DistilBART-MNLI zero-shot classifier to label posts as *finance* or *non-finance*.

### **02_emotion_model_training_mentalbert.ipynb**

Fine-tunes the **MentalBERT** model on the **GoEmotions** dataset for multi-label emotion classification (27 emotions + neutral).
Includes tokenisation, batching, training loop, loss curves, and model checkpoint saving.

### **06_model_apply_full_dataset.ipynb**

Loads the trained MentalBERT checkpoint and applies it to the **entire cleaned dataset**.
Produces per-post emotion scores and saves them (e.g. as CSV) for downstream analysis. This notebook should be run **before** any analysis notebooks.

### **03_analysis_all_27_emotions_exploration.ipynb**

Early exploratory analysis using all 27 emotions.
Shows why the fine-grained labels were too sparse and why the project shifted toward basic-emotion grouping.

### **04_main_emotion_analysis_basic_emotions.ipynb**

The core analysis notebook:

* Uses the saved emotion scores from notebook 06
* Maps model output to 6 basic emotions + polarity
* Compares finance vs non-finance emotional patterns
* Runs chi-square tests
* Generates descriptive plots and temporal trends

### **05_topic_modelling_bertopic_finance_posts.ipynb**

Runs BERTopic on the cleaned finance-related subset to uncover common stressors (housing, therapy costs, work instability, etc).
Includes text cleaning, embedding, clustering, and topic visualisation.

## 📑 Data Source

This project uses Reddit posts obtained through the **Pushshift** dataset:

* Pushshift Reddit Dataset: [https://arxiv.org/abs/2001.08435](https://arxiv.org/abs/2001.08435)
* Additional subreddit dump reference:
  [https://www.reddit.com/r/pushshift/comments/1itme1k/separate_dump_files_for_the_top_40k_subreddits/](https://www.reddit.com/r/pushshift/comments/1itme1k/separate_dump_files_for_the_top_40k_subreddits/)

Raw data is **not** included in this repo due to size and Reddit’s content redistribution rules.

---

## 🚀 Reproducing the Workflow

Recommended order:

1. **Clean and label finance posts**
   `01_data_cleaning_and_finance_classification.ipynb`

2. **Train the emotion model**
   `02_emotion_model_training_mentalbert.ipynb`
   (Saves the fine-tuned MentalBERT checkpoint.)

3. **Apply the trained model to all posts**
   `06_model_apply_full_dataset.ipynb`
   (Generates and saves emotion scores for every post.)

4. **Run the main analysis (basic emotions + polarity)**
   `04_main_emotion_analysis_basic_emotions.ipynb`

5. *(Optional)* **Explore all 27 emotions**
   `03_analysis_all_27_emotions_exploration.ipynb`

6. **Run topic modelling on finance posts**
   `05_topic_modelling_bertopic_finance_posts.ipynb`


## 🤝 Acknowledgements

This work was completed as part of the **Data Science Research Project** at the **University of Adelaide** under the supervision of **Dr Indu Bala**.
Thanks to colleagues and peers who contributed feedback and ideas throughout the project.



---

If you want, I can also draft a `requirements.txt` that matches these notebooks.
