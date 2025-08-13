# 🏡 Predicting House Prices in Ames, Iowa 🔮

Welcome, fellow data adventurer! This repository documents an epic quest to predict house prices for the legendary Ames, Iowa dataset from Kaggle. What follows is a tale of exploration, feature wrangling, and model showdowns, all culminating in a powerful XGBoost model that climbed the leaderboard.

> ### **🏆 Final Kaggle Score: 0.15 🏆**

---

## 🗺️ The Game Plan

Every good quest needs a map. Ours was a structured workflow that took us from being total strangers to the data to becoming its best friend.

### 1. The Detective Work 🕵️‍♂️ (Data Exploration)

First, we put on our detective hats and interrogated every feature to uncover its secrets.

* **Numerical Clues (`GrLivArea`, `YearBuilt`):** We used scatter plots to see if there was a "you go up, I go up" relationship with `SalePrice`. This helped us spot the obvious heroes and the suspicious outliers.
* **Categorical Clues (`Neighborhood`, `OverallQual`):** Boxplots were our secret weapon here. They let us see at a glance if living in 'NridgHt' was a golden ticket compared to 'Edwards', telling us which categories were the real VIPs.

### 2. Gold Mining & Tidying Up 🧹 (Feature Engineering)

This is where the real magic happened. We didn't just throw everything at the model; we carefully curated our features based on the clues we found. The goal: keep the gold, and toss the junk.

#### 💎 **The Goldmines: Features We Kept**

* **`OverallQual` & `ExterQual`:** The superstars! Their boxplots were perfect "staircases" to success. Every step up in quality meant a clear step up in price. A model's dream!
* **`GrLivArea` & `TotalBsmtSF`:** The bigger, the better! These showed a beautiful, straight-line relationship with price. More space = more money. Simple and powerful.
* **`GarageFinish`:** We picked this hero over its noisy cousin, `GarageType`. Why? It told a clean story: a finished garage is worth more than a rough one, which is worth more than an unfinished one. Easy!
* **`Neighborhood`:** Location, location, location! The boxplots proved that where a house is can drastically change its price. This was a must-have.

#### 🗑️ **The Noise: Features We Dropped**

* **`OverallCond` & `ExterCond`:** These were chaotic storytellers. Their boxplots were all over the place, with no clear trend. They would have just confused our model, so we politely showed them the door.
* **`Heating` & `Electrical`:** Snooze-fest! Over 95% of houses had the same type. A feature that doesn't change tells you nothing new. Dropped!
* **`MiscFeature`:** The "lottery ticket" feature. Sure, having a tennis court is a big deal, but only one house had one! A model can't learn a pattern from a single event. It was too rare to be reliable.

#### ✨ **Our Engineering Magic Tricks**

* **Smartly Filling Blanks:** We didn't just guess. We filled missing `LotFrontage` with the median of its own neighborhood and confirmed that missing garage info meant the house simply didn't have one.
* **The "Other" Bucket:** For features with lots of rare categories, we grouped the lonely ones into a single 'Other' bucket. This stops the model from chasing ghosts and gives it a stronger, cleaner signal to learn from.

### 3. The Universal Translator 🌐 (Data Preprocessing)

Our model only speaks the language of numbers, so we had to do some translating.

* **Taming the Beast (`SalePrice`):** Our target variable was wild and skewed. A log transformation (`np.log1p`) tamed it into a nice, normal distribution that our model could work with.
* **The Dummy Variable Factory:** We used `pd.get_dummies` to turn all our text-based categories into simple 0s and 1s, the only language our model truly understands.

### 4. Choosing Our Champion ⚔️ (Modeling)

We held a tournament of models to see who was worthy.

1.  **The Baseline Knights (`Linear` & `Ridge` Regression):** Our trusty but simple swords. They fought bravely but couldn't handle the complex, curvy nature of the data.
2.  **The Dragon Slayer (`XGBoost`):** The final boss! This powerful, tree-based model could learn all the complex twists and turns in the data that the linear models missed. It was the clear champion.

### 5. The Victory Lap 🏁

Our final XGBoost champion landed a **0.15** on the Kaggle leaderboard! This awesome score proved that our detective work, gold mining, and choice of a powerful model paid off.

The next adventure? Fine-tuning our XGBoost champion's magic dials (`hyperparameters`) to see if we can climb even higher!

---

## 🚀 How to Run This Adventure

1.  **Clone the Repo:** `git clone ...`
2.  **Install the Gear:** Make sure you have `pandas`, `numpy`, `scikit-learn`, `seaborn`, `matplotlib`, & `xgboost`.
3.  **Get the Treasure Maps:** Place `train.csv` and `test.csv` in the `data/` folder.
4.  **Start the Quest:** Run the `House_Prices.ipynb` notebook and enjoy the show!
