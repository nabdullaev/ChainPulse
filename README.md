# ChainPulse

ChainPulse is a machine learning solution for on-chain analytics. In this project, I built an MVP that predicts the daily active addresses for multiple crypto tokens by leveraging aggregated on-chain data. The solution employs classical ML models with time series cross-validation and MLflow for experiment tracking.

I start with a market-level model to capture overall trends and tokenomics, enabling easier comparison across multiple loss functions and custom metrics for business logic (Weighted MAE and Weighted Directional Accuracy). Later, the approach is refined by training token-specific models and proposing future work direction.

This repository serves as an experimental playground to understand market dynamics and offers a foundation for further improvements, including the integration of social signals.
