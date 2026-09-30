# Smart Search Engine

A domain-specific Information Retrieval (IR) based search engine for searching UIC (University of Illinois Chicago) webpages.

The project uses **TF-IDF, Cosine Similarity, and PageRank** to retrieve and rank relevant webpages. A Flask web application provides a simple interface where users can enter a query and receive the top 10 ranked results.

---

## 📌 Project Overview

The Smart Search Engine follows a classical Information Retrieval pipeline:

```text
User Query
    ↓
Query Preprocessing
    ↓
TF-IDF Representation
    ↓
Cosine Similarity
    ↓
Top 200 Relevant Pages
    ↓
PageRank Re-ranking
    ↓
Top 10 Results
    ↓
Flask Web Interface
```

The repository contains precomputed TF-IDF and PageRank data, so **you do not need to crawl the UIC website or rebuild the complete index just to run the search engine**.

---

## ✨ Features

* Domain-specific webpage search
* Query preprocessing using NLTK
* Stopword removal
* Tokenization and stemming
* TF-IDF based document representation
* Cosine Similarity based retrieval
* PageRank based result ranking
* Top 10 search results
* Simple Flask web interface
* Runs locally on Windows/Linux/macOS
* No database required
* No API key required
* No external API required for normal search

---

## 🧠 Information Retrieval Concepts Used

### 1. Document Collection

The original project works with webpages from the UIC domain.

The repository contains the precomputed data required for searching, so live crawling is not required for normal execution.

### 2. Text Preprocessing

User queries are processed using NLTK.

The preprocessing pipeline includes:

* Lowercasing
* Tokenization
* Stopword removal
* Stemming
* Basic text cleaning

### 3. TF-IDF

TF-IDF (Term Frequency-Inverse Document Frequency) is used to represent documents and queries numerically.

It helps determine how important a term is within a document relative to the complete document collection.

### 4. Cosine Similarity

The query vector is compared with document TF-IDF vectors using Cosine Similarity.

The system first retrieves the most relevant candidate webpages based on their similarity to the query.

### 5. PageRank

PageRank is used as a link-based ranking signal.

After retrieving relevant candidate webpages, their precomputed PageRank scores are used to improve the final ordering.

### 6. Final Ranking

The system:

1. Retrieves the top 200 candidate webpages using Cosine Similarity.
2. Uses PageRank scores to rank those candidates.
3. Returns the top 10 webpages.

---

# 📂 Project Structure

The important files/directories are:

```text
SMART-SEARCH-ENGINE/
│
├── search_engine_web_app.py
├── search.py
├── cosine_similarity.py
├── queries_cleaning_processing.py
│
├── tf_idf_files/
│   ├── idf.json
│   ├── tf_idf.zip
│   └── tf_idf.json
│
├── web_page_ranks/
│   └── web_ranks.json
│
├── sample_queries/
│   └── sample_query_examples
│
├── templates/
│   ├── query_page.html
│   └── result.html
│
├── requirements.txt
└── README.md
```

### Main files

| File                             | Purpose                           |
| -------------------------------- | --------------------------------- |
| `search_engine_web_app.py`       | Flask web application             |
| `search.py`                      | Main search and ranking logic     |
| `cosine_similarity.py`           | Cosine similarity based retrieval |
| `queries_cleaning_processing.py` | Query preprocessing               |
| `tf_idf_files/tf_idf.json`       | Precomputed TF-IDF data           |
| `tf_idf_files/idf.json`          | IDF information                   |
| `web_page_ranks/web_ranks.json`  | Precomputed PageRank scores       |
| `templates/query_page.html`      | Search page                       |
| `templates/result.html`          | Search results page               |

---

# 💻 Requirements

You need:

* Python 3.8+ recommended
* pip
* Git

The project has been tested locally with Python 3.12.

No GPU is required.

No database is required.

No API key is required.

---

# 🚀 Installation & Setup

