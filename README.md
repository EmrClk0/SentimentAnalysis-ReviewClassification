
# Review Classification Based On Sentiment Analysis


The purpose of this project is to extract the positive, negative, and neutral sentiment ratios from user reviews and assign a score between 1 and 5 based on this sentiment analysis. The sentiment ratios derived from the reviews are fed into a trained logistic regression model, which classifies each review with a specific score. The project aims to automatically analyze user reviews to quickly and accurately measure the overall satisfaction with a product or service. This allows businesses and developers to make better use of user feedback.



## Dataset

The dataset used in this project is the Women’s E-Commerce Clothing Reviews dataset. This dataset contains customer reviews of women's clothing products along with various supporting features. The details of the dataset are as follows:

- **Source**: [Kaggle - Women’s E-Commerce Clothing Reviews](https://www.kaggle.com/datasets/nicapotato/womens-ecommerce-clothing-reviews)
- **Size**:  23,486 rows and 10 features.
- **Content**
  - **Clothing ID**: A unique identifier for the products.
  - **Age**: The age of the reviewer.
  - **Title**: The title of the review.
  - **Review Text**: The content of the review.
  - **Rating**: The score given by the user (1 - Worst, 5 - Best).
  - **Recommended IND**: Whether the product was recommended (1 - Recommended, 0 - Not recommended).
  - **Positive Feedback Count**: The number of other users who found this review helpful.
  - **Division Name**: The high-level category of the product.
  - **Department Name**: The department name of the product.
  - **Class Name**: The class name of the product.

- **Rating Distribution**
    - **5 stars**: 12,540 reviews  
    - **4 stars**: 4,908 reviews  
    - **3 stars**: 2,823 reviews  
    - **2 stars**: 1,549 reviews  
    - **1 stars**: 821 reviews  



## Steps of the Project

### 1. Cleaning Data
The data cleaning phase is a critical step to ensure the data is accurate and consistent. The following operations were performed in this step:

**Removing Unnecessary Columns**

Unnecessary columns in the dataset were removed. Only the review and rating columns were retained as they provide the necessary data for the model to work.

**Removing Missing Data**

Rows containing NaN (Not a Number) values were identified and removed from the dataset.

**Type Conversion**

Some features had incorrect data types, so they were converted to the appropriate data types.



### 2. Sentiment Score Extraction
The data cleaning phase is a critical step to ensure the data is accurate and consistent. The following operations were performed in this step:

**Model Selection**

The model used, "cardiffnlp/twitter-roberta-base-sentiment", is trained on social media texts and has shown high success in extracting sentiment ratios from texts.

**Processing the Reviews**

Each review in the dataset was processed in sequence and converted into the format required by the model. The model extracted three main sentiment ratios for each review:

- **Positive (Pos)**: The portion of the review that conveys a positive sentiment.
- **Negative (Neg)**: The portion of the review that conveys a negative sentiment.
- **Neutral (Neu)**: The portion of the review that conveys a neutral sentiment.



*Example Data*


| review | rating | neg | neu | pos | result |
| :------| :------| :---| :---| :---| :------ |
| Absolutely wonderful - silky and sexy and | 4 | 0.002245 | 0.010576|0.987180|pos|




### 3. Classification

#### **Data Visualization**

##### **Rating Distribution**
The first visualization focuses on the distribution of ratings in the dataset. This visualization shows how many comments there are for each rating (from 1 to 5).

![distribution of ratings](https://github.com/user-attachments/assets/cace240e-0579-470f-87ae-7e85bdf7b138)


##### **Sentiment Distribution by Rating**
The second visualization shows sentiment distributions based on rating values. This visualization analyzes the positive, negative, and neutral sentiment ratios for each rating (from 1 to 5). It allows us to observe, for example, whether reviews with a rating of 5 are mostly positive or neutral.

![Sentiment Distribution by Rating1](https://github.com/user-attachments/assets/8ce25d26-71d8-450f-be3b-b5a7a6c14422)

![Sentiment Distribution by Rating2](https://github.com/user-attachments/assets/e5d10593-a8f4-40ed-bb7a-e35dd89b19cc)
---

#### **Data Balancing**
In datasets, when some classes (in this case, certain ratings) are over-represented, the model may focus more on these classes. This can lead to the issue of class imbalance. Imbalanced datasets can cause the model to fail in learning low-frequency classes properly, increasing classification errors. To address this problem, data balancing techniques were applied.

##### **Random Under-Sampling (RUS)**
The RandomUnderSampler method reduces the number of examples from over-represented classes randomly to resolve the imbalance.

##### **SMOTE (Synthetic Minority Over-sampling Technique)**
The SMOTE method synthetically generates new examples for under-represented classes. This technique creates new samples from existing ones to increase the number of minority class examples. The advantage of SMOTE is that it helps prevent the model from overfitting while generating more samples.

---

#### **Logistic Regression Model**
Logistic regression, which is typically used for binary classification problems, can also be effectively applied to multi-class classification problems. In this project, the logistic regression model was used to **rate** user reviews from 1 to 5. The model was trained to classify each review with a specific rating based on sentiment analysis.

##### **Model Training**
The model was trained using the **training data**. In this phase, features derived from sentiment analysis (positive, negative, and neutral ratios) and labeled rating information were used. The training data allowed the model to learn each class (ratings from 1 to 5) accurately.

##### **Hyperparameter Optimization**
To improve the performance of the logistic regression model, **hyperparameter optimization** was performed. This step is crucial for ensuring that the model gives better results with the correct hyperparameters. In particular, optimization was carried out on hyperparameters such as the **C parameter**, which controls the learning rate of the model.

---

#### **Model Evaluation**
After the training process, the model's performance was evaluated on the test data. **Accuracy** and other metrics (precision, recall, F1 score) were used to measure the model's success.

![cm1](https://github.com/user-attachments/assets/a99e1f40-a890-4b84-8eb1-98b104e1333a)

