# COMP8420-DocBot
 
# DocBot: Intelligent Document Discovery
## Overview
In large enterprises, navigating extensive data warehouses to locate specific files and their respective paths can be a daunting task. This project addresses this real-world challenge by developing an Intelligent Question Answering (QA) system designed to enhance document discovery. The system aims to predict the correct file path, including folders and subfolders, when provided with a filename, thereby streamlining data retrieval processes in complex data environments. The output also gives the top 3 outputs with the highest probabilities as the folder names the files are located in.

## Project Scope
Data warehouses in large organizations store vast amounts of information across numerous folders and subfolders. Employees often face difficulties in locating the exact file they need, leading to inefficiencies and wasted time. The complexity of these data warehouses necessitates a robust solution that can accurately predict the paths of specific files based on minimal input, such as a filename or a short description.

## Methodlogy
**DistilBERT**: Chosen for its efficiency and effectiveness in question-answering tasks. DistilBERT, a smaller and faster variant of BERT, retains a significant portion of BERT's performance while requiring fewer computational resources.\ 
**Synthetic Data Generation**: Created using a Kaggle-based dataset, transforming product names into FAQs. The synthetic dataset serves as the foundation for training the model, ensuring it can handle a variety of user queries.\

## Dataset Utilized
A Kaggle-based dataset was adapted to form a synthetic dataset. Product names in the dataset were converted into user FAQs designed to find specific products. Manual annotation was performed for a subset of the products, while a Large Language Model (LLM) generated additional FAQs to increase the dataset size.

## Data Preparation
**Manual Annotation**: For a select number of products, team members manually created FAQs to ensure accuracy and relevance.\
**LLM Generation**: Leveraged a Large Language Model to generate additional FAQs, significantly expanding the dataset. This approach allows for the creation of diverse and varied queries that mimic real-world user interactions.\
**Final Training Data**: The combined FAQs and their corresponding labels (file paths) constitute the final training dataset.\

# Abalation Study
## Analysis of Model Outputs
### Original Model Output
  Before the ablation study, let’s assume the original model provided the following outputs for a given input:

Folder: face mask, Sub-folder: fresh, Probability: 0.7897\
Folder: eye cream, Sub-folder: fresh, Probability: 0.0319\
Folder: moisturizer, Sub-folder: fresh, Probability: 0.0210

###New Model Output After Ablation Study
After conducting the ablation study and removing weight decay, the model provided the following outputs:

Folder: sun protect, Sub-folder: supergoop!, Probability: 0.0906\
Folder: face mask, Sub-folder: fresh, Probability: 0.0821\
Folder: eye cream, Sub-folder: fresh, Probability: 0.0527\

### Detailed Analysis
#### Impact on Top Prediction

Original Top Prediction: face mask/fresh with a probability of 0.7897\
Ablation Top Prediction: sun protect/supergoop! with a probability of 0.0906\
\
**Analysis**: The removal of weight decay led to a significant change in the top prediction. The original model was highly confident in predicting face mask/fresh, while the new model is less confident and predicts sun protect/supergoop! as the top category. This indicates that the regularization previously helped in making more confident and potentially accurate predictions.
Probability Distribution

**Original Model**: The top prediction had a much higher probability (0.7897) compared to the rest.
**Ablation Model**: The probabilities are more evenly distributed (0.0906, 0.0821, and 0.0527).
**Analysis**: Removing weight decay resulted in a less confident model, as indicated by the more even distribution of probabilities. This could mean that without regularization, the model's decision boundaries have become less clear, leading to more uncertainty in predictions.
