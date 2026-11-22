# HW4 — Short Answers

Answer each question in 2–3 sentences.

## 1. Rolling-update safety
Why does the Deployment use `maxUnavailable: 0`, and what would change if it were `maxUnavailable: 1`?

> If you were to change the Deployment use to `maxUnavailable:1`, then available application capacity could temporarily be reduced from three replicas to two. For fraud detection, maintaining service availability is critical because downtime could prevent transactions from being checked for fraud, potentially opening customers and the bank to security risks. 

## 2. Health probes
Why do the liveness/readiness probes target `/health` instead of `/predict`?

> We want to check the status of the pods without calling on the inference model, which will use compute with every call. In addition, `/predict` could depend on external services that may be temporarily unavailable or slow, causing false health check failures and potentially unnecessary pod restarts.

## 3. Autoscaling under load
Your HPA scales at 40% CPU up to 8 pods. If request volume doubled, what would you expect to happen — and what happens once it reaches the maximum?

> When traffic doubles, the HPA will continue to add pods up to the maximum of 8 to attempt to maintain an average CPU utilization of 40% across the pods. However, once the deployment reaches eight pods, no more can be added so so CPU utilization may rise above the 40% target if demand continues increasing. The application may experience slower responses, timeouts, or failed requests past this point.

### AI use statement

> ChatGPT was used to help interpret assignment instructions, guide command line operations in GitHub codespaces and in Azure, and help to troubleshoot when the Azure container apps environment stalled during provisioning. All deployment code updates in the starter files were written by me. ChatGPT reviewed Kubernetes concepts and reviewed the technical accuracy and wording of my short answers. I performed the deployment tasks. [Conversation here](https://chatgpt.com/share/6b037dc0-6da0-83e9-8747-846479cc896a)