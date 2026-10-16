# Review Lens — Multi-Platform Product Review Sentiment Analyzer

Review Lens is a machine-learning project that analyzes product reviews across multiple e-commerce platforms. It classifies reviews as **Positive, Neutral, or Negative** and provides insights into customer sentiment, product performance, and review trends.

## Features

- **Sentiment Analysis:** Classifies customer reviews into positive, neutral, and negative sentiment.
- **Machine Learning:** Compares multiple classifiers and selects a model using evaluation metrics.
- **Product Analytics:** Analyzes customer sentiment and review patterns for individual products.
- **Platform Comparison:** Examines reviews across different e-commerce platforms.
- **Product Comparison:** Compares sentiment and feedback across products.
- **Review Search:** Searches reviews using keywords and available filters.
- **AI-Generated Insights:** Supports optional AI summaries through OpenRouter.
- **REST API:** Provides endpoints through FastAPI, with interactive Swagger documentation.

## Technology Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Backend Framework | FastAPI |
| Machine Learning | Scikit-learn |
| NLP / Feature Extraction | TF-IDF |
| Data Processing | Pandas, NumPy |
| AI Integration | OpenRouter API |
| Frontend | HTML, CSS, JavaScript |
| API Server | Uvicorn |

## Project Structure

```text
review-lens/
├── readme.md
├── frontend/
│   └── index.html
└── backend/
    ├── README.md
    ├── app/
    ├── ml/
    ├── utils/
    ├── data/
    ├── tests/
    ├── pyproject.toml
    ├── uv.lock
    └── run.py
```

## Getting Started

### Prerequisites

- Python 3.10 or newer
- `uv` package manager
- Git

### 1. Clone the repository

```bash
git clone https://github.com/Manish-cdr/review-lens
cd review-lens
```


### 2. Install backend dependencies

```bash
cd backend
uv sync
```

### 3. Prepare the dataset

The backend expects the dataset at:

```text
backend/data/reviews.csv
```

If the CSV is not included in the repository, generate it using `backend/utils/generate_dataset.py`. Ensure the generator writes the file to the expected location.

The generated dataset is synthetic demonstration data, not a verified collection of real customer reviews.

### 4. Start the backend

From the `backend` directory, run:

```bash
uv run uvicorn app.main:app --reload --port 8000
```

### 5. Access the API

Once the server is running:

- **Swagger UI:** http://localhost:8000/docs
- **ReDoc:** http://localhost:8000/redoc
- **Health Check:** http://localhost:8000/health

### 6. Open the frontend

Open `frontend/index.html` in your browser. Keep the backend running at `http://localhost:8000` unless you update the frontend's API configuration.

## Machine Learning Workflow

1. Load and prepare the review dataset.
2. Process review text using TF-IDF feature extraction.
3. Train and compare candidate machine-learning classifiers.
4. Evaluate models using metrics such as macro F1 score.
5. Select and save the best-performing model.
6. Use the trained model for sentiment predictions and product-level analysis.

## Evaluation Considerations

The project uses synthetic review data for demonstration. Repeated text patterns can lead to artificially high evaluation scores. These scores should not be interpreted as real-world performance without testing on an independent, representative dataset.

## Configuration

AI-generated insights require an OpenRouter API key. Store the key in a local environment file and never commit API keys, passwords, or other secrets to GitHub.

## Future Improvements

- Evaluate models on real, independently labeled customer reviews.
- Improve duplicate detection and prevent data leakage during evaluation.
- Expand automated testing.
- Improve frontend configuration and deployment.
- Add further product and platform analytics.

## Author

**Manish Sharma**

This project demonstrates the application of machine learning, natural language processing, and API development to product-review analysis.
