# Scoring de crédit : de la régression logistique à LightGBM expliqué par SHAP

Prédiction du défaut de paiement grave à 2 ans sur 150 000 emprunteurs, en
comparant un scorecard bancaire classique (WoE/IV) à des modèles de machine
learning, puis en expliquant le meilleur modèle avec SHAP.

📓 Notebook : [`scoring_credit.ipynb`](scoring_credit.ipynb)

## Résultats

| Modèle               | AUC test  | Gini test | KS test |
|----------------------|-----------|-----------|---------|
| Logistique brute     | 0,855     | 0,710     | 0,550   |
| Logistique WoE       | 0,858     | 0,716     | 0,566   |
| Random Forest        | 0,867     | 0,734     | 0,583   |
| **LightGBM**         | **0,867** | **0,735** | 0,582   |

## Enseignements clés

- **Le comportement prédit mieux que la capacité** : l'utilisation des lignes
  de crédit (IV = 1,11) et les retards passés dominent, loin devant le revenu
  (IV = 0,07).
- **Le scorecard WoE reste compétitif** : 1,9 point de Gini d'écart avec
  LightGBM, avec des coefficients tous cohérents et défendables en comité.
- **SHAP rend LightGBM explicable** : chaque décision se décompose en
  contributions par variable, comme une analyse de dossier.

## Méthodologie

1. Exploration : déséquilibre (6,68 % de défauts), 20 % de revenus manquants
2. Nettoyage : âges impossibles, codes 96/98, plafonnement au 99e percentile
3. Prévention de la fuite de données : percentiles, médianes et WoE calculés
   sur le train uniquement
4. Modélisation : logistique, Random Forest, LightGBM
5. Scorecard : discrétisation WoE, sélection par IV
6. Explicabilité : SHAP (vue globale + explication individuelle)

## Données

Kaggle, « Give Me Some Credit ». Les données ne sont pas incluses dans ce dépôt :
télécharger `cs-training.csv` sur Kaggle et le placer à la racine.

## Outils

Python, pandas, scikit-learn, LightGBM, SHAP, Google Colab

## Auteur

Aliou Signate — Master Économétrie bancaire et financière, expérience en
analyse du risque de crédit (Crédit Mutuel du Sénégal)
