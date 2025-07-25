# 🎵📈 Absurd Correlations: Can Spotify Trends Predict the S&P 500?  

![Predicted vs Actual S&P 500 Returns](./images/covers/image3.png)  

This project explores a **deliberately far-fetched question**:  

> _Can weekly Spotify audio feature trends (like danceability and energy) predict S&P 500 weekly returns?_  

Spoiler: **No, they can’t.**  
But the real value of this project lies in **going through the full data science pipeline**, practicing feature engineering, baseline models, neural networks, and even sequence models like LSTMs.  

---

## 🛠 What I Did  

1. **Data Collection**  
   - Downloaded **Spotify 1921–2020 dataset** (600k+ tracks) from Kaggle  
   - Aggregated weekly audio features: `danceability`, `energy`, `valence`, etc.  
   - Pulled **S&P 500 weekly closing prices** via `yfinance`  
   - Shifted financial data to align with Spotify’s Monday-based weekly bins  

2. **Data Exploration**  
   - Visualized **Spotify feature distributions**  
   - Examined **correlation matrix** for audio features  

   | Spotify Feature Distribution | Correlation Matrix |
   |------------------------------|--------------------|
   | ![Spotify Features](./images/spotify_feature_distribution.png) | ![Correlation Matrix](./images/spotify_correlation_matrix.png) |

3. **Target Engineering**  
   - Instead of raw prices (non-stationary), calculated **weekly returns (% change)**  
   - Prepared a clean merged dataset of Spotify weekly features + S&P weekly returns  

4. **Modeling Workflow**  
   - ✅ **Random Forest baseline** → severe overfitting, negative test R²  
   - ✅ **Feedforward Neural Network** → slight MAE improvement, still no signal  
   - ✅ **Lag features (past 3 weeks) + NN** → stabilized but still R² ~0  
   - ✅ **LSTM sequence model (5-week lookback)** → tested temporal context, still no meaningful predictive power  

5. **Final Evaluation**  
   - All models failed to generalize beyond training (negative R²)  
   - Predicted returns hug the mean, while actual returns remain noisy  

---

## 📊 Key Results  

| Model                     | Test MAE | Test RMSE | Test R² |
|---------------------------|----------|-----------|---------|
| Random Forest (returns)   | ~0.87    | ~0.94     | -6.0    |
| Feedforward NN (returns)  | ~0.47    | ~0.60     | -1.85   |
| NN w/ Lag Features        | ~0.016   | ~0.026    | -0.03   |
| LSTM Sequence Model       | ~0.032   | ~0.047    | -2.31   |

Even with increasingly complex models, **no predictive signal emerged**.  

---



## 📝 Conclusion  

This project wasn’t about finding a magical correlation between Spotify and the stock market—it was about **going through the entire ML workflow**:  

- ✅ Cleaning and aligning **multiple time series datasets**  
- ✅ Engineering meaningful targets (returns instead of raw prices)  
- ✅ Building **baseline models (Random Forest)** and **deep learning models (NN, LSTM)**  
- ✅ Evaluating and comparing performance across multiple approaches  

The final verdict?  
> **Spotify audio feature trends don’t meaningfully predict S&P 500 weekly returns.**  

But the journey was valuable: it highlights **how to rigorously test absurd hypotheses**, avoid spurious correlations, and learn when the data simply has no signal.  

---

## 🎯 Key Takeaways  

- **Not all data relationships have predictive value**—even with complex ML models  
- **Random Forests & Neural Networks can overfit easily** on noisy financial data  
- **Temporal models like LSTMs don’t help when no true signal exists**  
- **The process matters**: data cleaning, feature engineering, and modeling are skills worth practicing, even if the final result is negative  

---

## 🧰 Tech Stack  

- **Python 3.10+**  
- **Pandas & NumPy** → data processing & merging  
- **Matplotlib & Seaborn** → visualizations (feature distributions, correlation matrix)  
- **yfinance** → S&P 500 weekly financial data  
- **scikit-learn** → Random Forest baseline, preprocessing, evaluation metrics  
- **TensorFlow/Keras** → Neural Networks & LSTM sequence models  
