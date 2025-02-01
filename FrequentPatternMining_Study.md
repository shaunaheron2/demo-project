# **Study Notes: Data Mining - Chapter 6**
## **Frequent Pattern Mining, Association Rules, and Correlation Analysis**

### **1. What is Frequent Pattern Mining?**
- **Definition:** A frequent pattern is a set of items, sequences, or structures that **appear frequently** in a dataset.
- **First introduced** by Agrawal, Imielinski, and Swami (1993) in the context of **association rule mining**.
- **Applications:**
  - Market Basket Analysis
  - Web Log Analysis
  - DNA Sequence Analysis
  - Social Network Mining

### **2. Market Basket Analysis**
- **Goal:** Identify **associations** between items frequently bought together.
- **Example:** 
  - **Association Rule:** `{Laptop} → {Mouse}` (If a laptop is bought, a mouse is also likely bought)
  - **Support:** Probability that both items appear together in transactions.
  - **Confidence:** Probability that a transaction containing `{Laptop}` also contains `{Mouse}`.

### **3. Key Measures for Association Rules**
1. **Support:**  
   Measures how frequently an itemset appears in the dataset.  
   $$
   Support(A \Rightarrow B) = P(A \cup B)
   $$
2. **Confidence:**  
   Measures how often **B** appears in transactions containing **A**.  
   $$
   Confidence(A \Rightarrow B) = P(B | A) = \frac{Support(A \cup B)}{Support(A)}
   $$
3. **Lift:**  
   Measures how much more likely **A and B** occur together compared to **independent** occurrences.  
   $$
   Lift(A \Rightarrow B) = \frac{P(A \cup B)}{P(A) P(B)}
   $$
   - **Lift > 1:** A and B are positively correlated.
   - **Lift < 1:** A and B are negatively correlated.

### **4. Frequent Itemsets and Rule Generation**
- **Frequent Itemset:** A set of items appearing together in at least **min_support** transactions.
- **Strong Rules:** Rules that meet **min_support** and **min_confidence**.
- **Example:**
  - **Transactions:**
    ```
    {Milk, Bread, Diaper}
    {Milk, Bread}
    {Milk, Diaper}
    {Bread, Diaper}
    ```
  - **Frequent Itemsets (min_support = 50%):**
    ```
    {Milk, Bread} → 50%
    {Milk, Diaper} → 50%
    ```

### **5. Apriori Algorithm (Breadth-First Search)**
- **Key Idea:** Uses the **downward closure property** – if an itemset is **frequent**, then all its subsets must also be frequent.
- **Steps:**
  1. Find frequent **1-itemsets**.
  2. Generate candidate **2-itemsets** from 1-itemsets.
  3. Keep itemsets with **min_support**.
  4. Repeat for **k-itemsets** until no more frequent itemsets exist.
- **Limitations:**
  - Multiple database scans.
  - High computational cost for large datasets.

### **6. FP-Growth Algorithm (Depth-First Search)**
- **Key Idea:** Uses **tree structures (FP-Tree)** to avoid candidate generation.
- **Steps:**
  1. Construct an **FP-Tree** (compressed representation of transactions).
  2. Use **recursive pattern growth** to mine frequent itemsets.
  - **Advantages over Apriori:**
    - Faster (avoids candidate generation).
    - Uses less memory.

### **7. Correlation Analysis & Alternative Interestingness Measures**
- **Limitations of Confidence:** Can be misleading when items are **independent**.
- **Alternative Measures:**
  - **Kulczynski Measure:**
    $$
    Kulc(A, B) = \frac{1}{2} (P(A | B) + P(B | A))
    $$
  - **Cosine Similarity:**
    $$
    Cosine(A, B) = \frac{P(A \cup B)}{\sqrt{P(A) P(B)}}
    $$
  - **Chi-Square Test:**
    $$
    \chi^2 = \sum \frac{(O_{ij} - E_{ij})^2}{E_{ij}}
    $$
  - **Interest Factor:**
    $$
    Interest(A, B) = \frac{P(A \cup B)}{P(A) P(B)}
    $$

### **8. Null Transactions and Null-Invariance**
- **Null Transactions:** Transactions that do not contain **A** or **B**.
- **Issue:** Some measures (like Lift) are **not null-invariant**, meaning they are affected by the number of null transactions.
- **Null-Invariant Measures:** Kulczynski, Cosine, Jaccard.

---

## **Summary**
- **Frequent pattern mining** identifies relationships between items in transactions.
- **Support, confidence, and lift** are key metrics for association rules.
- **Apriori algorithm** uses **candidate generation**, while **FP-Growth** eliminates it with **tree-based mining**.
- **Correlation measures** like **Kulczynski, Chi-Square, and Interest Factor** provide alternative interestingness criteria.

---

Let me know if you need modifications! 🚀
