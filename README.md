# AI ADMET Profiler for Indian Herbal Compounds
### Which Ayurvedic and kitchen-herb molecules are the best starting points for drug discovery?

An end-to-end mini project that profiles **39 compounds from Indian herbs and spices** using **three machine-learning models and RDKit**, then ranks them with one transparent score.

**Skills used:** Python, RDKit (cheminformatics), machine learning (scikit-learn), ADMET prediction, drug discovery.

## What it does
1. Takes 39 herbal molecules (curcumin, piperine, gingerol, thymol, berberine, quercetin and more). Each structure is checked against its published chemical formula.
2. Uses **RDKit** to calculate about 200 molecular descriptors, plus QED drug-likeness and Lipinski's Rule of Five.
3. Trains three **Random Forest** models on public data:
   - **Solubility** (Delaney/ESOL, about 1,100 molecules)
   - **Blood-brain barrier penetration** (BBBP, about 2,000 molecules)
   - **Toxicity assays** (Tox21: AhR, ARE, MMP, p53; about 8,000 molecules)
4. Predicts the ADMET profile of every herbal compound and combines it into a **Lead-likeness score (0 to 100)**: 30% QED + 25% solubility + 30% low toxicity risk + 15% Lipinski rules. Brain access is shown separately because whether it is desirable depends on the drug target.

## Results
| Model | Test performance (unseen molecules) |
|---|---|
| Solubility | R2 = 0.90, RMSE = 0.64 log units |
| Brain barrier | ROC-AUC = 0.96 |
| Toxicity (4 assays) | ROC-AUC = 0.84 to 0.94 |

**No data leakage:** every herbal compound was removed from the training data of every model.

**External check on real herbal compounds the models never saw:**
- Solubility: 13 herbs with lab-measured values, mean absolute error = **0.56 log units**.
- Toxicity assays: 144 labelled lab results (31 positive), pooled ROC-AUC = **0.92**.

Top starting points by score: zingerone, vanillin, menthol, linalool, ferulic acid.
Most flagged in toxicity assays: apigenin, emodin, luteolin.

## Limits (please read)
- Predictions are **computational, not proof**. Lab and clinical studies decide.
- Toxicity comes from **in-vitro (test-tube) assays**, not human safety data.
- The Lead score is a simple heuristic. It favours small, simple molecules, so a high score does not mean a good medicine.
- Public datasets are small and old, and herbal compounds are not well covered.
- Not modelled yet: hERG, CYP enzymes, metabolism, permeability, dose.

## Next steps
Add more ADMET endpoints (hERG, CYP), try gradient boosting and graph neural networks, use bigger datasets, and dock the top compounds against a target protein.

## How to run
Open the notebook in Google Colab (colab.research.google.com, File, Upload notebook), then **Runtime, Run all**. It downloads the data automatically and takes about 5 to 8 minutes.

## Data sources
Delaney (ESOL) solubility; BBBP (Martins et al., 2012); Tox21 (public toxicology challenge). All via public GitHub mirrors.

## Credits
Built with AI assistance as a learning project. The author ran and reviewed every step.
