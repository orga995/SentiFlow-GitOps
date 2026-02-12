# SentiFlow-GitOps
SentiFlow GitOps Repository 🚀
מאגר זה מנהל את המצב הרצוי (Desired State) של אפליקציית SentiFlow בתוך קלאסטר ה-Kubernetes (EKS) באמצעות ArgoCD.
+1

🛠 דרישות קדם (Prerequisites)
קלאסטר EKS פעיל (הוקם באמצעות מאגר SentiFlow-Infra).
+1

כלי ה-CLI של kubectl מותקן ומחובר לקלאסטר.

ArgoCD מותקן על הקלאסטר.
+1

🔑 גישה לממשק ArgoCD
כדי לגשת לממשק הניהול של ArgoCD, הרץ את הפקודה הבאה כדי לבצע Port Forwarding:

Bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
כעת ניתן לגשת לממשק בכתובת: https://localhost:8080.

פרטי התחברות:

User: admin

Password: ניתן לקבל את הסיסמה הראשונית באמצעות הפקודה: kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

🚀 פריסת האפליקציה (Deployment)
הפריסה מתבצעת באופן אוטומטי בשיטת GitOps. ברגע שמתבצע שינוי ב-Helm Charts במאגר האפליקציה או בקבצי ה-YAML במאגר זה, ArgoCD יזהה את השינוי ויבצע סנכרון לקלאסטר.
+1

הוספת האפליקציה ל-ArgoCD ידנית (במידת הצורך):
לחץ על New App.

Application Name: sentiflow.

Project: default.

Sync Policy: Automatic.

Repository URL: הלינק למאגר זה.

Path: הנתיב לתיקיית ה-Environment הרלוונטית (Staging/Production).

Cluster URL: https://kubernetes.default.svc.

Namespace: sentiflow.
