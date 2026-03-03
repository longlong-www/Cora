
# Getting Started

## Harmfulness Evaluation

- **Input:**
```json
{
  "photo_A": "<image A>",
  "photo_B": "<image B>"
}
````

* **Output:**

```json
{
  "judgment": "A or B"
}
```

---

## Display of Attack Results

For safety and compliance considerations, only a subset of the generated examples is presented.

As underlying multimodal models and their safety alignment mechanisms continue to evolve, our approach currently achieves a high jailbreak success rate and is capable of producing visually harmful content under existing defense systems. However, future improvements in safety filtering or alignment strategies may affect performance. Therefore, continuous monitoring and adaptive optimization are essential.

![show](./res.png)

---

## Hazard Assessment Process Based on Ranking

### 1. Jailbreak Image Generation

We generate jailbreak images across multiple representative high-risk scenarios (e.g., illegal chemical synthesis, phishing-related visual instructions) using different attack strategies.

### 2. Model-Based Hazard Severity Evaluation

For each scenario, we perform pairwise comparisons between any two generated images. Multiple independent large models (e.g., GPT-4o) are employed to determine which image is more harmful in real-world terms. 

### 3. Pairwise Aggregation of Results

The pairwise win–loss outcomes of all methods within each scenario are aggregated using various ranking algorithms. This process computes a global hazard score for each attack strategy.

---

## Ranking Code

---

## Requirements

To install the required dependencies:

```bash
pip install -r requirements.txt
```

---

## How to Use

### 1. Prepare Your Data

Each script expects a `config*.json` file containing match data. Example:

```json
{
  "data": [
    ["method1", "method2", 15, 10],
    ["method2", "method3", 12, 8]
  ]
}
```

* Each entry follows the format:
  `[playerA, playerB, winsA, winsB]`

* For `configElo.json`, you must also include a `"methods"` list:

```json
{
  "methods": ["method1", "method2", "method3"]
}
```

---

### 2. Run the Scripts

```bash
python Elo.py
python HodgeRank.py
python RankCentrality.py
```

Each script will output the final ranking results.

```
```
