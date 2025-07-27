# Wallet_Risk_Scoring_From_Scratch


This project analyzes 103  wallet adresses using transaction history from the **Compound V2 protocol**, computes wallet-level features, and assigns a **risk score from 0 to 1000**.

## 📁 Files Included

- `wallet id-Sheet1.csv`:File containing wallet adresses.
- `wallet_risk_scores.csv`: Final output with wallet IDs and risk scores.
- `Wallet_Risk_Scoring_From_Scratch.ipynb`: The main Colab notebook containing the full code pipeline.
- `README.md`: This file, documenting the workflow and methodology.

## 🚀 Objective

Given a list of wallet addresses, the goal is to:
1. Fetch Compound V2 on-chain transaction history.
2. Generate features describing activity and risk.
3. Score wallets on a scale of 0 (low risk) to 1000 (high risk).

## 📊 Features Used for Scoring

For each wallet, the following indicators were derived from Compound V2 activity:

- `compound_tx_count`: Total number of transactions involving Compound V2.
- `unique_contracts_interacted`: Number of unique Compound V2 contracts interacted with.
- `max_tx_value_eth`: Largest single transaction value (in ETH).
- `avg_gas_fee_eth`: Average gas fee across Compound-related transactions.
- `last_activity_days_ago`: How many days ago the wallet last interacted with Compound V2.

## 🧮 Scoring Methodology

Each feature was normalized using min-max scaling and combined using the following weights:

| Feature                     | Weight |
|----------------------------|--------|
| Compound transaction count | 0.3    |
| Unique contracts           | 0.2    |
| Max TX Value (ETH)         | 0.2    |
| Avg Gas Fee (ETH)          | 0.1    |
| Recency (inverse)          | 0.2    |

The resulting score was scaled from **0 to 1000**, where a higher score reflects greater on-chain activity and potentially higher risk exposure.

## 🧾 Sample Output (`wallet_risk_scores.csv`)

| wallet_id                                   | score |
|--------------------------------------------|-------|
| 0x0039f22efb07a647557c7c5d17854cfd6d489ef3  | 800   |
| 0x06b51c6882b27cb05e712185531c1f74996dd988  | 313   |
| ...                                         | ...   |

## 📌 Notes

- Data was retrieved using the **GoldRush API** (free tier).
- Only transactions associated with **Compound V2 contract addresses** were considered.
- The notebook is optimized for Google Colab and processes all 103 wallets end-to-end.

---

