****Reddit Clone with Kubernetes Ingress for DevOps Engineer****

**Prerequisites**

1. EC2 ( AMI- Ubuntu, Type- t2.medium )
2. Docker
3. Minikube
4. kubectl

1. I have created two servers name as “Continuous Integration” and “Deployment Server”

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/6e38ef74-b2e1-46c8-b102-e80de508040f/Untitled.png)

1. Now, Initially I have connected with “Continuous Integration” server.
2. Now I have to export the Github Code into ““Continuous Integration” server”, for the same I have used the command as : git clone_github_code_link

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/3784b959-8635-4909-9e53-c7e54b2ad6b3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/22738892-8f95-4d65-9b01-1aac5fd626b1/Untitled.png)

**Building The Code**

1. “cat Docker” to see what is in the docker file

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/e35e4d8a-d4ed-4803-868b-ccf85be6d0c4/Untitled.png)

1. “vim Dockerfile” to open the docker file
2. Now I had Logged in Docker tool, to take my reddit docker name.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/aa2526c6-59b1-41d5-9d39-dcb328ab8798/Untitled.png)

1. Now To build the image, in the terminal used command : docker build . -t girishdevops/reddit-clone 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/63cba1ce-9284-40d6-88ed-c51e263ac5df/Untitled.png)

**Push Image into Dockerhub**

1. To login into docker, command used : docker login

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/e46d1ba0-683d-488c-9f9b-48590978478b/Untitled.png)

1. Successfully logged in, and now to PUSH the image. command used : 

       docker push <DockerHub_Username>/<Imagename>

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/41180eac-fc8c-415f-8ca2-32429ff58e57/Untitled.png)

1. Now when I opened Docker Console, I can see, I have successfully pushed image here

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/8ce67726-a186-4535-8cf6-a2775a243a9e/Untitled.png)

Connect with K8 Server (Deployment Server)

1. Successfully connected with k8 instance and completed prerequisites

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/34b7c8c2-a4e5-4853-937c-df223bdbdb8f/Untitled.png)

1. To install minikube, I used Following Commands:

```
# For Minikube & Kubectl
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

sudo snap install kubectl --classic
minikube start --driver=docker
```

1. After installation, Deployment of Kubernetes
2. I have created an .yml file for kuberenetes(k8s) and wrote below yml code.

apiVersion: apps/v1
kind: Deployment
metadata:
name: reddit-clone-deployment
labels:
app: reddit-clone
spec:
replicas: 2
selector:
matchLabels:
app: reddit-clone
template:
metadata:
labels:
app: reddit-clone
spec:
containers:
- name: reddit-clone
image: girishdevops/reddit-clone
ports:
- containerPort: 3000

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/f3afd16f-3d5a-4207-b8f0-5cdc2fed619e/Untitled.png)

1. Now to deploy the same, I used command as : kubectl apply -f deployment.yml

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/eb2f71c8-a7d2-4b7e-85d1-628095e19ffc/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/48f2c6a9-c721-470f-838d-481c1645affb/Untitled.png)

1. And I have created deployment successfully.

1. Now to access the Pod file,I have created service.yml file and wrote below code

apiVersion: v1
kind: Service
metadata:
name: reddit-clone-service
labels:
app: reddit-clone
spec:
type: NodePort
ports:

- port: 3000
targetPort: 3000
nodePort: 31000
selector:
app: reddit-clone

1. This way I have successfully deployed service file. Now to access the application command used as : minikube service reddit-clone-service --url

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/588d8850-0d04-45fa-a9b4-573ee3d631d9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0d7b0c79-b88d-454f-a6c3-31736ac720c2/8b50ed0a-af88-407e-b4ad-f1073e810f1a/Untitled.png)

1. **And This way I have successfully Deployed a Reddit Copy on Kubernetes with Ingress Enabled.**
