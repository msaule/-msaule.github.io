# Blockchain + Machine Learning Healthcare Fraud Ledger

Description: A project that combines everything I care about: healthcare, data, trust, transparency, and building systems that actually matter.
Skills Demonstrated: Blockchain, Data Science, Fraud Analytics, Machine Learning, Transparency
Project Status: Planning

## **💬 Why I Built This**

Healthcare has always been personal for me.

I grew up around systems that weren’t always transparent or reliable, and I lost my dad partly because of failures in that system. Years later, being treated at Mayo Clinic showed me the opposite, what excellent healthcare feels like when it works the way it should.

Those two experiences shaped how I think about healthcare,

**good systems save lives, and broken ones cost them.**

This project is my way of exploring that intersection using data, machine learning, and even blockchain (yes, actual blockchain, not crypto hype) to build a more transparent, trustworthy way to detect and audit fraudulent healthcare claims.

I wanted to create something that felt like a *real internal tool*, not a school assignment. Something with structure, risk scoring, integrity checks, and analytics that someone in healthcare operations could actually use.

# 🧠 **What This Project Actually Does**

This system takes real insurance claims data from Kaggle, predicts fraud using a trained XGBoost model, and stores each claim inside a custom blockchain ledger I built from scratch.

Every claim becomes a “block” that contains:

- key claim metadata
- financial information
- the ML model’s fraud probability
- timestamp
- SHA-256 hash of the block
- previous block’s hash

Together, they form a **tamper-evident audit ledger**.

If someone tries to modify a claim or alter a fraud score, the entire chain breaks.

That’s the entire point: **trust through structure**.

---

# ⚙️ **How the System Works (High-Level)**

### **1. ML Scoring Pipeline**

I trained an XGBoost model on structured claims data.

It processes fields like:

- incident type
- insured occupation
- claim amounts
- injury/property/vehicle damage
- incident severity
- and more

It outputs a fraud probability:

```python
proba = model.predict_proba(df)[:, 1]
df["fraud_prob"] = proba
```

The scored dataset becomes the input to the blockchain.

![image.png](Blockchain%20+%20Machine%20Learning%20Healthcare%20Fraud%20Led/image.png)

---

### **2. Custom Blockchain Implementation**

I implemented the blockchain manually using Python, no libraries, no shortcuts.

Each block is hashed:

```python
hashlib.sha256(block_string.encode()).hexdigest()
```

And each block links to the previous one:

```python
new_block.previous_hash = last_block.hash
```

If even one number changes, the entire chain becomes invalid.

This turned out to be my favorite part because it forced me to think like a systems engineer, not just a data scientist.

![image.png](Blockchain%20+%20Machine%20Learning%20Healthcare%20Fraud%20Led/image%201.png)

---

### **3. Fraud Ledger Export**

The ledger (1,001 blocks including genesis) is exported to a JSON file:

```
data/processed/chain_output.json
```

This is the “source of truth” for the whole system.

---

### **4. Interactive Dashboard**

Using Streamlit, I built a simple dashboard to visualize:

- total claims
- high-risk claims
- total exposure
- fraud probability distribution
- a high-risk claims table
- a block explorer (view a single block’s content)

It’s not over-engineered, it’s exactly what a fraud analyst would want to look at.

![image.png](Blockchain%20+%20Machine%20Learning%20Healthcare%20Fraud%20Led/image%202.png)

![image.png](Blockchain%20+%20Machine%20Learning%20Healthcare%20Fraud%20Led/image%203.png)

---

# 📊 **Some Real Insights From the Ledger**

Working with the full pipeline revealed patterns I never would’ve noticed by just looking at the CSV:

- **22.3% of claims were high-risk (>0.70)**
- **Total financial exposure was ~$52.7M**
- Multi-vehicle collisions and single-vehicle collisions were the most common incident types
- Fraud risk varies pretty widely across states
- The top 5 riskiest claims had fraud probabilities between **0.983–0.990**

These aren’t “perfect” findings, but they’re real, and they demonstrate how ML + structured auditing can complement each other.

![image.png](Blockchain%20+%20Machine%20Learning%20Healthcare%20Fraud%20Led/image%204.png)

---

# 🧱 **What I Learned**

This project reinforced a few big lessons for me:

### **1. ML is just one piece of a system.**

A model without structure or oversight is basically a guessing engine.

Putting it inside an auditable pipeline made it feel like it had purpose.

### **2. Transparency matters.**

Being able to prove that data hasn’t been changed, or detect when it has, matters in healthcare.

### **3. Good engineering feels like building trust.**

Hashing, linking, validating - these aren’t “just code.”

They’re mechanisms to enforce honesty.

### **4. My best work happens when it ties back to something personal.**

This project meant more because of why I built it.

---

# 🗂 **Project Structure (Clean & Modular)**

```
app/                    → pipeline scripts
blockchain/             → custom blockchain core
ml/                     → model loading + scoring
models/                 → trained XGBoost fraud model
data/raw                → original claims
data/processed          → scored claims + blockchain ledger
streamlit_app.py        → dashboard

```

---

# 🔭 **If I Extended This Project…**

I’d add:

- provider-level fraud analytics
- real anomaly detection (cluster-based)
- per-block SHAP explanations
- a real-time API
- a tamper-detection demo button in the dashboard

But honestly, for now, I’m happy with where this landed.

---

# 🔚 **Final Thoughts**

This project started as “what if I combined ML with a blockchain”

and ended as something that genuinely reflects what I care about:

- using data to improve healthcare
- building systems that enforce trust
- designing tools that could help real analysts
- and pushing myself beyond just training models

And I’m proud of it.

If you want to talk to me about this project or anything related to healthcare, ML, or fraud detection, I’m always open to conversations.

**Markuss Saule**