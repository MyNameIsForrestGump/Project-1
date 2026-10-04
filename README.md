Project Structure


Project 1
│
├── data/  
│   ├── processed_data/          # Cleaned dataset
│   └── raw_data/    # Original dataset 
│
├── notebooks/
│   ├── EDA.ipynb                  # Exploratory Data Analysis
│   ├── Preprocessing.ipynb        # Data cleaning & encoding
│   └── Model_Training.ipynb       # Model training, GridSearch & evaluation
│
├── models/           # Serialized trained models (.pkl)        
├── requirements.txt  # Project dependencies
└── README.md



Q&A Section: 

1. Q: Is it classification or regression? Which model error would be more costly in reality?
A: It is a binary classification problem, as the target variable (Churn) takes discrete values: 1 (the customer leaves) or 0 (the customer stays).
2. Q: Why do we split the data before scaling?
A: Because for scaling the data, we would use the mean and variance of the entire population creating some sort of a data leakage. The mean and variance include insights of the entire population including the testing set which we don't want to share before splitting the data. 
3. Q: What score does a model that knows nothing achieve?
 A: For F1-Score the baseline model predicting 1 for all instances achieves an F1-score of 0.00 if it predicts only the majority class (0), or around ~0.42 if it predicts only the minority class 1, due to low precision.

For Accuracy the baseline model that always predicts the majority class (No Churn) would achieve an Accuracy of ~73.4% simply because ~74.5% of the clients in this dataset do not churn. This highlights why Accuracy is a misleading metric for imbalanced data.
A:
4. Q: Which model turned out to be better, and why do you think that happened?
A: Random Forest and Logistic Regression close behind turned out to be the best-performing models, achieving a top F1-Score of ~0.628. Logistic Regression perform remarkably well on this dataset because key business drivers (like contract type, tenure, and payment method) have direct, linear relationships with churn risk. Random Forest slightly surpassed it by capturing additional non-linear interactions between financial metrics (MonthlyCharges, TotalCharges, tenure)

5. Q:Why did you choose the primary metric you selected?
A: I selected the F1-Score (specifically on the positive class 1) because the Telco dataset is imbalanced (0.7346 vs. 0.2653 (Acording to EDA.ipynb file)). Standard Accuracy rewards models that over-predict the majority class while ignoring churning customers. F1-Score acts as the harmonic mean between Precision (avoiding false alarms) and Recall (catching as many actual churning customers as possible), providing a balanced and robust evaluation focused on business value.
