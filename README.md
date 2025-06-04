# Product Circularity & Automation in the Refurbishment Sector  
**By UKANDU Chidinma – Python Analysis Project**

---

## Project Overview

This project explores how refurbished devices are evaluated, categorized, and ultimately processed for resale or disposal. It focuses on:

- Understanding the distribution of device condition scores
- Examining manufacturer trends and component specs (RAM, HDD) 
- Assessing how different condition categories relate to automation and reuse
- Investigating performance drivers like device type, condition, and internal specs

---

## Tools Used

- **Python (pandas, seaborn, matplotlib)** – Data analysis and visualization
- **Jupyter Notebook** – Interactive exploration
- **Power BI (optional companion)** – For possible reporting enhancements

---

## Key Insights & Visual Interpretations

---

### 🔍 1. Distribution of Condition Scores

```python
sns.histplot(Rebu_drop['Condition.Score'], kde=True, bins=10)
```

![image](https://github.com/user-attachments/assets/2258a06c-44d2-4300-8c81-0eb2c7436eae)


**Interpretation:**
> The condition scores are **right-skewed**, with the majority of devices scoring **between 3.5 and 4.5**. This implies that most devices received are in relatively good shape, with fewer devices in poor condition (scores < 2). The KDE curve also shows strong clustering near 4, indicating refurbishment potential.

---

### 2. Condition Category Breakdown

```python
sns.countplot(x='Condition.Category', data=Rebu_drop, order=['High', 'Medium', 'Low', 'Discard'])
```

![image](https://github.com/user-attachments/assets/15a830ad-b62e-4011-a610-4ff3f30297a7)


**Interpretation:**
> About **44% of the devices** fall into the **High** category, followed by **40% Medium**, and **15% Low**. Only **0.6% are discarded**, which is an encouraging circularity indicator. It shows most devices can be repurposed.

---

### 3. Correlation Between Specs & Condition

```python
sns.heatmap(Rebu_drop[['Condition.Score', 'RAM.GB', 'HDD.MB']].corr(), annot=True)
```

![image](https://github.com/user-attachments/assets/f76ecc84-bed2-4c36-a679-551fc8e0045e)


**Interpretation:**
> There is a **moderate to strong positive correlation** between `Condition.Score` and:
- `RAM.GB` (**0.7**)
- `HDD.MB` (**0.56**)

This suggests that **better hardware configurations often correlate with higher condition scores**, possibly due to less wear and newer models.

---

### 🏢 4. Manufacturer Condition Trends

```python
avg_condition = Rebu_drop.groupby('Manufacturer')['Condition.Score'].mean().sort_values()
```

![image](https://github.com/user-attachments/assets/bdc16474-b5b9-42e0-9c6e-27ba71e88638)


**Interpretation:**
> This graph ranks manufacturers by **average device condition**. Brands like **ASUS, Gateway, and HP-Pavilion** scored high, whereas others (e.g., **Sony, Toshiba, Lenovo**) had more devices in poorer shape. These patterns could guide sourcing or supplier partnerships.

---

### 💻 5. Device Type vs Condition Categories

```python
Rebu_drop.groupby(['Type', 'Condition.Category']).size().unstack().plot(kind='bar', stacked=True)
```

📷 ![image](https://github.com/user-attachments/assets/b976a330-110d-4196-9f3c-397504bbfd95)


**Interpretation:**
> All observed devices are categorized as **computers**, with the majority falling under **Medium** and **High** conditions. There’s very minimal discard, again reinforcing that refurbishment is viable for most devices.

---

### 6. Proportion of Condition Categories (Pie View)

```python
Rebu_drop['Condition.Category'].value_counts().plot(kind='pie', autopct='%1.1f%%')
```

![image](https://github.com/user-attachments/assets/bd253852-c850-484a-b48f-4558f5ccd1c2)


**Interpretation:**
> The pie chart mirrors earlier findings: **High (44%)** and **Medium (40%)** dominate. This format clearly communicates to stakeholders how few products are lost to discard — a strong case for sustainability and reuse.

---

### 7. Manufacturers of Discarded Devices

```python
Rebu_drop[Rebu_drop['Condition.Category'] == 'Discard']['Manufacturer'].value_counts().plot(kind='barh')
```

![image](https://github.com/user-attachments/assets/090e7db3-8ca5-4048-94fa-bd69fafda6f1)


**Interpretation:**
> Among discarded devices, **Lenovo and HP Inc.** appear most often. This doesn’t necessarily imply poor quality but could suggest a higher volume of low-end models being processed. It could guide procurement filters or QC thresholds.

---

### 8. Component Impact on Condition

```python
sns.scatterplot(x='RAM.GB', y='Condition.Score', hue='Condition.Category')
sns.scatterplot(x='HDD.MB', y='Condition.Score', hue='Condition.Category')
```

![image](https://github.com/user-attachments/assets/a5b525d5-77d0-47cd-b83a-9b10f046fa24)

![image](https://github.com/user-attachments/assets/da3f7248-5c96-49bd-87dc-ee84cb12f106)


**Interpretation:**
> Higher RAM and HDD capacities generally lead to **better condition scores** and are associated with **High/Medium condition categories**. Devices with lower component specs cluster around lower condition scores — crucial for refurbishment triage decisions.

---

### 9. Device Registration Trends Over Time

```python
df.groupby('Month')['Device_ID'].count().plot(marker='o')
```

📷 ![image](https://github.com/user-attachments/assets/b8799b98-24ff-4699-8c26-6408087ea13a)


**Interpretation:**
> Registrations spiked notably in **late 2017 and early 2019**, possibly due to bulk inventory returns or seasonal collection drives. Understanding such trends aids **forecasting, staffing, and resource allocation** during peak return periods.

---

## Final Conclusions

- **Most devices (84%) are reusable**, which strongly supports circularity goals.
- **Hardware specs (RAM/HDD)** play a major role in **condition ratings**.
- **Lenovo, HP, and Toshiba** dominate discarded counts, but also high-volume refurbishables.
- Strategic **supplier selection and intake filtering** can reduce discard rates.
- Visual analytics helped uncover **hidden relationships** in component and condition patterns.

---

## Author & Contact

** Author:** UKANDU Chidinma  
Master's Student in Business Intelligence  
Besançon, France  
Email: chidinmaukandu8@gmail.com
LinkedIn: ([https://www.linkedin.com/in/chidinma-ukandu](https://www.linkedin.com/in/chidinma-ukandu-nwafor-01357b156/))

---

## 📄 License

Licensed under the [MIT License](LICENSE)

---

