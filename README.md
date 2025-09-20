# Design and Analysis of a Content-Based Restaurant Recommender System

## 🚀 Introduction

This project presents a content-based restaurant recommender system designed to provide personalized dining suggestions. By analyzing various attributes of restaurants such as cuisine, location, and customer ratings the system identifies and recommends establishments that are most similar to a user's specified choice.

The entire analysis and model development process is documented in the accompanying Jupyter Notebook.

***

## 🎯 Problem Statement

The main goal of this project is to develop a robust **content-based recommender system** that suggests restaurants to users based on the similarity of their attributes to a given restaurant. The system is designed to be wrapped in a function that takes a restaurant name as input and returns the top 10 most similar recommendations.

***

## 📊 Dataset

The project utilizes the **"Dataset 3B (restaurant recommendation)"**, which contains the following key features for each restaurant:

* **Restaurant Details**: Name, Zomato URL, location, and type (e.g., Quick Bites, Casual Dining).
* **Cuisine**: Types of cuisines served.
* **Service Options**: Availability of online ordering and table booking.
* **Customer Feedback**: Overall rating (0-5) and the number of votes.
* **Cost**: Approximate cost for a meal for two people (in Rupees).
* **Categorization**: Restaurant category (e.g., Delivery, Dine-out).
* **Menu Offerings**: Binary flags indicating whether the restaurant sells specific food types like beverages, Chinese, Thai, Indian, Mediterranean, fast food, or desserts.

***

## 🛠️ Methodology

The project is structured around a comprehensive data science workflow, from data cleaning and exploration to building and evaluating the recommender system.

### 1. Exploratory Data Analysis (EDA) & Preprocessing

A thorough EDA was performed to clean the data, handle anomalies, and prepare it for modeling. The key steps included:

* **Data Cleaning**:
    * **Missing Values**: Missing `rate` values were imputed for restaurants with votes by using the mean rate of similar establishments (based on location and restaurant type). Rows with missing rates and zero votes were dropped, as they provided little value. The remaining missing values, constituting only about 1% of the data, were also dropped for simplicity.
    * **Anomaly Handling**: Anomalous and non-numeric entries in the `rate` column (such as 'NEW', 'X', '-') were removed. The `cost` column was cleaned by removing commas and converting it to a numeric type.
    * **Text Formatting**: Inconsistent text encoding in the `name` column was fixed using the `ftfy` library.
* **Handling Multi-Branch Restaurants**: Since many restaurants have multiple branches, the dataset was preprocessed by grouping entries by the restaurant `name`. For each restaurant, categorical features like `cuisines`, `location`, `rest_type`, and `type` were aggregated by combining their unique values into a single string. Numerical features like `rate`, `votes`, and `cost` were averaged across all branches.
* **Feature Engineering & Scaling**:
    * Binary features were encoded for columns like `online_order` and `book_table`.
    * Numerical features (`cost`, `votes`, `rate`) were scaled using `RobustScaler` to handle skewed distributions and outliers effectively.

### 2. Content-Based Recommender System

The core of the project is a content-based recommender system built using the **"Soup" technique**. This approach creates a unified text representation (a "soup") for each restaurant by combining its most important attributes.

* **Weighted Feature Soup**: A weighted "soup" was created for each restaurant by concatenating its `location`, `rest_type`, `cuisines`, `type`, `rate`, and `votes`. The weights were subjectively assigned based on their perceived importance in influencing customer choice:
    * **cuisines (7)**: Highest weight, as it is the primary decision factor.
    * **location & rate (6)**: High importance for convenience and customer satisfaction.
    * **votes & rest\_type (5)**: Reflects popularity and dining occasion suitability.
    * **type & cost (4)**: Moderate importance, depending on user needs.
* **TF-IDF and Cosine Similarity**:
    * The "soup" for each restaurant was transformed into a numerical vector using **TF-IDF (Term Frequency-Inverse Document Frequency)**.
    * **Cosine similarity** was then calculated between all restaurant vectors to determine their similarity.
* **Recommendation Function**: A function, `get_recommendations_with_details`, was created to take a restaurant name as input and return the top 10 most similar restaurants based on their cosine similarity scores.

***

## 📈 Evaluation & Analysis

The recommender system was evaluated using three distinct inputs to test its performance across different restaurant types.

### 1. Black Cup Cafe (Common Restaurant Type - Cafe)

* **Input**: A cafe in the BTM area, known for fast food and beverages, available for dine-out and delivery.
* **Recommendations**: The system recommended other cafes, primarily in the **BTM area**, with similar cuisine offerings (fast food, beverages). The high similarity scores (ranging from 0.81 to 0.92) confirm that the model effectively prioritized `location`, `rest_type`, and `cuisines`.

### 2. Hard Rock Cafe (Less Common Type - Pubs and Bars)

* **Input**: A well-known pub and bar on St. Marks Road, serving American and BBQ cuisine.
* **Recommendations**: The system successfully recommended other high-end pubs, microbreweries, and bars like **Arbor Brewing Company** and **Big Pitcher**. The recommendations shared similar attributes in `rest_type` (Pub, Microbrewery), `type` (Drinks & nightlife), and high customer `ratings` and `votes`, showing the model's ability to capture the "vibe" of an establishment.

### 3. Cinnamon's Kitchen (Randomly Selected Restaurant)

* **Input**: A Quick Bites restaurant on Old Airport Road, serving North and South Indian fast food, primarily for delivery.
* **Recommendations**: The recommendations were highly relevant, featuring other Quick Bites and delivery-focused restaurants on **Old Airport Road** that also serve Indian and fast food. The top recommendation, **"Chef Fast Food,"** had an exceptionally high similarity score (0.985), indicating a very close match.

***

## 💡 Conclusion

The content-based recommender system developed in this project has proven to be highly effective and contextually accurate. The "Soup" technique, combined with weighted features, successfully captures the defining characteristics of restaurants, leading to relevant and logical recommendations.

The system's strength lies in its ability to prioritize features like **cuisine and location**, which are critical to user decision-making, while also considering other important factors like customer ratings and restaurant type. The evaluation confirms its robustness across both common and niche restaurant categories.

While the current model is a strong foundation, future improvements could include incorporating more user-specific data for personalization and exploring more advanced techniques to further enhance recommendation diversity.

***

## ⚙️ How to Reproduce

To run this analysis and use the recommender system, follow these steps:

1.  **Clone the repository**:
    ```bash
    git clone [https://github.com/arieltarliman/Design-and-Analysis-of-a-Content-Based-Restaurant-Recommender-System.git](https://github.com/arieltarliman/Design-and-Analysis-of-a-Content-Based-Restaurant-Recommender-System.git)
    ```
2.  **Install dependencies**: Make sure you have Python and the required libraries installed (e.g., pandas, scikit-learn, ftfy).
3.  **Run the Jupyter Notebook**: Open and run the `UAS NO 3.ipynb` notebook to see the full analysis and interact with the recommendation function.
