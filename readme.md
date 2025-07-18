Credit Scoring Model for DeFi Wallets on Aave V2


Overview
This project builds a machine learning model that assigns a credit score between 0 and 1000 to Ethereum wallets based on their transaction behavior on the Aave V2 protocol.

Higher scores reflect responsible and reliable usage (e.g., repayments, consistent deposits).

Lower scores indicate risky, bot-like, or exploitative behavior (e.g., many borrows without repayments, frequent liquidations).

Project Structure
bash
Copy
Edit
├── model       # Main training + scoring script
├── cleaned_data.csv       # Input cleaned transaction data
├── credit_score_model.pkl       # Trained ML model (RandomForest)
├── README.md                   # Methodology and project explanation
├── analysis.md                 # Post-model analysis and score insights
Feature Engineering
The model is trained on aggregated behavioral features per wallet, derived from transaction-level logs:

Feature Name	Description
total_deposit	Total number of deposit actions
total_borrow	Total number of borrow actions
total_repay	Total number of repay actions
total_liquidation	Total number of liquidation events
deposit_amount	Total amount deposited (ETH equivalent)
borrow_amount	Total amount borrowed (ETH equivalent)
repay_amount	Total amount repaid (ETH equivalent)
liquidation_count	Times wallet was liquidated
repay_per_borrow	Ratio of repay to borrow actions
liquidation_per_borrow	Liquidation frequency relative to borrowing
avg_borrow_per_tx	Average ETH per borrow
avg_repay_per_tx	Average ETH per repay

ML Model Architecture
Model Type: RandomForestRegressor

Target Variable: Custom score between 0–1000 (engineered based on behavior)

Train-Test Split: 80/20 split

Cross-validation: 5-fold CV for robustness

Scoring Logic: Based on heuristic weighted behavior, normalized to 1000 scale

Processing Flow
Load CSV: cleaned_data.csv

Aggregate: Compute wallet-level behavioral features

Score Assignment: Create score column using heuristic weights

Train Model: Fit a RandomForestRegressor on features to predict scores

Save Model: Export trained model to model.pkl

Predict Scores: Apply to all wallets, save scored dataset

Execution
To run and train the model:

bash
Copy
Edit
python credit_score_model.py
Make sure cleaned_aave_data.csv is in the same folder.

Dependencies
pandas

numpy

scikit-learn

matplotlib (for analysis)

Install with:

bash
Copy
Edit
pip install -r requirements.txt
