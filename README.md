# 🍷 Week 3 Task: Unsupervised Learning and Clustering Analysis

## 🎓 Yuva Intern / NSDC Internship Program

This repository contains my Week 3 submission for the Yuva Intern / NSDC internship. The task was to apply unsupervised machine learning techniques — specifically K-Means and Hierarchical (Agglomerative) Clustering — on a public dataset using Python and Scikit-learn, and to explain the results properly instead of just showing numbers.

## 🎯 Objective

The main goal of this task was to:
- 📥 Pick a public dataset and prepare it for clustering
- 🔢 Find the right number of clusters instead of guessing
- 🧩 Apply K-Means and Hierarchical Clustering separately
- 📊 Visualize the clusters so the grouping is easy to understand
- 🧠 Explain what each cluster actually means, and check if the results make sense

## 📂 Dataset Used

I used the **Wine dataset** from the UCI Machine Learning Repository (available directly through `sklearn.datasets.load_wine`). It has **178 samples** of wine, each described by **13 chemical features** like alcohol, malic acid, magnesium, flavanoids, color intensity, hue and proline.

The dataset also comes with a known label (which wine cultivar each sample belongs to), but I did **not** use this label while clustering — I only used it at the end to check how good my clustering actually was. This is important because clustering is supposed to be unsupervised, so using the label during training would defeat the purpose.

✅ There were 0 missing values in the dataset, so no cleaning was required before moving to preprocessing.

## 🛠️ Steps I Followed

1. **📥 Data Acquisition** – Loaded the Wine dataset using sklearn and converted it into a pandas DataFrame.
2. **🔍 Exploratory Data Analysis (EDA)** – Checked the shape, summary statistics, and plotted a correlation heatmap to see how features relate to each other.
3. **⚖️ Preprocessing** – Used `StandardScaler` to scale all features, since some features (like proline) had much bigger numbers than others (like hue), which would otherwise mess up distance-based clustering.
4. **📈 Finding the Right Number of Clusters (k)** – Used both the Elbow Method (WCSS) and Silhouette Score across k = 2 to 10, instead of relying on just one method, to pick the best k more confidently.
5. **🧩 K-Means Clustering** – Applied K-Means with the chosen k and calculated the silhouette score for the final result.
6. **🌳 Hierarchical Clustering** – Built a dendrogram using Ward linkage and also applied Agglomerative Clustering with the same k, mainly to cross-check the K-Means result with a second method.
7. **🗺️ PCA Visualization** – Since the dataset has 13 dimensions and can't be plotted directly, I used PCA to reduce it to 2D just to visualize how well-separated the clusters are.
8. **🧪 Cluster Profiling** – Grouped the data by cluster and took the average of each feature per cluster, to understand what makes each cluster chemically different.
9. **✅ Validation Against Ground Truth** – Compared my clusters with the actual wine labels (only after clustering was done) to check how accurate the unsupervised result turned out to be.

## 📊 Results

- 🔢 The optimal number of clusters came out to be **k = 3**, confirmed by both the silhouette score peak and the elbow curve bend.
- 🏆 K-Means achieved a silhouette score of **0.285**, and Hierarchical Clustering achieved **0.277** — both close to each other, showing the two methods largely agree.
- ✅ When compared against the actual wine cultivar labels, the clusters matched very closely, which shows the clustering found real, meaningful structure in the data and not something random.
- 🍇 Each cluster turned out to represent a distinct chemical profile — for example, one cluster had high proline and flavanoids (likely riper, more aged wines), while another had high color intensity but low phenolic content.

## 🧰 Tech Stack / Libraries Used

- 🐍 Python 3
- 🐼 pandas, numpy
- 📉 matplotlib, seaborn
- 🤖 scikit-learn (StandardScaler, PCA, KMeans, AgglomerativeClustering, silhouette_score)
- 🔬 scipy (for the dendrogram and linkage)

## 📁 Files in this Repository

| File | Description |
|---|---|
| 🐍 `clustering_analysis.py` | Full Python script with all steps from data loading to validation |
| 📄 `Week3_Clustering_Report.docx` | Final report with explanations, code snippets, screenshots and analysis |
| 🖼️ `plots/` | All generated visualizations (heatmap, elbow/silhouette graph, dendrogram, PCA cluster plots) |
| 📊 `cluster_profile.csv` | Average feature values per cluster |
| 📋 `crosstab_kmeans_vs_actual.csv` | Comparison between predicted clusters and actual wine labels |

## ⚠️ Limitations

- 📉 The silhouette score (~0.28) is decent but not extremely high, mainly because a few features in the dataset are correlated with each other, and a handful of samples sit chemically between two clusters.
- 🗺️ PCA visualization only captures around 55% of the total variance in 2D, so the plot is a simplified view and not the full picture of the original 13-dimensional data.
- ⭕ K-Means assumes roughly round/spherical clusters, which worked well for this dataset, but might not work as well on datasets with irregularly shaped groups.
- 🎯 This dataset happens to have ground truth labels available for validation, which is rare in real-world unsupervised problems, where such direct validation usually isn't possible.

## ▶️ How to Run

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
python clustering_analysis.py
```

All plots will be saved inside the `plots/` folder, and the cluster profile/validation tables will be saved as CSV files in the same directory.

## 🏁 Conclusion

This task helped me understand how unsupervised clustering actually works in practice — not just running an algorithm, but also figuring out the right number of clusters, cross-checking results with a second method, and interpreting what the clusters mean instead of just accepting the output blindly.
