1. Install kubectl inside 

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/


2.Install kind 
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-amd64 
chmod +x ./kind 
sudo mv ./kind /usr/local/bin/kind
verify kind:
kind version

3. Then Create Cluster
kind create cluster --config kind.yaml
Verify Cluster
kubectl get nodes

4. bUILD docker image:(only build)
5.nano ~/.aws/credentials
6. docker run -d -p 8081:8081 image(task 2)
(there will be error regarding connection)
- change flaskapp.py and docker file and rebuild again and run the same 

7. task 3: tag and push to ecr

8. Task 4: kubectl get nodes

9. Task 5: create namespace: kubectl create ns test
kubectl apply -f deployment.yaml -n test (you will get doesnot match label error)
chanfe the name and port in deployment, port and match label to same as up
check the version as well

grep -r apiVersion .

kubectl apply -f deployment.yaml
kubectl get pods -n test (if there is error, kubectl describe pods pod_name -n test)

create secret:
kubectl create secret generic ecr-reg-cred --from-file=.dockerconfigjson=/home/ec2-user/.docker/config.json \--type=kubernetes.io/dockerconfigjson -n test

k describe secret ecr-reg-cred -n test

kubectl delete pod -n test --all

kubectl apply -f deployment.yaml

Task 6: 

kubectl scale deployment flask-app --replicas=3 -n test
kubectl get deploy -n test
kubectl get pods -n test


Task 7:

kubectl apply -f serviceClusterIp.yaml -n test
kubectl get svc -n test

kubectl port-forward svc/flask-app 8081:80 -n test( if stuck change the servicecluster)


Task 8:
check the nodeport:30000
targetport :8081
change the sg

kubectl apply -f serviceNodePort.yaml -n test
 kubectl get svc -n test
kubectl describe svc flask-app -n test

http://100.26.176.116:30000/






