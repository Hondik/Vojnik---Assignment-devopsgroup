Task D - Pod in CrashLoopBackOff

The pod is crashing because index.js is configured to throw an error 1 second after the container startup. This causes the Kubernetes pod to fail repeatedly. We can verify this with "kubectl logs deployment/deploy_name -c demo". On startup the first log will be "Starting app…", followed by "App crashed on purpose!"

Task E - Secret not mounted as ENV 

I didn't find any issue with the deployment.yaml and secret.yaml at first glance. However, as mentioned in assignment "fix namespace/application mismatch or missing resource", the only problem I could see is that the deployment and secret are in different namespaces. The db-secrets is for sure in the default namespace, but it's not clear which namespace the deployment is in. Debugging without printing secret in logs:

kubectl get secrets - check if the secret exists

kubectl describe secret db-secret - check content of the secret

kubectl describe deployment deploy_name - verify if the deployment is correctly referencing the secret
