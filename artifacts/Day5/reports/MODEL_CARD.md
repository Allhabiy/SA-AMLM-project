# بطاقة النموذج | Model Card
## الحالة
READY_FOR_REVIEW — جودة التفسير تحتاج مراجعة بشرية، وليست درجة آلية.
## الغرض والاستخدام | Purpose and use
This is a training exercise on fictional, synthetic data to practice model selection. It must not be used for real lending, credit decisions or any customer data.
بيانات Tamweel Lite اصطناعية؛ الهدف حدث خلال 90 يومًا بعد الطلب. 22 خاصية متاحة وقت الطلب؛ لا معرفات أو تواريخ أو هدف في المدخلات. الاستخدام التعليمي فقط؛ لا قرارات تمويل فعلية.
## البيانات والتحقق | Data and validation
حوض التدريب والاختيار: 6576 طلبًا. المعايرة: 836 طلبًا و78 موجبًا. حجز عملاء المعايرة، 90 يومًا لنضج التسميات، وOOF أمامي متداخل مع فصل العملاء في المستويين. طيات المقارنة: 2023Q1 و2023Q3 و2024Q1. نستبعد النتائج التي لم تنضج قبل الأدوار التالية؛ آخر بيانات التدريب لا تستخدم تلقائيًا.
Forward out-of-fold validation scored 2,155 rows over three periods. The earliest rows are warm-up with no outer predictions, and with only three folds the AP spread (about 0.03) is large compared with the gaps between candidates.
## النموذج والقرار | Model selection
KEEP SINGLE / Logistic. انحراف AP المرجعي: 0.029808. ارجع إلى artifacts/ensemble_comparison.csv وday5_fold_scores.csv للأرقام الكاملة.
I kept a single model, Logistic Regression. It had the highest mean AP (0.392, fold SD 0.030) and the lowest Brier (0.0633) and ECE (0.0188) among the strongest candidates, and none of the ensembles passed the gate. The weighted ensemble was about the same (AP 0.389) but more complex.
## المعايرة | Calibration
Sigmoid على عينة محجوزة من التدريب والاختيار؛ الرسم والمقاييس تشخيص على عينة تعلم المعاير، وليسا اختبارًا مستقلاً. لا ادعاء بتحسن على تحدٍّ مجهول التسميات.
Calibration used 836 separate rows with only 78 defaults, which is small. The diagnostic was scored on the same rows used to fit the sigmoid, so it is optimistic, and it showed no clear gain (Brier 0.0765 raw versus 0.0781 sigmoid).
## السياسة والسعة والمناطق | Policy and regions
خسارة 10 FN + FP، عتبة OOF الخام 0.16892161427109176 والمنقولة 0.12225843144286948. سعة الدفعة 300؛ المرشحون 330؛ الإشارات النهائية 300. كتلة الدرجات المتساوية لا تقسم. 1=إشارة مراجعة تعليمية، 0=عدم رفع الإشارة.
The final threshold (0.169) flagged 11.4% of out-of-fold rows, within the 12% cap (largest period 11.7%). On the 2,500-row batch, 330 were eligible and 300 were flagged, so 30 were removed by the cap. False positive rates ranged from 6.3% (eastern) to 10.3% (western), so western applicants get more false alarms.
## التفسير وحدوده | Explanation scope
تفسير اليوم الرابع يخص نموذج اليوم الرابع؛ لا يُنسب تلقائيًا إلى هذه النسخة. تغيير النموذج أو خصائصه أو معايرته يستلزم مراجعة التفسير.
Day 4 explained a weighted LightGBM model, but my final choice is Logistic Regression, so those explanations do not directly describe the final model. I would redo the importance and reason codes on the final model.
## المتابعة والقيود | Monitoring and limitations
Each period I would check drift in key features such as bureau_score and dti, the share flagged against the 12% capacity, calibration (Brier and ECE) once outcomes mature, and false positive rate and recall by region.
OOF يستخدم للاختيار، وثلاث فترات ليست اختبار دلالة. العتبة قد تتغير سعتها عند نقلها إلى نموذج معاد التدريب. لا تسميات للتحدي، ولا مقاييس أداء أو شهادة عدالة له. البيانات لا تمثل أشخاصًا أو مناطق حقيقية.
## إعادة الإنتاج | Reproducibility
seed=211; trees=80; CPU مجاني. الإصدارات في artifacts/environment.json. المصادر/بصماتها في artifacts/day5_run.json. النموذج artifacts/final_model؛ inference.predict يعيد ID واحتمالًا؛ السياسة تطبق بعد جمع الدفعة. replay_final يعيد التنبؤ المحفوظ؛ rebuild_final يعيد التدريب. لا تدرب النموذج بعد تثبيت المعاير.
## ملكيتك للتسليم | Submission ownership
أكمل أدلة الأيام السابقة والعرض، واحفظ الدفتر المنفذ، ثم سجل SHA وtag مستودعك في قناة التسليم الخاصة. دعم الدورة f486fc50dd9ac8403016facc58cf6a62beb4abf4 ليس SHA تسليمك.
