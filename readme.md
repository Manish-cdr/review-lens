# Review Lens — Multi-Platform Review Sentiment Analysis

Review Lens is a machine learning-based application that analyzes customer reviews across **7 e-commerce platforms and 60 products**. It classifies review sentiment, compares machine learning models, and provides product-level insights to help users understand customer feedback.

## Features

- **Sentiment Analysis:** Classifies customer reviews as Positive, Neutral, or Negative using a machine learning model.
- **Model Comparison:** Evaluates 10 classification algorithms and selects the best-performing model based on macro F1-score.
- **Product Analytics:** Provides sentiment scores, rating distributions, and review summaries for individual products.
- **Platform Comparison:** Analyzes customer feedback across different e-commerce platforms.
- **Review Insights:** Displays top reviews and highlights customer sentiment patterns.
- **Monthly Trends:** Tracks sentiment changes over time.
- **AI-Powered Summaries:** Supports optional AI-generated product insights and comparison summaries through OpenRouter.
- **REST API:** Exposes application functionality through a FastAPI backend.

## Tech Stack

| Category | Technologies |
|---|---|
| Language | Python |
| Backend | FastAPI, Uvicorn |
| Machine Learning | scikit-learn |
| Data Processing | pandas, NumPy |
| Model Evaluation | Accuracy, Macro F1-score, Cross-validation |
| AI Integration | OpenRouter API |
| Testing | pytest |

## Project Structure

```text
review-lens/
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── routers.py
│   │   └── ai_client.py
│   ├── ml/
│   │   ├── pipeline.py
│   │   └── model_comparison.py
│   ├── utils/
│   │   └── generate_dataset.py
│   ├── data/
│   │   ├── reviews.csv
│   │   └── models/
│   ├── tests/
│   ├── pyproject.toml
│   ├── uv.lock
│   └── run.py
├── frontend/
│   └── index.html
├── .env.example
├── .gitignore
└── README.md
```

*Note: The structure above describes the main expected files. Adjust it if your repository uses different filenames or folders.*

## Getting Started

### Prerequisites

Install the following before running the project:

- Python 3.11 or a compatible Python version supported by the project dependencies
- [uv](https://docs.astral.sh/uv/getting-started/installation/)
- Git

Verify your installations:

```bash
python --version
uv --version
git --version
```

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/review-lens.git
cd review-lens
```

Replace `YOUR-USERNAME` with your GitHub username.

### 2. Navigate to the Backend

```bash
cd backend
```

### 3. Install Dependencies

Install the project dependencies using `uv`:

```bash
uv sync
```

This creates or updates the project's virtual environment and installs the dependencies declared in `pyproject.toml` and `uv.lock`.

### 4. Configure Environment Variables

AI-powered features are optional. If you want to use them, copy the example environment file:

**Windows PowerShell**

```powershell
Copy-Item .env.example .env
```

**macOS/Linux**

```bash
cp .env.example .env
```

Add your OpenRouter API key to `.env` using the variable name expected by the application. For example, if the code reads `OPENROUTER_API_KEY`:

```env
OPENROUTER_API_KEY=your_api_key_here
```

Never commit your `.env` file or expose API keys in source code.

If you do not configure an API key, the local machine learning sentiment analysis features can still work, provided the dataset and model dependencies are available. AI-powered features that require OpenRouter will not be available.

### 5. Prepare the Dataset

The application expects the review dataset at:

```text
backend/data/reviews.csv
```

If the dataset is not included in the repository, generate it using the provided script:

```bash
uv run python utils/generate_dataset.py
```

Run this command from the `backend` directory.

The generator may create synthetic review data for development and testing. Synthetic data is not a substitute for real customer reviews and should not be used to claim real-world model performance.

### 6. Start the Backend

From the `backend` directory, run:

```bash
uv run python run.py --reload
```

Alternatively, if you prefer to start the FastAPI application directly:

```bash
uv run uvicorn app.main:app --reload --port 8000
```

The API should be available at:

- **Application:** http://localhost:8000
- **Interactive API documentation:** http://localhost:8000/docs
- **Health check:** http://localhost:8000/health

Keep the terminal running while using the application.

### 7. Open the Frontend

Open `frontend/index.html` in your browser.

If the frontend cannot communicate with the backend when opened directly from the filesystem, serve it through a local HTTP server or configure the frontend to use the correct backend API URL. Ensure that the frontend's API base URL matches the running backend.

## Running Tests

From the `backend` directory, run:

```bash
uv run pytest tests/ -v
```

This executes the project's test suite with verbose output.

## Machine Learning Workflow

Review Lens uses the following general workflow:

1. Load and validate the review dataset.
2. Remove duplicate reviews where required.
3. Prepare the text and sentiment labels.
4. Split the data into training and testing sets.
5. Train and compare 10 classification algorithms.
6. Evaluate models using accuracy and macro F1-score, along with cross-validation.
7. Select the best-performing model and save it for subsequent predictions.
8. Use the selected model to analyze reviews and generate product-level insights.

The model comparison process helps evaluate different algorithms under the same experimental setup.

**Evaluation note:** Model performance depends on the dataset and its quality. Scores obtained from synthetic data may be unusually high and should not be interpreted as evidence of equivalent performance on real-world reviews.

## API Overview

The backend exposes REST endpoints for product data, platform data, machine learning analysis, and AI-generated insights.

Examples of available endpoints in the current application include:

| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/` | Application root |
| GET | `/health` | Health check |
| GET | `/api/v1/data/products` | Retrieve product data |
| GET | `/api/v1/data/platforms` | Retrieve platform data |
| POST | `/api/v1/ml/analyze` | Analyze review sentiment |

For request parameters, response schemas, and additional endpoints, start the backend and visit [http://localhost:8000/docs](http://localhost:8000/docs).

## Dataset and Limitations

- The project supports analysis of reviews associated with 60 products and 7 platforms in its generated dataset.
- Synthetic reviews are intended for development and demonstration.
- Repeated or templated review text can introduce data leakage or make classification artificially easy.
- Model metrics should be validated on a representative, independently collected dataset before drawing conclusions about real customer behavior.
- AI-generated summaries require an appropriate OpenRouter configuration and may depend on API availability and usage limits.

## Security

- Keep API keys in environment variables.
- Do not commit `.env` files, credentials, or private configuration.
- Exclude virtual environments, caches, and generated model artifacts from Git unless there is a specific reason to version them.
- Review dataset licensing and privacy before publishing real customer reviews.

## Future Improvements

- Evaluate models using real-world, independently labeled customer reviews.
- Add stronger data validation and preprocessing.
- Improve multilingual sentiment analysis.
- Add more detailed cross-platform comparisons.
- Expand automated tests and model monitoring.
- Improve frontend error handling and API integration.

## License

Choose a license before distributing or reusing this project. If you intend to make the project open source, consider adding an appropriate `LICENSE` file.

---

**Developed as a machine learning project for multi-platform customer review analysis.**
