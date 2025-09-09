Task C - Deploy Kubernetes App with Helm

The first step was to download the nginx chart from the Bitnami registry and extract it.
- helm pull oci://registry-1.docker.io/bitnamicharts/nginx tar -xvzf nginx-21.1.23.tgz

After that, I installed the chart under the name nginx-test and checked if everything is running fine.
- helm install nginx-test nginx

After this point, there was 1 nginx pod and service of type LoadBalancer. Assignment required ingress, so I modified the values.yaml.
- Changed service.type to ClusterIP (values.yaml, line 674)
- Changed ingress.enabled from false to true (values.yaml, line 800) 

Then I reinstalled the app and tested if everything has changed as issued.
However when I described nginx-test ingress, it didn't have a class and address because the cluster was missing an ingress controller.
To fix this, I installed the nginx ingress controller with Helm (from bitnami hub - bitnami/nginx-ingress). 

Finally, I updated the original nginx app by setting the ingressController name:
- ingressClassName: nginx (values.yaml, line 832)

After deploying again I checked all the pods, svc, ingress and ingressClass. Ingress now had an IP and class.

As the last step, I tested ingress with Curl:
- curl -H "Host: nginx.local" http://192.168.56.21:30135
  - nginx-local was required by ingress rule
  - the IP was the worker node address and port belonged to nginx ingress controller 

The response returned the default nginx page, which confirmed that ingress was working as expected.

