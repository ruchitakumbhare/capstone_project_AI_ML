# Capstone_Project_AI_ML

Black‑Box Optimisation (BBO) Capstone Project
1. Project Overview
   
This repository documents my work on the Black‑Box Optimisation (BBO) Capstone Project, a multi‑week challenge focused on optimising eight unknown functions under strict query constraints. Each function represents a synthetic but realistic scenario—ranging from contamination detection to hyperparameter tuning—where the internal structure is hidden, evaluations are expensive and noisy, and only a limited number of queries are allowed.
The overall goal is to propose one new query point per function each week, using the growing dataset to refine modelling strategies and improve performance. This mirrors real‑world ML settings where engineers must optimise expensive processes (e.g., simulations, experiments, model training) without full visibility into the underlying system.
This project supports my career by strengthening skills that are essential in ML and applied data science:
- Working with incomplete information
- Building surrogate models
- Balancing exploration vs exploitation
- Designing interpretable, reproducible optimisation workflows
- Communicating technical reasoning clearly
These are the same skills used in hyperparameter tuning, A/B testing, scientific experimentation, and optimisation of financial or engineering systems.

2. Inputs and Outputs
   
Each week, I submit one query vector for each of the eight black‑box functions.
Input format
- A vector of dimension d, where d varies by function (2D, 3D, 4D, 5D, 6D, 8D).
- Each coordinate must:
- Begin with 0.
- Be in the range [0,1)
- Be specified to six decimal places
- Format:
x1-x2-x3-...-xd


- Example for a 2D function:
0.123456-0.654321
Output- A single numeric value returned by the black‑box function.
- All tasks are framed as maximisation problems.
- Outputs may be:
- Noisy
- Non‑linear
- Multi‑modal
- Transformed (e.g., negated side‑effects)
These outputs form the dataset used to update my models and guide future queries.

3. Challenge Objectives
  
   The objective is to maximise all eight unknown functions using as few evaluations as possible.
   Key constraints include:- Strict query budget: one query per function per week
- Delayed feedback: outputs arrive only after submission
- Unknown structure: no gradients, no closed‑form expression
- High dimensionality in some functions (up to 8D)
- Noisy evaluations, especially in functions with stochastic behaviour
Success depends on building models that can generalise from very limited data and making principled decisions about where to query next.

4. Technical Approach
  
   This section summarises my evolving strategy across the first three rounds. I treat it as a living record and will continue updating it as the project progresses.

   Week 1 – Baseline Exploration- With only the initial dataset available, I used a balanced exploration–exploitation approach.
    - I avoided committing too strongly to any region and selected points that were near promising areas but still expanded coverage.
    - The focus was on mapping the space rather than chasing early optima.
  Week 2 – Function‑Specific Strategy- After receiving the first set of outputs, I shifted to a more differentiated approach:
    - Exploitation for functions showing strong performance (5, 7, 8)
    - Exploration for functions with consistently poor values (1, 4, 6)
    - Mixed strategy for functions with moderate improvement (2, 3)
    - I used simple surrogate models (e.g., GP‑like reasoning, local trends) without heavy hyperparameter tuning.
    - I began analysing local linearity and feature influence to guide perturbations.
  Week 3 – Model‑Driven Refinement + SVM Thinking- With more data, I relied more on model predictions and local structure.
    - I introduced SVM‑based reasoning:
    - Using a soft‑margin SVM to classify “high vs low” performance regions
    - Considering kernel SVMs to capture non‑linear boundaries
    - Using the SVM margin to identify uncertain regions worth exploring
    - This classification perspective complements regression‑based surrogates by highlighting where the decision boundary between “good” and “bad” lies.
    - I also monitored model limitations:
    - Risk of overfitting in higher dimensions
    - Emerging irrelevant or low‑impact features
    - Increasing uncertainty in sparsely sampled regions
      
Exploration vs Exploitation Philosophy

  My approach balances three principles:- Exploit when the function shows stable, high‑performing regions
(e.g., Functions 5, 7, 8)
- Explore aggressively when the function remains flat or poor
(e.g., Functions 1, 4, 6)
- Use model‑guided refinement when the function shows partial structure
(e.g., Functions 2, 3)
This evolving strategy mirrors real‑world optimisation workflows where data is scarce, noise is present and decisions must be justified
