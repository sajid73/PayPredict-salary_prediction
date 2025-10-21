// ...existing code...

# PayPredict — Software Developer Salary Prediction

Small Streamlit app that predicts software developer salaries using Stack Overflow Developer Survey data and a trained regression model.

## Repository structure
- `app.py` — Streamlit entry point that selects pages.
- `predict_page.py` — Prediction UI and model loader. See `predict_page.load_model` and `predict_page.show_predict_page`.
- `explore_page.py` — Data exploration UI and preprocessing helpers. See `explore_page.load_data`, `explore_page.shorten_categories`, `explore_page.clean_experience`, and `explore_page.clean_education`.
- `notebook/SalaryPrediction.ipynb` — Prototype notebook used to train the model and produce the saved preprocessing / model objects.
- `utils/survey_results_public_2022.csv` — Survey dataset (source file used for analysis).
- `requirements.txt` — Python dependencies.
- (Optional) `models/` or `model.pkl` — Serialized model + encoders produced by the notebook (place where `predict_page.load_model` expects them).

## Quick start

1. Create a virtual environment and install dependencies:
```sh
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

2. Run the Streamlit app:
```sh
streamlit run app.py
```

3. Open the app in the host browser (from inside the dev container):
```sh
$BROWSER http://localhost:8501
```

## Notes / Tips
- The explorer page uses the loader in `explore_page.load_data`. Ensure the dataset filename referenced there matches the actual CSV at `utils/survey_results_public_2022.csv`.
- The predictor expects a serialized model + encoders produced by the notebook (`notebook/SalaryPrediction.ipynb`). The notebook demonstrates how to save the preprocessing objects and regression model (typically via `pickle`). Place the saved object(s) where `predict_page.load_model` will find them (update the path in that function if needed).
- If you retrain the model in the notebook, save the resulting object(s) to the project (for example `models/model.pkl`) so `predict_page.load_model` can load them.

## Development
- Modify UI logic in `predict_page.py` and `explore_page.py`.
- Re-run the notebook (`notebook/SalaryPrediction.ipynb`) to regenerate the model after changes to preprocessing or feature selection.
- Add unit tests for preprocessing helpers and prediction logic where appropriate.

## Troubleshooting
- If Streamlit fails to start, verify dependencies were installed from `requirements.txt`.
- If the dataset fails to load, confirm the path in `explore_page.load_data` matches `utils/survey_results_public_2022.csv`.
- If model loading fails, check the serialized model filename and format (pickle) and update `predict_page.load_model` accordingly.
