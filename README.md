# Introduction-to-Helm-Chart
In this mini project, you will delve into the practical aspects of working with Helm charts, including installation, customization, and deployment of applications on Kubernetes clusters.



Helm is a package manager for Kubernetes applications. It simplifies the deployment and management of applications on Kubernetes by providing a way to define, install, and upgrade even the most complex Kubernetes applications. This practical exercise is designed for learners who are eager to dive into the world of Kubernetes, offering a hands-on experience with Helm, a key tool in modern cloud-native technology stacks. Throughout this project, you will learn how to utilize Helm to streamline the deployment and management of applications in a Kubernetes environment. By creating, configuring, and deplovina a simple web application, you'll gain valuable insights into the efficiencies Helm brings to Kubernetes application management. 
Imagine you're a chef in a large, busy kitchen. In this scenario, Kubernetes is the kitchen itself, equipped with all the necessary tools and stations, while the individual dishes you need to prepare are the applications. Now, Helm acts like a recipe book that not only contains recipes but also automates the preparation process. Each Helm chart is a recipe, specifying ingredients (containers, services, etc.) and the steps needed to create the dish (application). By using Helm, you're not just cooking one dish at a time; you're efficiently managing multiple dishes, ensuring each is prepared consistently and to the highest standard, no matter how busy the kitchen gets. This project will help you learn to be that efficient chef in the Kubernetes kitchen, making the process of deploying and managing applications as seamless as preparing a well-structured meal


**Step 1: Install Helm**

For macOS Users
1. Open Your vscode:
   
- Run you vscode as an administrator
  
- Access your CLI by opening the Terminal.

2. Download Helm:

```
curl -L https://get.helm.sh/helm-v3.5.0-darwin-amd64.tar.gz -o helm.tar.gz

```

3. Extract the Downloaded File:

```
tar -zxvf helm.tar.gz

```

4. Move the Helm binary

```
mv linux-amd64/helm /usr/local/bin/helm

```

5. Verify installation

```
helm version

```

6. Clean up

```
rm helm.tar.gz && rm -r *-amd64

```

Step 2: Create a New Helm Chart

Now that we have helm installed on our environment, let's create a helm chart

1. Create Project Directory:

```
mkdir helm-web-app

cd helm-web-app

```

2. Create a new chart

```
helm create webapp

```

3. Initialize a Git Repository:

```
git init
git add .
git commit -m "Initial Helm webapp chart"

```

4. Push to Remote Repository:
   
- Create a new repository on GitHub, GitLab, or your preferred Git hosting service.
  
- Follow the instructions provided by your Git service to push your local repository to the remote. For example:

![image](https://github.com/user-attachments/assets/11b88d2a-62ec-4831-a8f0-5b139dcc60f7)


![image](https://github.com/user-attachments/assets/d47fabc9-173f-4eb2-8998-8ea220381004)


![image](https://github.com/user-attachments/assets/8250fe3c-dec1-49e6-b240-7e0a8501dedb)



# Mini-Project---Working-with-Helm-Chart
Practical experience in creating, customizing, and deploying Helm charts for various applications.

# Step 1: Customize Your Helm Chart

**Understanding Helm Charts, Values, and Templates**

**Why Helm Charts Are Needed:**

- Helm charts are packages or collections of pre-configured Kubernetes resources.
  
- ﻿﻿They simplify the deployment and management of applications in Kubernetes by bundling all necessary resources into a single, manageable unit.
- ﻿﻿Helm charts promote reusability and consistency, allowing you to define, install, and upgrade even the most complex Kubernetes applications easily.
  
What Are Charts, Values, and Templates:

- Charts: A Helm chart is a directory with a predefined structure. It contains all the resource definitions needed to run an application, tool, or service inside a Kubernetes cluster. Think of it as a recipe with instructions on how to create and run a Kubernetes application.
  
- ﻿﻿Values: The 'values, yaml ' file inside a chart provides configuration values for a chart's templates. These values can be overridden during chart installation or upgrades, allowing for flexibility and customization without altering the chart's core logic.
  
- ﻿﻿Templates: The templates/ directory contains the template files. These are standard Kubernetes YAML files with placeholders (*{{" .Values. someParameter "}}'). Helm dynamically fills these placeholders with the values from the 'values. yaml' file or override values provided during runtime. This allows you to customize the deployment without changing the actual YAML files.
  
1. Explore the 'webapp' Directory:
   
Navigate to the 'webapp' directory created by Helm. Inside, you'll find:

- ﻿﻿'Chart.yaml': Contains metadata about the chart such as name, version, and description.
  
- ﻿﻿'values. yaml': Provides configurable values that Helm will inject into the templates. Here you set default configuration values.
  
- ﻿﻿'templates/': Contains the template files that will generate Kubernetes manifest files. These templates reference the values defined in 'values yaml'.
  
2. Modify 'values yaml':
   
- ﻿﻿Open 'values. yaml' in a text editor.
  
- ﻿﻿Set the image to use the Nginx stable version.

```
replicaCount: 2

image:
  repository: nginx
  tag: stable
  pullPolicy: IfNotPresent

```

<img width="783" alt="image" src="https://github.com/user-attachments/assets/0ebd4330-88a6-40cb-b6fe-cb2840ee24df" />

- This configuration will deploy two replicas (replicaCount: 2') of the Nginx server.
  
- Save your changes.

3. Customize 'templates/deployment.yaml' :
   
- Open the 'deployment.yaml' file in the templates/ directory.
  
- Remove the line below from under 'spec. template.spec.containers. resources'.

<img width="1107" alt="image" src="https://github.com/user-attachments/assets/4383dd43-cc9c-453d-b22e-179667fa115a" />


- Add a simple resource request and limit under ' spec. template.spec.containers. resources'. This helps Kubernetes manage resources           efficiently:

```
resources:
  requests:
    memory: "128Mi"
    cpu: "100m"
  limits:
    memory: "256Mi"
    cpu: "200m"

```

<img width="1067" alt="image" src="https://github.com/user-attachments/assets/9dc57fa3-1873-495e-8fe7-c1e5c0c20290" />

- These settings specify that your deployment should request 128Mi of memory and 100m of CPU, but it won't use more than 256Mi of memory and   200m of CPU.
  
- Save the file after making your changes.


4. Commit and Push Changes:


```
git add .
git commit -m "Customized Helm chart"
git push

```

![image](https://github.com/user-attachments/assets/202326c2-6b61-4f46-bb9d-834bc1aed336)



Step 2: Deploying Your Application


1. Deploy with Helm: Navigate to the root of your project directory ' helm-web-app'.
Deploy the the application on Kubernetes using the below command:


```
helm install my-webapp ./webapp

```

2. Check deployment

```
kubectl get deployments

```
![image](https://github.com/user-attachments/assets/dd04195d-830b-4c75-8400-e5c9a914cfa7)


3. Visit Application URL: Get the application URL by running these commands:


```
export POD_NAME=$(kubectl get pods -n default -l app.kubernetes.io/instance=my-webapp -o jsonpath='{.items[0].metadata.name}')

export CONTAINER_PORT=$(kubectl get pod $POD_NAME -n default -o jsonpath='{.spec.containers[0].ports[0].containerPort}')

kubectl --namespace default port-forward $POD_NAME 8081:$CONTAINER_PORT

```
![image](https://github.com/user-attachments/assets/c0daab4e-2ce2-41ea-8e79-615822e7d36f)

Visit http://127.0.0.1:8081 to use your application


![image](https://github.com/user-attachments/assets/0152b561-637c-4606-aa18-65efa44cb5e6)




