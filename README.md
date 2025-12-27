# 🎬 Movie Recommendation System Using Biclustering

A Python-based recommendation system that applies biclustering techniques to identify subgroups of users and movies with similar rating patterns, enabling personalized movie recommendations.

<img width="940" height="753" alt="image" src="https://github.com/user-attachments/assets/4b34a201-541d-4ddb-8d32-97d4ea92870a" />

---

## 📌 Project Overview

This project implements a **biclustering-based movie recommendation system** using the **Spectral Co-clustering** algorithm. The system simultaneously clusters users and movies to discover meaningful subgroups, allowing for personalized recommendations based on shared preferences within these clusters.

### Key Features:
- **Biclustering Implementation**: Identifies coherent user-movie subgroups using Spectral Co-clustering.
- **Personalized Recommendations**: Generates movie suggestions based on cluster-specific preferences.
- **Interactive Web Interface**: Built with Gradio for real-time recommendation generation.
- **Comprehensive Visualizations**: Includes heatmaps and genre distribution charts for cluster analysis.
- **Scalable Architecture**: Designed to handle large-scale user-item matrices (20k+ users × 18k+ movies).

---

## 📊 Dataset

**MovieLens 20M Dataset**  
Source: [Kaggle - MovieLens 20M Dataset](https://www.kaggle.com/datasets/grouplens/movielens-20m-dataset?select=rating.csv)

### Files Used:
1. **`ratings.csv`** - Contains 3,072,316 user ratings
   - Columns: `userId`, `movieId`, `rating`, `timestamp`
2. **`movies.csv`** - Contains 27,278 movie entries
   - Columns: `movieId`, `title`, `genres`

### Data Statistics:
| Metric | Value |
|--------|-------|
| **Total Users** | 20,948 |
| **Total Movies** | 18,211 |
| **Matrix Dimensions** | 20,948 × 18,211 |
| **Sparsity Level** | High |

---

## 🛠️ Installation & Setup

### Prerequisites
- Python 3.8+
- pip package manager

### 1. Clone the Repository
```bash
git clone <repository-url>
cd movie-recommendation-biclustering
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

**Requirements.txt:**
```
pandas==1.5.3
numpy==1.24.3
scikit-learn==1.3.0
matplotlib==3.7.1
seaborn==0.12.2
gradio==3.44.3
jupyter==1.0.0
```

### 3. Download Dataset
1. Download the MovieLens 20M dataset from [Kaggle](https://www.kaggle.com/datasets/grouplens/movielens-20m-dataset?select=rating.csv)
2. Extract the zip file and place `ratings.csv` and `movies.csv` in the `data/` directory

### 4. Run the Application
```bash
python main.py
```

For Jupyter Notebook users:
```bash
jupyter notebook
# Open Movie_Recommendation_System.ipynb
```

---

## 🚀 Usage

### 1. Data Preparation
The system loads and merges the datasets, creating a user-item matrix where:
- Rows represent users
- Columns represent movies
- Values represent ratings (0 = no rating)

### 2. Biclustering Model
```python
from sklearn.cluster import SpectralCoclustering

# Initialize model with 5 clusters
bicluster_model = SpectralCoclustering(n_clusters=5, random_state=42)
bicluster_model.fit(user_item_matrix)
```

### 3. Generate Recommendations
The system follows a 4-step recommendation process:
1. **Identify User's Bicluster** - Determine which cluster the user belongs to
2. **Filter Unrated Movies** - Select movies from the same bicluster not yet rated
3. **Calculate Average Ratings** - Compute average ratings from other users in the bicluster
4. **Rank and Recommend** - Sort movies by average rating and return top 5

### 4. Interactive Interface
Launch the Gradio web interface:
```bash
python app.py
```
Then open `http://localhost:7860` in your browser.

**Interface Features:**
- User ID input field (1-100 for demo)
- Real-time recommendation generation
- Movie titles with genres
- Bicluster membership information
- Cluster genre preferences

---

## 📈 Bicluster Analysis

The system identified 5 distinct biclusters:

| Cluster | Users | Movies | Top Genres | Avg Rating |
|---------|-------|--------|------------|------------|
| 1 | 3,281 | 7,372 | Drama, Comedy, Thriller | 3.59 |
| 2 | 0 | 7 | Documentary, Sci-Fi | N/A |
| 3 | 5,269 | 603 | Drama, Comedy, Thriller | 3.50 |
| 4 | 1 | 9 | Drama, Romance | 4.06 |
| 5 | 12,397 | 10,220 | Drama, Comedy, Romance | 3.54 |

### Key Insights:
- **Bicluster 5**: Mainstream audience (59% of users) preferring popular genres
- **Bicluster 4**: Single user with specific, highly-rated preferences
- **Bicluster 2**: Niche movies with no ratings in this dataset

---

## 📊 Visualizations

### 1. Genre Distribution
Bar chart showing top 10 genre preferences in each bicluster (e.g., Drama dominates Bicluster 5).
<img width="940" height="787" alt="image" src="https://github.com/user-attachments/assets/5785afea-c8f1-4909-beb2-3f03db5a7236" />


### 2. Heatmap Visualization
Heatmap displaying rating patterns for users × movies within biclusters:
- Darker areas indicate higher ratings
- Reveals localized patterns of user-movie preferences
  <img width="940" height="1259" alt="image" src="https://github.com/user-attachments/assets/f21d9ce8-08ab-4fc4-88ac-0f25f2f04e6d" />


---

## 🧪 Example Recommendation

**For User ID 1 (Bicluster 5):**
1. Diana Vreeland: The Eye Has to Travel (2011) - Documentary
2. Felony (2013) - Thriller
3. Gardens of the Night (2008) - Drama
4. Workingman's Death (2005) - Documentary
5. The Tall T (1957) - Western

*Note: Bicluster 5 often enjoys Drama, Comedy, and Romance genres*

---

## ⚠️ Limitations & Challenges

1. **Data Sparsity**: High sparsity (many zero ratings) affects clustering quality
2. **Cold-Start Problem**: New users/movies without ratings cannot be clustered
3. **Scalability Issues**: Large matrix size requires significant computation
4. **Over-clustering**: Some clusters contain very few users/movies
5. **Memory Constraints**: Full matrix operations require substantial RAM

---

## 🔮 Future Improvements

1. **Hybrid Approach**: Combine biclustering with collaborative/content-based filtering
2. **Dimensionality Reduction**: Apply PCA or SVD to handle sparsity
3. **Real-time Updates**: Implement incremental clustering for new users/ratings
4. **Performance Metrics**: Add RMSE, precision@k, recall@k for evaluation
5. **Cloud Deployment**: Deploy on AWS/GCP with scalable infrastructure


## 📚 References

1. Dhillon, I. S. (2001). Co-clustering documents and words using bipartite spectral graph partitioning.
2. MovieLens 20M Dataset: F. Maxwell Harper and Joseph A. Konstan. 2015. The MovieLens Datasets
3. Scikit-learn Documentation: Spectral Co-clustering
4. Gradio Documentation: Building ML Web Interfaces

