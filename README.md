# RN-SMOTE-on-Imbalanced-Data

## **Preprocessing Workflow**

### **Library Import & Data Extraction**
The script begins by importing necessary libraries for data manipulation, visualization, and modeling. It reads a CSV file (`train_test_network.csv`) as the input dataset.

### **Data Exploration**
1. **Initial Data Examination:**
   - Displays the first 10 rows of the dataset using `data.head(10)`.
   - Checks the dataset's structure with `data.info()`.

2. **Dropping Unnecessary Columns:**
   - Columns such as IP addresses, ports, and the `type` column are removed as they are not useful for the analysis.

3. **Handling Categorical Data:**
   - Identifies a list of categorical columns.
   - Computes the number of unique values for each categorical column to understand their diversity.
   - Removes the `dns_query` column due to its high cardinality.

4. **Encoding Categorical Data:**
   - Uses one-hot encoding (`pd.get_dummies`) to convert categorical columns into numeric form.

---

### **Feature Scaling**
The script applies three scaling methods (`MinMaxScaler`, `StandardScaler`, and `RobustScaler`) to normalize the numerical features. The scaled data is then used for further modeling.

---

### **Label Encoding**
The target variable (`label`) is encoded into numeric format using `LabelEncoder`.

---

## **Model Training with Different Balancing Techniques**

### **1. No Balancing**
- Splits the dataset into training and testing sets (e.g., 90/10 split).
- Fits an **XGBoost** classifier on the imbalanced data.
- Evaluates the model's performance using:
  - Accuracy score.
  - Confusion matrix.
  - Classification report.
  - ROC-AUC score (for binary classification).

---

### **2. SMOTE (Synthetic Minority Over-sampling Technique)**
- Balances the data by synthesizing new samples from the minority class.
- Trains the XGBoost model on the balanced dataset.
- Evaluates performance using the same metrics as above.

---

### **3. RN-SMOTE (Random Noise SMOTE)**
- Adds random noise to the synthetic samples generated by SMOTE.
- Trains the XGBoost model on the noise-added dataset.
- Evaluates performance using the same metrics.

---

### **Performance Comparison**
A helper function `get_metrics` is defined to compute:
- Accuracy.
- Precision.
- Recall.
- F1-score.
- ROC-AUC (if applicable).

The performance of the three techniques (No Balance, SMOTE, RN-SMOTE) is summarized in a DataFrame.

---

## **Results**
| Method        | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---------------|----------|-----------|--------|----------|---------|
| No Balance    | 0.997252 | 0.997250  | 0.997252 | 0.997251 | 0.981721 |
| SMOTE         | 0.820516 | 0.890296  | 0.820516 | 0.832883 | 0.981721 |
| RN-SMOTE      | 0.820516 | 0.890296  | 0.820516 | 0.832883 | 0.981721 |

### **Observations:**
- The "No Balance" model performs exceptionally well, likely due to data imbalance.
- SMOTE and RN-SMOTE significantly reduce the model's accuracy but may improve the balance between precision and recall for minority classes.

---

### **Suggestions for Further Analysis**
- Analyze confusion matrices to better understand class-specific performance.
- Test additional balancing techniques like **ADASYN** or cost-sensitive learning.
- Validate results with a larger test set or cross-validation.

