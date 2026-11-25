# Tamweel Lite | مشروعك النهائي

## الملخص التنفيذي
اخترت نموذج Logistic Regression نموذجًا نهائيًا لأنه حقق أعلى متوسط AP وهو 0.392، مقابل 0.345 لـ LightGBM و0.353 لـ XGBoost، ولم يتجاوز أي تجميع شرط التحسن. حددت العتبة عند 0.169، فتم تمييز 11.4% من الطلبات ضمن سعة المراجعة البالغة 12%. هذا العمل تدريبي على بيانات اصطناعية ولا يصلح لقرارات حقيقية.

## Executive summary
I chose Logistic Regression as the final model because it had the highest mean AP (0.392, versus 0.345 for LightGBM and 0.353 for XGBoost), and no ensemble passed the improvement gate. With a threshold of 0.169, 11.4% of applications are flagged, within the 12% review capacity. This is a training exercise on synthetic data, not for real decisions.

Decision: KEEP SINGLE / Logistic. Full-batch flags: 300/2500.

اقرأ reports/MODEL_CARD.md والسياسة في artifacts/final_policy.json. الحزمة للتدريب؛ ليست نتيجة تقييم نهائية أو إثبات تسليم. ادمج أدلة أيامك السابقة واحفظ الدفتر المنفذ والعرض.
