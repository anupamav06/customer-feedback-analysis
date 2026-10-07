# Customer Feedback Analysis and Automated Response

## 1. Project Overview

This project analyzes customer reviews to identify critical negative feedback
and automatically generate personalized customer-support responses using
Generative AI.

The project combines Python-based data analysis, rule-based text processing,
and Google Gemini Generative AI.

The main workflow is:

Customer Reviews
→ Data Cleaning
→ Critical Review Filtering
→ Complaint Keyword Analysis
→ Complaint Phrase Analysis
→ Complaint Category Analysis
→ Rule-Based Priority Scoring
→ Top 3 Critical Reviews
→ Gemini AI
→ Personalized Customer-Support Emails


## 2. Objective

The objectives of this project are:

- Clean and analyze customer review data using Python and Pandas.
- Identify critical reviews using a rule-based approach.
- Identify common complaint keywords and phrases.
- Analyze major complaint categories.
- Prioritize highly critical and detailed reviews.
- Select the three highest-priority reviews.
- Generate personalized and empathetic customer-support emails using
  Google Gemini.


## 3. Dataset

The project uses a Trustpilot customer-review dataset.

The original dataset contains customer reviews, star ratings, companies,
business categories, review titles, and review text.

For this analysis, the dataset is restricted to the following retail-relevant
categories:

- Shopping & Fashion
- Electronics & Technology
- Home & Garden

This scope was selected to keep the analysis focused on online retail
customer feedback.

The filtered dataset contains 17,531 reviews.


## 4. Data Cleaning

The following preprocessing steps are applied to the review text:

1. Convert text to lowercase.
2. Remove HTML tags.
3. Remove unnecessary special characters.
4. Normalize multiple spaces.
5. Remove leading and trailing whitespace.

The original review column is preserved, while a separate
`review_clean` column is created for text analysis.


## 5. Identifying Critical Reviews

Reviews with a rating of 1 or 2 stars are classified as critical reviews.

This is a rule-based approach and does not use Machine Learning.

The critical reviews are then analyzed separately to identify common
complaint patterns.


## 6. Complaint Keyword Analysis

Common complaint keywords are identified using document frequency.

Instead of counting every occurrence of a word, each review contributes
at most one count for a particular keyword.

This allows the analysis to represent the percentage of critical reviews
containing a keyword more accurately.

Common English stopwords are removed while important negative words such
as `not`, `no`, and `never` are retained because they can carry important
meaning in customer complaints.


## 7. Complaint Phrase Analysis

Bigrams are used to identify frequently occurring two-word complaint
phrases.

Examples include:

- customer service
- no response
- not received
- no reply

These phrases provide additional context beyond individual keywords.


## 8. Complaint Category Analysis

Rule-based keyword groups are used to identify major complaint themes,
including:

- Delivery
- Orders
- Refund and Payment
- Customer Service
- Product Quality

A review can belong to more than one complaint category.


## 9. Category-Level Business Analysis

The project also calculates the proportion of critical reviews across
different business categories.

This helps identify categories with relatively higher levels of negative
customer feedback.


## 10. Rule-Based Priority Scoring

A transparent rule-based priority score is used to select the three most
critical and detailed reviews.

The score considers:

- Star-rating severity
- Explicit severity phrases
- Review detail/length

Examples of severity signals include phrases such as:

- scam
- fraud
- never arrived
- still waiting
- trading standards
- solicitor
- chargeback

No Machine Learning model is used for prioritization.


## 11. Generative AI

Google Gemini is used to generate personalized customer-support emails.

The prompt instructs the model to:

- Act as a professional customer-support agent.
- Address the customer's specific complaints.
- Reference concrete facts from the review.
- Maintain an empathetic and professional tone.
- Avoid inventing refunds, replacements, compensation, policies,
  investigations, or other unsupported actions.
- Avoid making unsupported promises.
- Keep the response concise.
- Sign off using the relevant company name.


## 12. API Key Setup

The project uses the Google Gemini API.

The API key is intentionally NOT stored in the notebook.

When running the GenAI section, the notebook securely asks for the API key
using `getpass`.

Example:

```python
from google import genai
from getpass import getpass

api_key = getpass("Enter your Gemini API key: ")

client = genai.Client(api_key=api_key)

## 13. How to Run

1. Install the required Python libraries.
2. Place `trustpilot_reviews_2005.csv` in the same directory as the notebook.
3. Open `int1.ipynb` in Jupyter Notebook or VS Code.
4. Run the cells from top to bottom.
5. When prompted, enter your Gemini API key.
6. The notebook generates the top 3 responses and saves them to:
   `top_3_genai_responses.csv`.