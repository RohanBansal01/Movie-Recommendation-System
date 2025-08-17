
---

# Movie Recommendation System 🎬

[![License: MIT](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Python Version](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Repo-black?logo=github)](https://github.com/YourUsername/Movie-Recommendation-System)

A **content-based movie recommendation engine** built with Python and machine learning. The system recommends movies by finding titles with similar attributes such as genres, keywords, cast, and crew. Recommendations are generated using textual similarity between movies, providing a personalized viewing experience.

---

## 📌 Project Overview

This project builds a movie recommendation system from scratch using [The Movie Database (TMDB)](https://www.themoviedb.org/) datasets. Steps include:

1. **Data Acquisition & Preprocessing**

   * Merge `tmdb_5000_movies.csv` and `tmdb_5000_credits.csv`.
   * Parse JSON-like strings to extract genres, keywords, cast, and crew.

2. **Feature Vectorization**

   * Combine movie attributes into a single string.
   * Use `CountVectorizer` (Bag-of-Words) to convert text into numerical vectors.

3. **Similarity Measurement**

   * Compute cosine similarity between movie vectors.
   * Scores closer to 1 indicate higher similarity.

4. **Recommendation Generation**

   * Sort movies by similarity scores.
   * Return top 5 recommended titles for a given movie.

---

## 🗂 Key Files

* `tmdb_5000_movies.csv` & `tmdb_5000_credits.csv` – raw datasets.
* `movie_dict.pkl` – preprocessed movie data (IDs, titles, combined tags).
* `similarity.pkl` – precomputed cosine similarity matrix.
* Jupyter Notebook / Python scripts – data processing and recommendation logic.

---

## ⚡ Installation

1. Clone the repository:

```bash
git clone https://github.com/YourUsername/Movie-Recommendation-System.git
cd Movie-Recommendation-System
```

2. Install dependencies:

```bash
pip install pandas numpy scikit-learn nltk
```

---

## 🏃 How to Use

Load the pre-saved data and generate recommendations:

```python
import pickle
import pandas as pd

# Load data
movies_list = pickle.load(open('movie_dict.pkl', 'rb'))
similarity = pickle.load(open('similarity.pkl', 'rb'))
movies = pd.DataFrame(movies_list)

# Recommendation function
def recommend(movie):
    try:
        movie_index = movies[movies['title'] == movie].index[0]
        distances = sorted(list(enumerate(similarity[movie_index])), reverse=True, key=lambda x: x[1])
        print(f"Recommendations for '{movie}':\n")
        for i in distances[1:6]:
            print(movies.iloc[i[0]].title)
    except IndexError:
        print(f"Sorry, '{movie}' not found in the database.")

# Example
recommend('The Dark Knight Rises')
```

**Sample Output:**

```
Recommendations for 'The Dark Knight Rises':

The Dark Knight
Batman Begins
Amidst the Maelstrom
Batman Returns
The Prestige
```

---

## 📈 Features

* Content-based recommendations using genres, keywords, cast, crew, and overview.
* Efficient lookup using a precomputed similarity matrix.
* Easy to extend with additional NLP or collaborative filtering techniques.

---

## 🤝 Contributing

1. Fork the repository
2. Create a new branch (`git checkout -b feature-name`)
3. Make your changes and commit (`git commit -m "Add feature"`)
4. Push to the branch (`git push origin feature-name`)
5. Open a Pull Request

---

## 📝 License

This project is licensed under **MIT License** – see the [LICENSE](LICENSE) file for details.

---