## 1. Clone the repository

```bash
git clone https://github.com/VETURISRIRAM/SMART-SEARCH-ENGINE.git
```

Move into the project directory:

```bash
cd SMART-SEARCH-ENGINE
```

Depending on how the repository is extracted/cloned, make sure you are inside the directory containing:

```text
search_engine_web_app.py
search.py
cosine_similarity.py
```

You can verify with:

### Windows PowerShell

```powershell
dir
```

---

## 2. Create a virtual environment

### Windows

```powershell
py -m venv .venv
```

Activate it:

```powershell
.\.venv\Scripts\Activate.ps1
```

You should see:

```text
(.venv) PS C:\...\SMART-SEARCH-ENGINE>
```

### macOS/Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

---

## 3. Install dependencies

If `pip` is available directly:

```bash
pip install -r requirements.txt
```

If Windows blocks `pip.exe`, use:

```powershell
python -m pip install -r requirements.txt
```

For the current Flask application, the required packages include:

```powershell
python -m pip install flask nltk
```

---

# 📦 4. Download NLTK Resources

Run:

```powershell
python -c "import nltk; nltk.download('stopwords'); nltk.download('punkt'); nltk.download('punkt_tab')"
```

The following resources are required:

```text
stopwords
punkt
punkt_tab
```

---

# 🗜️ 5. Extract the TF-IDF Data

The repository contains the compressed TF-IDF data:

```text
tf_idf_files/tf_idf.zip
```

Extract it into the same directory:

### Windows PowerShell

```powershell
tar -xf "./tf_idf_files/tf_idf.zip" -C "./tf_idf_files"
```

After extraction, verify that this file exists:

```text
tf_idf_files/tf_idf.json
```

The search engine requires the extracted TF-IDF file at:

```text
./tf_idf_files/tf_idf.json
```

---

# ▶️ 6. Run the Search Engine

From the project root directory:

```powershell
python search_engine_web_app.py
```

If you are using the Windows Python launcher:

```powershell
py search_engine_web_app.py
```

You should see something similar to:

```text
* Serving Flask app 'search_engine_web_app'
* Debug mode: on
* Running on http://127.0.0.1:8000
```

---

# 🌐 7. Open the Web Application

Open your browser and visit:

```text
http://127.0.0.1:8000
```

You should see the Smart Search Engine interface.

Enter a query and click **Search**.

Example queries:

```text
engineering research
```

```text
admissions
```

```text
library
```

```text
tuition fees
```

The application returns the top ranked webpages for the query.

---

# 🔍 How the Search Works

Suppose the user searches:

```text
engineering research
```

### Step 1 — Query Processing

The query is cleaned and tokenized.

```text
engineering research
        ↓
Tokenization
        ↓
Stopword removal
        ↓
Stemming
```

### Step 2 — TF-IDF

The processed query is represented using TF-IDF.

The project already contains precomputed TF-IDF information for the indexed webpages.

### Step 3 — Cosine Similarity

The query vector is compared with document vectors.

Conceptually:

```text
Query
  ↓
TF-IDF Vector
  ↓
Compare with document vectors
  ↓
Cosine Similarity
  ↓
Top 200 candidate webpages
```

### Step 4 — PageRank

The candidate webpages are then ranked using their precomputed PageRank scores.

```text
Top 200 Candidates
        ↓
PageRank Scores
        ↓
Ranking
        ↓
Top 10 Results
```

### Step 5 — Display Results

The Flask application displays the final URLs in the browser.

---

# 🏗️ Architecture

```text
                    ┌─────────────────┐
                    │     User        │
                    │      Query      │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ Flask Web App   │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ Query           │
                    │ Preprocessing   │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ TF-IDF Query    │
                    │ Representation  │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ Cosine          │
                    │ Similarity      │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ Top 200         │
                    │ Candidates     │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ PageRank        │
                    │ Re-ranking      │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ Top 10 Results  │
                    └────────┬────────┘
                             ↓
                    ┌─────────────────┐
                    │ Flask Result UI │
                    └─────────────────┘
```

