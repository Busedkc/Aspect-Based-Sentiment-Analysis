# Aspect-Based Sentiment Analysis (ABSA) Annotation and Prompting Project

## Project Description
This project investigates and compares annotation methods and prompting techniques for Aspect-Based Sentiment Analysis (ABSA). The study comprises two main stages:

1. **Stage 1:**
   - **Dataset 1**: An annotated dataset (Dataset1) sourced online was used as a benchmark.
   - 100-200 samples were extracted from Dataset1, stripped of annotations, and re-annotated using:
     - **Zero-shot**, **few-shot**, and **chain-of-thought** (CoT) prompting strategies.
     - Advanced language models such as ChatGPT, Claude, and Gemini.
   - The re-labeled data was compared with the original dataset using accuracy, precision, F1-score, and recall metrics.

2. **Stage 2:**
   - **Dataset 2**: A new dataset of 300 entries was created by scraping YouTube comments using Selenium and ChromeDriver.
   - This dataset was annotated with zero-shot, few-shot, and CoT methods using ChatGPT.
   - Aspect categories were constrained to topics relevant to the video comments, with data saved in JSON format for consistency.

---

## Final Prompts Used for Annotation

### **Dataset 1 Prompts**

#### **Prompt 1: Zero-shot**
```text
Analyze the following review and identify the aspects discussed. The aspects can belong to the following categories: ambience, food, menu, miscellaneous, place, price, service, and staff. For each aspect mentioned, assign a sentiment (positive, negative, or neutral). Provide the output in JSON format.
Review: "The atmosphere was wonderful, but the service and food were terrible."
```

#### **Prompt 2: Few-shot**
```text
Analyze the following review for aspects and sentiments. The aspects can belong to the following categories: ambience, food, menu, miscellaneous, place, price, service, and staff. For each aspect, determine its sentiment (positive, negative, or neutral). Refer to the examples for guidance.

Example 1: 
Review: "The food was delicious, but the service was slow."
Output: {"aspects": [{"aspect": "food", "sentiment": "positive"}, {"aspect": "service", "sentiment": "negative"}]}

Review: "The atmosphere was wonderful, but the service and food were terrible."
```

#### **Prompt 3: CoT**
```text
Analyze the following review for aspects and sentiments step by step. The aspects can belong to the following categories: ambience, food, menu, miscellaneous, place, price, service, and staff. Follow these steps:

Step 1: Identify the aspects mentioned in the review.
Step 2: Assign a sentiment (positive, negative, or neutral) to each aspect.
Step 3: Provide the output in JSON format.

Review: "The atmosphere was wonderful, but the service and food were terrible."
```

### **Dataset 2 Prompts**

#### **Prompt 1: Zero-shot**
```text
Analyze the following review and identify the aspects discussed. The aspects can belong to the following categories: Recipe Ingredients, Recipe Instructions, Taste/Texture, Adjustments/Modifications, User Experience, Presentation/Visual Appeal, Questions/Clarifications, Sentiments Towards the Creator, Storage/Serving Suggestions, and Alternatives/Dietary Needs. For each aspect mentioned, assign a sentiment (positive, negative, or neutral). Provide the output in JSON format.

Example Review: "I used hot chocolate mix instead of cocoa powder because I don’t have cocoa powder.. will it taste the same?"
```

#### **Prompt 2: Few-shot**
```text
Analyze the following review for aspects and sentiments. The aspects can belong to the following categories: Recipe Ingredients, Recipe Instructions, Taste/Texture, Adjustments/Modifications, User Experience, Presentation/Visual Appeal, Questions/Clarifications, Sentiments Towards the Creator, Storage/Serving Suggestions, and Alternatives/Dietary Needs. Provide the output in JSON format.

Example 1: Review: "I tried the recipe and it tasted amazing"
Output: {"aspects": [{"category": "Taste/Texture", "sentiment": "positive"}]}

Example 2: Review: "This is the only baking channel I need."
Output: {"aspects": [{"category": "Sentiments Towards the Creator", "sentiment": "positive"}]}
```

#### **Prompt 3: CoT**
```text
Analyze the following review for aspects and sentiments step by step. The aspects can belong to the following categories: Recipe Ingredients, Recipe Instructions, Taste/Texture, Adjustments/Modifications, User Experience, Presentation/Visual Appeal, Questions/Clarifications, Sentiments Towards the Creator, Storage/Serving Suggestions, and Alternatives/Dietary Needs. Follow these steps:

Step 1: Identify the aspects mentioned in the review.
Step 2: Assign a sentiment (positive, negative, or neutral) to each aspect.
Step 3: Provide the output in JSON format.

Review: "Will it taste great if I don’t use the vanilla?"
```

---

## Scripts and Usage

### **xmltoJSON.py**
Converts an XML file into JSON format.

#### Steps to Run:
1. Place the XML file (e.g., `test.xml`) in the `dataset/` directory.
2. Execute:
   ```bash
   python xmltoJSON.py
   ```
3. Output: A JSON file (`test.json`) is saved in the `dataset/` directory.

### **delete_annotated_data.py**
Extracts text fields from a JSON file and saves them as separate objects.

#### Steps to Run:
1. Place the JSON file (`test.json`) in the `dataset/` directory.
2. Execute:
   ```bash
   python delete_annotated_data.py
   ```
3. Output: `texts_separate.json` is created in the `dataset/` directory.

### **first_100_texts.py**
Extracts the first 100 texts from a JSON file.

#### Steps to Run:
1. Place `texts_separate.json` in the `dataset/` directory.
2. Execute:
   ```bash
   python first_100_texts.py
   ```
3. Output: `first_100_texts.json` is saved in the `dataset/` directory.

### **webscrap.py**
Scrapes YouTube comments and processes them for annotation.

#### Steps to Run:
1. Update the video URL in the script:
   ```python
   video_url = "https://www.youtube.com/watch?v=your_video_id"
   ```
2. Execute:
   ```bash
   python webscrap.py
   ```
3. Output: A JSON file (`youtube_comments_english.json`) containing up to 300 English comments is saved.

---

## Evaluation Scripts

### **task3.py**
Compares annotations between two datasets and calculates the success rate of annotation matching.

### **task3_withSklearn.py**
Generates a classification report with precision, recall, and F1-score metrics.

#### Steps to Run:
1. Place the required JSON files in the `dataset/` directory.
2. Install dependencies:
   ```bash
   pip install scikit-learn
   ```
3. Execute:
   ```bash
   python task3_withSklearn.py
   
