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






