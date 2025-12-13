---
title: "My Work In Progress Post"
date: 2025-12-15 10:00:00 -0500 
draft: true 
published: false 
---
# This is the Content Section (Starts right after the closing '---')

---
# 1. POST METADATA (FRONT MATTER)
# -------------------------------------------------------------
title: "Project Milestone: Setting up a Data Cleaning Pipeline"
date: 2025-12-12 20:01:09 -0500 # Use the current date and time (or intended publish date).
draft: true
published: false
last_modified_at: 2025-12-12T20:01:09-05:00 # Automatically updated if you use an editor like VS Code
categories: # Choose 1-3 high-level categories
  - Python
  - Data Science
tags: # Use 3-5 specific keywords for search
  - pandas
  - data-wrangling
  - jupyter
  - setup
header:
  # Optional: Adds an image at the top of the post (requires path relative to site root)
  # image: /assets/images/header-image.jpg 
  # optional: You can specify a permalink to make the URL clean
  # permalink: /posts/data-cleaning-pipeline-setup
toc: true # Set to true to automatically generate a table of contents from your headings
toc_label: "Table of Contents"

# Optional: If you want to draft it locally before publishing
# published: false 
---

## 🌟 Overview & Goals Achieved

*(Start with a brief, 1-2 paragraph summary of the work covered in this post.)*

This week, I focused on Phase 1 of the Titanic Survival Prediction project: data acquisition and initial cleaning. The main goal was to establish a repeatable pipeline to handle missing values and standardize column formats, which will feed directly into the feature engineering phase next week.

## 🛠 Tools and Environment

*(List the specific libraries, versions, or environments used for this milestone.)*

* **Language:** Python 3.11
* **Primary Libraries:** `pandas`, `numpy`
* **Environment:** Jupyter Notebooks (VS Code Integrated)

---

## 🔬 Technical Deep Dive

*(Use this section to discuss the **problems** you faced and the **techniques** you used to solve them. Use level 3 headings (`###`) for specific topics.)*

### Data Acquisition and Loading

The raw dataset required simple loading. A quick note on best practice: always use `pd.read_csv()` with an explicit `encoding='utf-8'` to prevent unexpected errors later.

### Handling Missing Values (NaNs)

The `Age` and `Cabin` columns presented the biggest challenge.

For the `Age` column, I initially considered mean imputation but opted for median imputation based on the passenger class to preserve the data distribution better, as age is skewed.

```python
# Impute Age based on the median age for each class
df['Age'] = df.groupby('Pclass')['Age'].transform(lambda x: x.fillna(x.median()))