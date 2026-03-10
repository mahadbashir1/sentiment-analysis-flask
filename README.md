# Sentiment Analysis Web Application

A comprehensive full-stack machine learning web application built with Flask that analyzes the sentiment of text, CSV files, and Amazon product reviews. It utilizes a trained Random Forest model and TF-IDF vectorization to classify sentiments into Positive, Neutral, or Negative, while providing generative suggestions and a historical tracking system.

## Features

- **Multi-Source Input**:
  - **Text Input**: Manually paste reviews or text for instant sentiment analysis.
  - **File Upload**: Upload `.csv` or `.txt` files containing bulk reviews.
  - **Amazon Scraper**: Simply paste an Amazon product URL, and the app will intelligently scrape the product details and user reviews using Selenium.
- **Machine Learning**: Utilizes a robust `RandomForestClassifier` trained on sentiment datasets with a `TfidfVectorizer` for processing text.
- **Sentiment Categorization**: Classifies reviews as Positive, Neutral, or Negative.
- **Generative Suggestions**: Provides actionable feedback/suggestions based on the identified sentiment for each review.
- **History Tracking**: Saves all previous analyses (including scraped product details, summary statistics, and individual review results) into a local `history.json` file.
- **Dashboard Interface**: A responsive and modern UI to interact with your data.

## Tech Stack

- **Backend**: Python, Flask
- **Machine Learning**: Scikit-Learn, Pandas, NLTK, Joblib
- **Web Scraping**: Selenium, WebDriver Manager
- **Frontend**: HTML, CSS, Bootstrap (via templates and static assets)

## Project Architecture

1. `app.py`: The main Flask server application handling routing, model loading, file processing, and history management.
2. `train_model.py`: Script responsible for preprocessing training data (e.g., `reviews.csv`), balancing the dataset, training the Random Forest model, and exporting the model (`sentiment_model_new.pkl`) and vectorizer.
3. `amazon_scraper.py`: Contains a Selenium-based automated scraper that navigates to an Amazon URL, scrolls intelligently to trigger lazy-loaded elements, and extracts product titles, images, descriptions, and reviews.
4. `data_preprocessing.py`: Utility functions containing regex logic, stop-word removal, and lemmatization (using NLTK) to clean textual data.
5. `generative.py`: A utility file that returns contextual generative suggestions based on inferred sentiment inputs.

## Setup Instructions

### Prerequisites
Make sure you have Python 3.8+ installed on your system. You also need Google Chrome installed for the Selenium scraper to work.

### 1. Clone the Repository
```bash
git clone <your-repository-url>
cd sentiment-analysis-flask
```

### 2. Set Up a Virtual Environment (Recommended)
```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Required Dependencies
```bash
pip install -r requirements.txt
```

### 4. NLTK Data Check
The project relies on NLTK components (like stopwords and wordnet). Ensure that you have an `nltk_data` folder in the root path or that you have run:
```python
import nltk
nltk.download('stopwords')
nltk.download('wordnet')
nltk.download('punkt')
```

### 5. Running the Application
Start the Flask development server:
```bash
python app.py
```
The application will launch and be accessible at `http://localhost:5000` (or whichever port is defined).

## Usage

1. **Homepage (`/`)**: Use the main form to either provide a manual text block, upload a file, or paste an Amazon link.
2. **Analysis Result**: After clicking analyze, view the granular breakdown of individual reviews, alongside a statistical summary.
3. **History Sidebar**: Navigate back to past sentiment analyses using the history sidebar, which loads previous results instantly.

## Disclaimer

The Amazon Scraper relies on Selenium and Chrome WebDriver. Since Amazon frequently updates its DOM structure and utilizes anti-bot measures, the scraping script relies on smart scrolling and explicit waits. Heavy scraping should be strictly limited to avoid being rate-limited or blocked by the platform.
