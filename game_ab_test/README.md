# Cookie Cats Mobile Game - A/B Testing Analysis

This project performs an **A/B testing analysis** for the mobile puzzle game, **Cookie Cats**. The goal is to evaluate the impact of moving the first in-game gate (forcing players to wait or make a purchase) from **Level 30** to **Level 40** on player retention and game rounds played.

---

##  Project Overview & Business Problem
In mobile gaming, retaining players is crucial for long-term monetization. Gates are placed to create natural pauses in gameplay, preventing player burnout and encouraging in-app purchases. However, placing them too early or too late can negatively affect user retention.

* **Control Group (A):** Gate encountered at Level 30.
* **Test Group (B):** Gate encountered at Level 40.

Analyzed the dataset to determine which gate level drives better user engagement and long-term retention.

---

## 📊 Dataset Description
The dataset contains information on 90,189 players who installed the game during the A/B test:
* `userid`: A unique number that identifies each player.
* `version`: Whether the player was put in the control group (`gate_30`) or the test group (`gate_40`).
* `sum_gamerounds`: The number of game rounds played by the player during the first 14 days after install.
* `retention_1`: Did the player come back and play 1 day after installing? (True/False)
* `retention_7`: Did the player come back and play 7 days after installing? (True/False)

---

## Methodology & Statistical Analysis

### 1. Data Cleaning & EDA
* Detected and removed an extreme outlier in `sum_gamerounds` (a player with 49,854 rounds in 14 days).
* Handled users who installed the game but never played a single round (`sum_gamerounds == 0`).

### 2. Game Rounds Analysis (`sum_gamerounds`)
* **Test Used:** **Mann-Whitney U Test** (chosen because the distribution of game rounds was highly skewed and non-normal).
* **Result:** No statistically significant difference in the distribution of game rounds between the two groups ($p \approx 0.0502$).

### 3. Retention Analysis (`retention_1` & `retention_7`)
* **Test Used:** **Chi-Square ($\chi^2$) Test of Independence** (chosen for categorical retention variables).
* **Results:**
  * **Day 1 Retention:** No significant difference ($p \approx 0.0750$). Both versions perform similarly on the first day.
  * **Day 7 Retention:** **Highly statistically significant difference ($p \approx 0.0016$)**. 
    * `gate_30` (Control) Day 7 Retention: **19.02%**
    * `gate_40` (Test) Day 7 Retention: **18.20%**

---

## 🏆 Key Findings & Recommendation

Contrary to the intuitive idea that "more uninterrupted gameplay is better," delaying the gate to Level 40 actually decreased long-term player retention. 

* **The Decision:** **The company should keep the gate at Level 30.** A $0.82\%$ drop in Day 7 retention might look small, but at scale, it translates to thousands of lost active users and a substantial hit to long-term in-app purchase and ad revenue.

