What Drives the Price of a Used Car?

Overview

This project analyzes 342,000 used car listings to understand which factors most strongly influence vehicle prices. Using the CRISP-DM framework, we cleaned the data, engineered features, and built regression models to explain and predict used car values. These insights help dealerships make more informed pricing and acquisition decisions.

Data Prep

Key steps:
	•	Removed outliers or incomplete listings
	•	Dropped highly missing or low-value fields (size, condition, cylinders, VIN, paint_color)
	•	Engineered some features:
	•	    age = 2025 − year
	•	    odometer_log = log(odometer)
	•	    price_log = log(price)
	•	One-hot encoded categorical fields using sparse matrices to handle high-cardinality fields like model

Final dataset: 342k rows vs. 426k in the original dataset.

Modeling

Two regression models were trained:
	1.	Linear Regression (baseline)
	2.	Ridge Regression with 5-fold cross-validation and hyperparameter tuning

Evaluation Metrics: RMSE and MAE on a held-out test set.

Performance
Model	RMSE	MAE
Linear Regression	0.374	0.230
Ridge Regression	0.371	0.229

Ridge performed slightly better, indicating that regularization helps stabilize estimates

What we found:
	•	Age and mileage are strong predictors of price.
Older vehicles and higher-mileage vehicles show consistent, significant discounts.
	•	Certain models command outsized premiums.
Examples include Vanagon camper variants, Skyline GTR, Supra twin turbo, NSX, and LandCruiser FJ45—reflecting collector demand and rarity.
	•	Some models show steep price penalties.
Fiesta S sedan, Mighty Max, and certain Silverado/Traverse variants showed large negative coefficients.
	•	Title status strongly affects price.
Salvage or rebuilt titles sharply reduce expected value.
	•	Transmission, fuel type, and state matter but less than age/mileage.

⸻

Recommendations for Dealers
	•	Price vehicles primarily based on age and mileage, as these are the most reliable indicators of value.
	•	Expand acquisition of high-demand specialty models that show consistent premiums.
	•	Apply deeper discounts or avoid overpaying for models with historically low price performance.
	•	Treat salvage/rebuilt title vehicles as high-risk inventory requiring significant markdowns.