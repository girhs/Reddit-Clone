# Reddit-Clone
Reddit Clone with Kubernetes
Prerequisites
EC2 ( AMI- Ubuntu, Type- t2.medium )
Docker
Minikube
kubectl

Creating Servers
I have created two servers name as "Continuous Integration" and "Deployment Server"

2. Now, Initially I have connected with "Continuous Integration" server.
3. Now I have to export the Github Code into ""Continuous Integration" server", for the same I have used the command as :
git clone_github_code_link
Building The Code
"cat Docker" to see what is in the docker file

2. "vim Dockerfile" to open the docker file
3. Now I had Logged in Docker tool, to take my reddit docker name.
4. Now To build the image, in the terminal used command : docker build . -t girishdevops/reddit-clone
Push Image into Dockerhub
To login into docker, command used : docker login

2. Successfully logged in, and now to PUSH the image. command used :
3. Now when I opened Docker Console, I can see, I have successfully pushed image here
Connect with K8 Server (Deployment Server)
Successfully connected with k8 instance and completed prerequisites

2. To install minikube, I used Following Commands:
# For Minikube & Kubectl
curl -LO <https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64>
sudo install minikube-linux-amd64 /usr/local/bin/minikube
sudo snap install kubectl --classic
minikube start --driver=docker
3. After installation, Deployment of Kubernetes
4. I have created an .yml file for kuberenetes(k8s) and wrote below yml code.
apiVersion: apps/v1 kind: Deployment metadata: name: reddit-clone-deployment labels: app: reddit-clone spec: replicas: 2 selector: matchLabels: app: reddit-clone template: metadata: labels: app: reddit-clone spec: containers:
name: reddit-clone image: girishdevops/reddit-clone ports:
containerPort: 3000
5. Now to deploy the same, I used command as :
kubectl apply -f deployment.yml
6. And I have created deployment successfully.
7. Now to access the Pod file,I have created service.yml file and wrote below code
apiVersion: v1 kind: Service metadata: name: reddit-clone-service labels: app: reddit-clone spec: type: NodePort ports:
port: 3000 targetPort: 3000 nodePort: 31000 selector: app: reddit-clone
8. This way I have successfully deployed service file. Now to access the application command used as : minikube service reddit-clone-service - url
sAnd This way I have successfully…
🎉🥇 Deployed a Reddit Copy on Kubernetes 🏆✨💫
