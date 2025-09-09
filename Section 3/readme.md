Task A - Production went down

1. 
If there was a recent app update, check what was changed. This could indicate where the problem is coming from.
- kubectl rollout history

2.
List the deployments and other related components, verify their statuses.
- kubectl get all - check pods, deployments, svc

3.
Describe the deployment and pods, and check if there is a problem in the Events section. If not, log the pods with kubectl logs.
- kubectl describe deploy
- kubectl describe pods
- kubectl logs ...

4.
If no issues are visible in the logs, check the services if they have endpoints.
- kubectl describe svc

5.
Verify if the worker nodes are functioning correctly
- kubectl get nodes

6.
If the application seems fine, check the controlplane components, if everything is running as expected.
- kubectl get pods -n kube-system

At this point, it should be clear if the problem is application-related (and where exactly) or if it is cluster-related.
