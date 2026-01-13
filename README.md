# 📌 DBSCAN & Hierarchical Clustering – Practical Analysis

এই repository তে আমি **DBSCAN (Density-Based Spatial Clustering of Applications with Noise)** এবং **Hierarchical Clustering** ব্যবহার করে বিভিন্ন dataset (blob, circles, moons) এর উপর experiment করেছি। নিচে step-by-step explanation দেওয়া হলো, যেন যে কেউ output দেখেই core concept বুঝতে পারে।

---

## 🔹 Datasets Used

### 1️⃣ Blob Dataset (Varying Density)

* Cluster গুলো প্রায় spherical / blob-shaped
* Density একরকম না (কিছু dense, কিছু sparse)

### 2️⃣ Circular / Non-linear Dataset

* Inner–outer circles
* Non-spherical structure

---

## 🔹 DBSCAN Overview

**DBSCAN** হলো একটি **density-based clustering algorithm**।

### Key Parameters:

* **eps (ε)** → Neighborhood radius
* **min_samples** → Minimum points to form a dense region

### Labels Meaning:

* `0,1,2,...` → Valid clusters
* `-1` → Noise / Outlier points

---

## 🔹 DBSCAN Results Analysis

### ✅ Blob Dataset Output

```
Unique cluster labels: [-1, 0, 1, 2]
Total points: 400
Noise: 7 points
Cluster 0: 200 points
Cluster 1: 43 points
```

🔍 **Observation:**

* DBSCAN blobs detect করেছে, কিন্তু density variation থাকার কারণে

  * কিছু point `-1` (noise) হয়েছে
  * Cluster size uneven

📌 **Insight:**

> DBSCAN blob dataset এ কাজ করে, কিন্তু **K-Means বা Ward linkage** এখানে বেশি stable result দেয়।

---

### ✅ Effect of eps

| eps value       | Result                 |
| --------------- | ---------------------- |
| Small eps (0.2) | Many noise points (-1) |
| Medium eps      | Balanced clusters      |
| Large eps (0.5) | Clusters merge হয়ে যায় |

📌 **Rule of Thumb:**

> Optimal eps এ সাধারণত **5–10% noise** accept করা যায়

---

### 📈 k-distance Graph (k = 5)

* Sharp bend / elbow point ≈ best eps
* Graph এর steep rise শুরু হওয়ার আগের distance ideal eps

📌 **Why important?**

> eps guess না করে data-driven way তে choose করা যায়

---

### ✅ Circular Dataset with DBSCAN

```
Clusters found: 10
Labels: [-1 0 1 2 3 4 5 6 7 8 9]
```

🔍 **Observation:**

* eps ছোট হলে DBSCAN circle dataset কে multiple small clusters এ ভাগ করে ফেলে

📌 **Lesson:**

> Non-linear data তে eps tuning খুব critical

---

## 🔹 Hierarchical Clustering Overview

Hierarchical clustering builds a **tree-like structure (dendrogram)**.

### Linkage Methods Used:

* **Single** linkage
* **Complete** linkage
* **Average** linkage
* **Ward** linkage

---

## 🔹 Hierarchical Results

```
Single:   [0 1]
Complete:[0 1]
Average: [0 1]
Ward:    [0 1]
```

🔍 **Observation:**

* সব linkage method blob dataset এ **2 clear clusters** detect করেছে

---

## 🔹 Linkage Comparison

### 🟢 Ward Linkage (Most Intuitive)

* Minimizes intra-cluster variance
* Compact & balanced clusters
* Best for blob / spherical data

### 🟡 Single Linkage

* Chaining effect
* Best for non-spherical shapes (circles, moons)

### 🔵 Complete & Average

* Middle-ground behavior
* Less chaining than single

📌 **Conclusion:**

> General purpose use এর জন্য **Ward linkage** সবচেয়ে intuitive

---

## 🔹 When to Use Which Algorithm?

### ✅ Prefer DBSCAN when:

* Arbitrary shape clusters (circle, moon)
* Noise / outlier detection important
* Cluster number unknown

### ❌ Avoid DBSCAN when:

* Density varies a lot
* Very high-dimensional data

---

### ✅ Prefer Hierarchical Clustering when:

* Dataset small (< 10k points)
* Cluster number unknown
* Relationship visualization (dendrogram) দরকার
* Reproducible result চাই

### ❌ Avoid Hierarchical when:

* Dataset very large
* Performance critical

---

## 🔹 Final Takeaways

* **DBSCAN** → Shape-based + noise-aware clustering
* **Hierarchical (Ward)** → Clean & interpretable blob clustering
* **eps tuning** → DBSCAN এর সবচেয়ে critical part
* **k-distance graph** → eps selection এর best tool

---

