📚 Content-Based Book Recommendation System
Overview
This project is a Content-Based Recommendation Engine built from scratch using Python, Pandas, and Scikit-Learn. Instead of relying on user ratings or purchase history (Collaborative Filtering), this system analyzes the actual text, attributes, and authors of the books to find mathematical similarities and recommend the best possible matches.

🚀 Features
Content-Based Filtering: Recommends books by analyzing a combination of the book's Author and Plot Features.
TF-IDF Vectorization: Converts raw text data into numerical matrices, penalizing common/useless words and highlighting unique identifying features.
Cosine Similarity: Calculates the mathematical distance (angle) between book vectors to find the Top 15 closest statistical matches across the entire database.
Hybrid Sorting: Takes the Top 15 most similar books and applies a secondary sort based on the highest rating, ensuring recommendations are both highly relevant and high quality.
Memory Optimization: Designed to calculate vector similarities "on the fly" for specific search queries, bypassing the OOM (Out of Memory) crashes associated with building massive NxN correlation grids.
🛠️ Data Cleaning & Edge Case Handling
Intelligent Deduplication: Drops duplicate entries based on a combined ['title', 'author'] subset to prevent false duplicates (e.g., two different books with the same title).
Index Alignment: Safely resets Pandas indices after dropping NA values/duplicates to prevent "Index Out of Range" errors during Matrix traversal.
Empty Result Protections: Uses data validation (len() == 0 and .empty checks) to gracefully handle typos, nonexistent books, or aggressively filtered datasets without crashing the program.
💻 Tech Stack
Python: The core programming language.
Pandas: For loading datasets, manipulating DataFrames, data cleaning, and filtering output.
Scikit-Learn (sklearn): Used for Natural Language Processing (TF-IDF) and mathematical distance calculations (Cosine Similarity).
📖 How it Works (The Math)
Text Aggregation: The author and feature columns are cleaned (lowercased, spaces removed from names) and merged into a single tags string.
Vectorization: TfidfVectorizer reads the tags for every book and converts them into an array of context-weighted numbers, dropping standard English stop-words.
Similarity Calculation: When a user queries a book, cosine_similarity measures the angle between the queried book's vector and the vectors of every other book in the dataset. A score of 1.0 means an exact match.
Filtering & Output: The system isolates the 15 highest-scoring matches, drops duplicate titles from the subset, sorts the remainder by their public rating, and returns the absolute Top 5 best choices to the user.