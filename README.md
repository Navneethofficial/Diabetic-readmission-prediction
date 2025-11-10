# Diabetic Patient Readmission Segmentation

This project applies **unsupervised learning** (clustering) to segment diabetic patients based on their hospital admission patterns and medical features.  
The goal is to **identify distinct patient groups** that may have different risks of readmission, enabling healthcare providers to design **personalized interventions** and reduce hospital costs.  

---

## Project Overview
- **Objective**: Cluster diabetic patients into distinct groups to better understand readmission patterns.  
- **Dataset**: UCI Diabetic Data Set (130 US hospitals, 10 years of data).  
- **Techniques**:  
  - Data preprocessing (handling missing values, categorical encoding, scaling).  
  - Dimensionality reduction with PCA.  
  - Clustering with **KMeans** and **DBSCAN**.  
  - Visualization of patient clusters.  

---

## Dataset Summary
- **Observations**: ~100,000 hospital admission records.  
- **Target column**: Not supervised (unsupervised learning task).  
- **Key Features**:  
  - Demographics (age, gender, race).  
  - Hospitalization details (time in hospital, number of visits).  
  - Diagnoses (ICD-9 codes).  
  - Medications and changes.  
  - Lab results and procedures.  

---

## Models & Methods
- **KMeans Clustering**  
  - Elbow method & Silhouette Score used for optimal cluster selection.  
- **DBSCAN**  
  - Density-based clustering to detect outlier patients.  
- **PCA (2D/3D)** for visualization of patient clusters.  

---

## Results
- KMeans identified **distinct patient segments** based on hospitalization history and treatment details.  
- DBSCAN highlighted **outlier patients** with unusually high hospital visits.  
- Clusters showed separation based on:  
  - **Number of prior inpatient visits**  
  - **Time in hospital**  
  - **Medication changes**  
  - **Diabetes-related diagnoses**  

---

## Business Insights
- Different clusters represent **low-risk, medium-risk, and high-risk** patient groups.  
- Patients with frequent prior visits & longer hospital stays are **high readmission risk**.  
- **Outliers** (e.g., frequent ER users) need special management programs.  
- Hospitals can design **personalized discharge plans** and allocate resources more efficiently.  

---

## Files in the Repo
- `diabetic-readmission-segmentation.ipynb` – Source Jupyter Notebook  
- `diabetic_data.csv` – Dataset used in the project  
- `requirements.txt` – Required Python libraries  
- `README.md` – Project overview (this file)  

---

## Future Work
- Try **Hierarchical Clustering** for more granular segmentation.  
- Apply **autoencoders** for advanced dimensionality reduction.  
- Deploy with **Streamlit/Dash** for interactive hospital dashboards.  
- Integrate with hospital EHR systems for **real-time patient segmentation**.

## ✍️ Authorship
- **Author**: Azib Malick  
- **Role**: Data Science & Machine Learning Enthusiast  
- **Contact**: [LinkedIn](https://www.linkedin.com/in/azibmalick) | [GitHub](https://github.com/azibmalick)  
