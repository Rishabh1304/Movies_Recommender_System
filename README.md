# Movies_Recommender_System

A fully functional, high-performance **Content-Based Movie Recommender System** that accurately predicts and suggests the top 5 similar movies based on a user's selection. This project delivers a production-ready, cloud-deployed web application with a responsive user interface and dynamic, real-time data fetching.

👉 **Live Production URL:** [Paste your share.streamlit.io link here]

---

## 📌 Project Overview (Quick Summary)
If you are looking for a quick breakdown of this project, here is everything you need to know at a glance:
- **Core Purpose:** To recommend 5 movies most similar to a user's chosen film using advanced text vectorization and distance calculation metrics.
- **Dynamic Interface:** Built entirely with Streamlit, optimized in a wide-screen layout, showing movie names along with their official high-quality posters.
- **Real-Time Data Integration:** Instead of storing static images locally, the system performs live API calls to **The Movie Database (TMDB)** servers to pull the latest official movie posters dynamically on click.
- **Production Optimization (The 180MB Architecture Hack):** Standard implementations require uploading a massive pre-computed similarity matrix file (~180MB), which breaks GitHub's 100MB file limit. This project solves that production constraint by calculating the text vectorization and similarity matrix *live in memory* on the Streamlit cloud server within 2 seconds of the application initialization, rendering a 100% lightweight and clean codebase.

---

## 🛠️ Complete Tech Stack & Tools
This pipeline is engineered using industry-standard Data Science and Web Development frameworks:
- **Programming Language:** Python 3.x
- **Machine Learning & NLP:** Scikit-Learn (`CountVectorizer`, `cosine_similarity`)
- **Data Wrangling & Analytics:** Pandas & NumPy
- **Object Serialization:** Pickle (for lightweight metadata storage)
- **Frontend / UI Architecture:** Streamlit (Web Framework)
- **Networking & API Integration:** Requests Library (REST API integration with TMDB)
- **Development & DevOps Ecosystem:** Google Colab, VS Code, GitHub, Streamlit Cloud

---

## 🧠 Core System Architecture & Logic

The project consists of an end-to-end Machine Learning pipeline broken down into four distinct phases:

### 1. Exploratory Data Analysis & Feature Engineering (Google Colab)
- Processed raw metadata for over 4,800 movies, handling missing records and structured string manipulations.
- Extracted critical text-based features including genres, plot keywords, lead cast members, directors, and production crew summaries.
- Cleaned and tokenized individual elements (removing spaces between names, e.g., "Johnny Depp" to "JohnnyDepp") to prevent vectorization confusion.
- Combined all textual features into a single, comprehensive metadata string column named `tags`.

### 2. NLP Vectorization (Bag-of-Words Model)
- Utilized Scikit-Learn's `CountVectorizer` to convert unstructured text strings into mathematical coordinate arrays.
- Restricted the vocabulary to the top **5,000 most frequent words** while filtering out standard English stop words (`and`, `the`, `is`, etc.) to isolate contextually meaningful keywords.

### 3. Mathematical Similarity Scoring
- Applied **Cosine Similarity** to evaluate the multi-dimensional distances between different movie vectors.
- Calculated the dot product of normalized vectors to generate a relational score ranging between 0 and 1. When a user queries a movie, the system sorts the distances in descending order and isolates the top 5 closest data points.

### 4. Dynamic Poster Pipeline
- The system captures the unique TMDB ID associated with the recommended titles.
- It automatically triggers an asynchronous HTTPS request to the TMDB API (`https://api.themoviedb.org/3/movie/{movie_id}`), extracts the correct `poster_path`, and renders the full-bleed visual layout securely on the user screen.

---

## 📂 Repository Structure
```text
├── app.py                  # Main Streamlit web application script
├── movies.pkl              # Serialized Python dictionary containing processed movie metadata
├── movie_recommender.ipynb # Comprehensive Google Colab notebook documenting EDA, data cleaning, and model testing
├── requirements.txt        # Production configuration file detailing explicit Python dependencies
└── README.md               # Definitive project documentation and system overview
