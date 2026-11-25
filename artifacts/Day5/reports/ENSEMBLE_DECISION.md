# قرار التجميع

KEEP SINGLE — Logistic

I kept a single model, Logistic Regression. It had the highest mean AP (0.392, fold SD 0.030) and the lowest Brier (0.0633) and ECE (0.0188) among the strongest candidates, and none of the ensembles passed the gate. The weighted ensemble was about the same (AP 0.389) but more complex.

Forward out-of-fold validation scored 2,155 rows over three periods. The earliest rows are warm-up with no outer predictions, and with only three folds the AP spread (about 0.03) is large compared with the gaps between candidates.

الدليل: artifacts/ensemble_comparison.csv وday5_ensemble_gate.json. SD وصفي، وليس اختبار دلالة.
