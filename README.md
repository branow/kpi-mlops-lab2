# Iris ML API — Lab 2

![CI](https://github.com/branow/kpi-mlops-lab2/actions/workflows/ci.yml/badge.svg)

REST API for Iris flower classification built with FastAPI, containerized with Docker, and deployed to Render.

## Tech Stack

- **FastAPI** — REST API framework
- **scikit-learn** — Logistic Regression classifier
- **joblib** — model serialization
- **Docker** — containerization
- **GitHub Actions** — CI/CD
- **Render** — cloud deployment

## Project Structure

```
├── app/
│   ├── main.py        # FastAPI application
│   └── schemas.py     # Pydantic request/response models
├── ml/
│   └── train.py       # Model training script
├── tests/
│   ├── test_model.py  # Model unit tests
│   └── test_api.py    # API endpoint tests
├── Dockerfile
├── .github/workflows/ci.yml
└── requirements.txt
```

## Run Locally

```bash
# Install dependencies
uv venv --python 3.12
uv pip install -r requirements.txt

# Train the model
uv run python -m ml.train

# Start the API
uv run uvicorn app.main:app --reload
```

API available at `http://localhost:8000/docs`

## Run with Docker

```bash
docker build --network host -t ml-api:lab2 .
docker run --rm --network host ml-api:lab2
```

## Run Tests

```bash
uv run pytest -q
```

## API Endpoints

| Method | Endpoint   | Description          |
|--------|------------|----------------------|
| GET    | `/`        | Service status       |
| GET    | `/health`  | Health check         |
| POST   | `/predict` | Classify Iris flower |

### Example Request

```bash
curl -X POST http://localhost:8000/predict \
  -H "Content-Type: application/json" \
  -d '{"sepal_length": 5.1, "sepal_width": 3.5, "petal_length": 1.4, "petal_width": 0.2}'
```

### Example Response

```json
{
  "class_id": 0,
  "class_name": "setosa",
  "probability": 0.9998
}
```

## Live Demo

**https://kpi-mlops-lab2.onrender.com**

> Note: the free Render tier sleeps after inactivity — first request may take ~30s to wake up.
