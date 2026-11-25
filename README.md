# ComplyBot — FAQ-grounded compliance chatbot

A mobile-friendly Streamlit web app for general Indian GST, TDS and company-filing FAQs. It retrieves relevant FAQ entries with TF-IDF, sends only those entries to Groq for a concise explanation, and displays the FAQ/source references used. It has a low-relevance fallback.

## Run locally

1. Install Python 3.10+.
2. Create and activate a virtual environment.
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Create `.streamlit/secrets.toml`:

   ```toml
   GROQ_API_KEY = "gsk_your_key_here"
   ```

5. Start the app:

   ```bash
   streamlit run app.py
   ```

Never commit your API key. `.streamlit/secrets.toml` is ignored by Git.

## Deploy on Streamlit Community Cloud

1. Create a GitHub repository and upload the project files.
2. Go to https://share.streamlit.io/ and sign in with GitHub.
3. Select **Create app**, choose your repository, branch and `app.py`.
4. Open **Advanced settings / Secrets** before deploying (or the app's settings after creation).
5. Add:

   ```toml
   GROQ_API_KEY = "gsk_your_key_here"
   ```

6. Deploy. Streamlit installs packages from `requirements.txt`.

## Customize the FAQ knowledge base

Edit `data/faqs.json`. Each entry must contain:
- `id`: unique reference such as `GST-005`
- `category`
- `question`
- `answer`
- `source_name`
- `source_url`
- `last_verified` (YYYY-MM-DD)

Use official, current sources. Review and update compliance content regularly. The starter FAQs are general orientation material, not a complete or legally reviewed compliance database.

## Important limitations and safety

- Retrieval uses TF-IDF similarity, not semantic embeddings. Tune the threshold in `app.py` and test with real questions.
- Groq generates a plain-language response only from retrieved FAQ context. The model can still make mistakes; source links and professional review remain important.
- This is not legal, tax, accounting or company-secretarial advice.
- Do not add client PANs, GSTINs, financial records, passwords or other confidential personal/business data.
- Do not treat the relevance score as a legal confidence score.
- Confirm all filing dates, rates, thresholds, exemptions, forms and penalties against current official sources before publishing.

## Project structure

```text
complybot/
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
├── .streamlit/
│   └── secrets.toml.example
└── data/
    └── faqs.json
```
