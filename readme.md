💳 Credit Scoring Model for DeFi Wallets on Aave V2

## 📘 Overview

This project develops a machine learning model that assigns a **credit score between 0 and 1000** to Ethereum wallets based on their **behavioral patterns** on the **Aave V2 protocol**.

- **Higher scores** reflect **responsible and reliable usage**  
  (e.g., consistent repayments, deposits, low liquidation).
- **Lower scores** indicate **risky, bot-like, or exploitative behavior**  
  (e.g., borrowing without repaying, frequent liquidations, one-time actions).

---

## 📂 Project Structure

├── credit_score_model.py # Main training + scoring script
├── cleaned_data.csv # Cleaned input transaction data
├── credit_score_model.pkl # Trained ML model (RandomForest)
├── credit_score_distribution.png # Histogram of score distribution
├── README.md # Methodology and usage instructions
├── analysis.md # Post-model analysis and score insights

markdown
Copy
Edit

---

## 🛠️ Feature Engineering

The model is trained on **wallet-level aggregated features** derived from transaction logs:

| Feature Name            | Description                                             |
|-------------------------|---------------------------------------------------------|
| `total_deposit`         | Number of deposit actions                               |
| `total_borrow`          | Number of borrow actions                                |
| `total_repay`           | Number of repay actions                                 |
| `total_liquidation`     | Number of liquidation events                            |
| `deposit_amount`        | Total amount deposited (ETH equivalent)                |
| `borrow_amount`         | Total amount borrowed (ETH equivalent)                 |
| `repay_amount`          | Total amount repaid (ETH equivalent)                   |
| `liquidation_count`     | How often the wallet was liquidated                    |
| `repay_per_borrow`      | Ratio of repays to borrows                             |
| `liquidation_per_borrow`| Ratio of liquidations to borrows                       |
| `avg_borrow_per_tx`     | Average ETH per borrow transaction                      |
| `avg_repay_per_tx`      | Average ETH per repay transaction                       |

---

## 🧠 Model Architecture

- **Model Type**: `RandomForestRegressor`
- **Target Variable**: Custom credit score (0–1000), engineered heuristically
- **Train-Test Split**: 80% training, 20% testing
- **Cross-Validation**: 5-fold CV for generalization
- **Scoring Logic**:
  - Score derived from a **weighted combination of features**
  - Normalized to a **0–1000 scale**

---

## 🔁 Processing Pipeline

1. **Load CSV**: Import `cleaned_data.csv`
2. **Feature Aggregation**: Generate wallet-level behavioral features
3. **Score Assignment**: Calculate scores using heuristic weights
4. **Model Training**: Fit `RandomForestRegressor` on features to predict scores
5. **Save Model**: Export model as `credit_score_model.pkl`
6. **Predict Scores**: Apply to all wallets, export scored dataset

---

## ▶️ Execution

To train the model and assign scores:

```bash
python credit_score_model.py
Make sure cleaned_data.csv is present in the same directory.

📦 Dependencies
Install dependencies with:

bash
Copy
Edit
pip install -r requirements.txt
Required libraries:

pandas

numpy

scikit-learn

matplotlib (for visualizations)

