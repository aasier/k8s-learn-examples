# k8s-learn-examples
https://kubernetes.io/docs/reference/kubectl/cheatsheet/

# 01 - Commands:

kubectl config get-contexts  # Check where we are working.

kubectl get namespaces # get all namespaces (Don´t remove default, kube-system, kube-...)

# Apply and delete from yaml file.

kubectl apply -f frontend-deployment.yaml
kubectl delete -f frontend-deployment.yaml

# Apply and Delete from yaml files in a directory

kubeclt apply -f . # Deploy all yaml files
kubectl delete -f . # Remove all objects from yaml files

# View resources:

kubectl get pods
kubectl get pods --all-namespaces
kubectl get services
kubectl get services --all-namespaces

# Edit resources:

kubectl edit pod 
kubectl edit deployment
kubectl rollout undo deployment/frontend

Exercise:
Create a namespace with your name and deploy this solution.

# 02 - Commands - Replicas:

# Increasing the replicas

more frontend-deployment.yaml
kubectl apply -f frontend-deployment.yaml

kubectl scale --replicas=3 frontend


# 03 - Commands Rolling Update

more frontend-deployment.yaml
kubectl apply -f frontend-deployment.yaml
kubectl top pod
kubectl top pod --all-namespaces

# 04 - Commands Limits / Request CPU / MEM

more frontend-deployment.yaml
kubectl top pod
kubectl apply -f frontend-deployment.yaml
kubectl top pod


# 05 - Commands Readiness Liveness

kubectl apply -f frontend-deployment-fail.yaml
kubectl apply -f frontend-deployment-ok.yaml

https://blog.colinbreck.com/kubernetes-liveness-and-readiness-probes-how-to-avoid-shooting-yourself-in-the-foot/

        livenessProbe:
          httpGet:
            path: /version
            scheme: HTTP
            port: 80
          initialDelaySeconds: 15
          periodSeconds: 60
          timeoutSeconds: 60
        readinessProbe:
          httpGet:
            path: /version
            scheme: HTTP
            port: 80
          initialDelaySeconds: 15
          periodSeconds: 60
          timeoutSeconds: 60

        livenessProbe:
          exec:
            command:
            - cat
            - /tmp/healthy
          initialDelaySeconds: 5
          periodSeconds: 5


# 06 Commmands Logs

kubectl logs pod_name
kubectl logs pod_name | grep "error"


