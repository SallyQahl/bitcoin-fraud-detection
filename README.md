graph enhanced machine learning# Bitcoin Fraud Detection — Blockchain Analytics

Detecting illicit transactions in the Bitcoin network using graph-enhanced machine learning on the Elliptic dataset.

## Results

| Metric | Score |
|--------|-------|
| Accuracy | 99% |
| Precision (illicit) | 100% |
| Recall (illicit) | 88% |
| AUC-ROC | 0.997 |

## Dataset

The [Elliptic Data Set](https://www.kaggle.com/datasets/ellipticco/elliptic-data-set) maps 203,769 Bitcoin transactions to real entities — exchanges, wallets, darknet markets, scams, ransomware, and Ponzi schemes. Download from Kaggle and place in `elliptic_bitcoin_dataset/`.

## Methodology

Started with unsupervised anomaly detection using Isolation Forest on raw transaction features. 
The model failed to detect illicit transactions, which pointed to a structural problem: the 167 features are anonymized, 
and without network context, 
no statistical signal separates fraud from legitimate activity.

Rebuilt the pipeline using the transaction graph. Constructed the full Bitcoin network from 234,355 edges, computed degree centrality for each transaction node, and fed that into a class balanced Random Forest. 
The class weighting corrects for the 9:1 licit/illicit imbalance without discarding data.

## Key Finding

Graph structure matters. Isolation Forest on raw features: 0% recall. Graph-enhanced Random Forest: 
88% recall, 100% precision, AUC 0.997. The failure of the first model is itself the finding 
it explains why blockchain fraud detection requires network-aware methods.

## Visualizations

![Confusion Matrix](confusion_matrix.png)
![ROC Curve](roc_curve.png)
![Feature Importance](feature_importance.png)

## Phase 2

Graph Neural Network implementation on the same dataset, following the Elliptic/MIT paper methodology.

## Author

Salha Qahl