---

# 📊 Data Used by the Search Engine

The search-time implementation uses precomputed data.

### TF-IDF data

```text
tf_idf_files/tf_idf.json
```

### IDF data

```text
tf_idf_files/idf.json
```

### PageRank data

```text
web_page_ranks/web_ranks.json
```

The repository contains the data necessary for the normal search workflow.

Therefore:

* ❌ No live crawling required
* ❌ No database setup required
* ❌ No API key required
* ❌ No cloud service required
* ❌ No GPU required

---

# 🛠️ Troubleshooting

## `pip` is blocked on Windows

If this:

```powershell
pip install ...
```

produces an Application Control error, use:

```powershell
python -m pip install ...
```

or:

```powershell
py -m pip install ...
```

---

## `LookupError: Resource stopwords not found`

Run:

```powershell
python -c "import nltk; nltk.download('stopwords')"
```

---

## `LookupError: Resource punkt not found`

Run:

```powershell
python -c "import nltk; nltk.download('punkt')"
```

---

## `LookupError: Resource punkt_tab not found`

Run:

```powershell
python -c "import nltk; nltk.download('punkt_tab')"
```

Or download all required resources together:

```powershell
python -c "import nltk; nltk.download('stopwords'); nltk.download('punkt'); nltk.download('punkt_tab')"
```

---

## `FileNotFoundError: tf_idf.json`

Make sure you have extracted:

```text
tf_idf_files/tf_idf.zip
```

using:

```powershell
tar -xf "./tf_idf_files/tf_idf.zip" -C "./tf_idf_files"
```

Then verify:

```text
tf_idf_files/tf_idf.json
```

exists.

---

## Flask application does not start

Make sure you are running the command from the directory containing:

```text
search_engine_web_app.py
```

Then run:

```powershell
py search_engine_web_app.py
```

---

# 🧪 Testing

After starting the application, test with queries such as:

```text
engineering research
```

```text
admissions
```

```text
library
```

```text
tuition fees
```

The application should return a ranked list of webpages.

---

# ⚙️ Rebuilding the Search Data

The repository also contains source/data-generation related scripts for rebuilding the search data from webpages.

These are **not required for normal local execution**.

Examples include scripts related to:

* Web crawling
* HTML cleaning
* Document generation
* Inverted index construction
* Web graph generation
* PageRank calculation
* TF-IDF generation

If your goal is simply to run and demonstrate the search engine, use the precomputed data instead.

---

# 🎓 WAIR / Information Retrieval Concepts Demonstrated

This project demonstrates the following Information Retrieval concepts:

* Web crawling / document collection
* Document preprocessing
* Tokenization
* Stopword removal
* Stemming
* Inverted indexing
* TF-IDF
* Vector Space Model
* Cosine Similarity
* PageRank
* Query processing
* Document ranking
* Search result presentation

---

# 📈 Example Search Flow

For a query such as:

```text
machine learning research
```

the system performs:

```text
"machine learning research"
             ↓
       Query Cleaning
             ↓
        Tokenization
             ↓
      Stopword Removal
             ↓
          Stemming
             ↓
        TF-IDF Vector
             ↓
    Cosine Similarity Search
             ↓
       Top 200 Pages
             ↓
      PageRank Re-ranking
             ↓
        Top 10 Pages
```

---

# 🚫 What This Project Does Not Require

For the normal search workflow, you do **not** need:

* OpenAI API
* Gemini API
* Pinecone
* MongoDB
* MySQL
* PostgreSQL
* Docker
* GPU
* Live web crawling
* Cloud deployment

The project is designed to run locally using the precomputed search data.

---

# 👨‍💻 Author

Developed by **Nilesh Yadav**

---

# 📄 License

See the repository for the applicable project/license information.
