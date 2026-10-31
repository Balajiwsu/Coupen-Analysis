# Will a Customer Accept the Coupon?

Practical Application 1. This project looks at survey data on driving coupons and asks which drivers accept a coupon delivered to their phone, and in which situations.

**Notebook:** [coupon_acceptance_analysis.ipynb](coupon_acceptance_analysis.ipynb)

## The data

- Source: UCI Machine Learning Repository, collected through an Amazon Mechanical Turk survey (`data/coupons.csv`).
- Size: 12,684 survey responses.
- Each response describes a driving scenario: destination, passengers, weather, time of day, coupon type and expiry. It also describes the driver: age, income, occupation, and how often they visit bars, coffee houses and restaurants.
- The target is `Y`: 1 if the driver would accept the coupon (right away or later), 0 if not.
- Cleaning:
  - Dropped the `car` column (99% empty) and one column that never changes.
  - Removed 74 duplicate rows.
  - Dropped the 5% of rows with a missing visit frequency.
  - **12,007 responses** remain.

## Key findings

**Overall:** about **57%** of coupons are accepted. Cheap food coupons (carry-out, restaurants under $20) do best at over 70%. **Bar coupons do worst at 41%.**

![Coupon types](images/coupon_types.png)

### Bar coupons
- **Bar habits are what matter most.** Drivers who go to a bar more than 3 times a month accept **76%** of bar coupons. Everyone else accepts **37%**.
- Drivers who go to bars more than once a month accept about **71–72%** if they are also **under 30**, or have **no kids in the car**.
- Income, occupation and restaurant habits make little difference.

![Bar coupon groups](images/bar_groups.png)

### Coffee house coupons (independent investigation)
- **Coffee habits are what matter most.** People who never visit coffee houses accept only **18%**. People who go at least once a month accept **65–68%**.
- **Time of day:** acceptance is highest at **10AM (63%)** and **2PM (55%)**, and lowest in the evening.
- **Trip context:** acceptance is higher on trips with **no urgent destination (58%)** than when heading home (36%). It is also higher with **friends or a partner** in the car (57–60%) than when driving alone (43%).
- **Coupon design:** coupons that last **1 day** beat **2-hour** coupons (58% vs 43%). Venues **25+ minutes away** are mostly ignored (34%).
- Combining these, regular coffee drinkers who get the coupon at 10AM or 2PM accept **77%** of the time.

![Coffee house coupons](images/coffee_habits_context.png)

## Recommendations

- **Target by habit first.** Send bar and coffee coupons to people who already visit these places at least once a month. This alone roughly doubles acceptance.
- **Don't send bar coupons when kids are in the car.** Favour younger adults.
- **Send coffee coupons mid-morning or early afternoon**, on leisure trips rather than commutes.
- **Use a 1-day expiry** instead of 2 hours, and only promote venues less than 25 minutes away.
- **Skip people who never visit that type of venue.** They rarely accept.

## Next steps

- Build a classification model (for example logistic regression or a decision tree) to score how likely each driver is to accept in each situation.
- Repeat the analysis for carry-out and restaurant coupons.
- Confirm the patterns with statistical tests, and ideally with a real A/B test. This is a survey of what people *say* they would do, not what they actually did.

## Repository structure

```
├── README.md                          # This summary
├── coupon_acceptance_analysis.ipynb   # Full analysis
├── data/
│   └── coupons.csv                    # Survey data
└── images/                            # Plots saved from the notebook
```
