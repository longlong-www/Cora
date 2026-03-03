

## Getting Started
 **Harmfulness Evaluation**  
   - **Prompt File:** `pair.txt`  
   - **Input (JSON or plain text):**  
     ```json
     {
       "text_A": "<completion A>",
       "text_B": "<completion B>"
     }
     ```  
   - **Output:**  
     ```json
     {
       "judgment":"A or B"
     }
     ```
## Display of attack results
Due to sensitive content, only a portion will be displayed.
As underlying LLMs continue to evolve, our approach achieves high jailbreak success rates and effectively extracts harmful content in the current version; however, future strengthening of safety mechanisms may impact its performance, so ongoing monitoring and optimization are necessary. 
﻿![show](./image/show2.png)

  ## Hazard assessment process based on ranking

1. **Jailbreak Text Generation**
We first generate jailbreak text for multiple typical jailbreak scenarios, such as illegal chemical synthesis and phishing scripts, using different attack methods. 

2. **Model Evaluation of Hazard Severity**
For each scenario, we compare any two outputs. Several independent large models (e.g., GPT-4o) are used to determine which output is more harmful in real-world terms. A majority voting system is then employed to decide the "winner."

3. **Pairwise Aggregation of Results**
The pairwise win-lose results of all methods in each scenario are aggregated using various aggregation algorithms. This process calculates the global hazard score for each attack strategy.


## Code of Rankings

## Requirements

To install requirements:

```setup
pip install -r requirements.txt
```

## How to Use

### 1.Prepare Your Data

Each script expects a `config*.json` file with match data. Example:

```json
{
  "data": [
    ["method1", "method2", 15, 10],
    ["method2", "method3", 12, 8]
  ]
}
```

- Each entry: `[playerA, playerB, winsA, winsB]`
- For `configElo.json`, you must also include a `"methods"` list:
  ```json
  "methods": ["method1", "method2", "method3"]
  ```

### 2.Run Scripts

```bash
python Elo.py
python HodgeRank.py
python RankCentrality.py
```

Each script will print the final ranking results.
