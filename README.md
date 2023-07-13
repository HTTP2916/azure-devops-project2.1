# Overview

Hello, I am Phung, this is project 2 (CICD) in Nanodegree for DevOps Engineer using MS Azure from Udacity.

This project consists of flask application that is developed to predict housing prices in Boston (the model is already created by the instructor). 

This repositry demonstrate:
- Deploying the app in Azure CloudShell
- Deploying the app as a web server using Azure App Service.

If anything changed in it repository,  it will trigger the Github Action and also the Azure DevOps Pipelines to perform the CICD process and finally deploy to my app service.

## Badge

[![Python application test with Github Actions](https://github.com/HTTP2916/azure-devops-project2.1/actions/workflows/pythonapp.yml/badge.svg)](https://github.com/HTTP2916/azure-devops-project2.1/actions/workflows/pythonapp.yml)

## Project Plan

A [Trello](https://trello.com/b/3YsyayTe/build-cicd-pipeline-for-azure-devops) board to keep track of the tasks.

A [spreadsheet](project-schedule-h.xlsx) to manage the project plan.

## Instructions

Here is an architectural diagram:

![diagram](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/23a8a585-aed0-4b76-acd6-b38a9294ab31)


## Deploy the app in Azure Cloud Shell

In Azure Cloud Shell, clone the repo:
```
git clone git@github.com:HTTP2916/azure-devops-project2.1.git
```
![screenshot-gitClone-AzureCloud](![git_clone2](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/c213ce60-fdf9-4b3b-a2ae-6b8a59e49359)
)


Change into the new directory:
```
cd azure-devops-project2.1
```

Change to branch "ci-to-git-action"

```
git checkout ci-to-git-action
```

Create a virtual environment:
```
python3 -m venv ~/.myrepo
```

Activate the virtual environment:
```
source ~/.myrepo/bin/activate
```

Install dependencies in the virtual environment and run tests:
```
make all
```
![make-all](![make_all](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/35202bf0-ff93-44d1-ac8e-a0b7d290d861)
)

Make change and test GitHub action
![screenshot-test-githubaction](![test_git_action](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/9a1d44fd-f73b-4bb2-8f87-8e3806ca12a7)
)

## Deploy the app to an Azure App Service

Create an App Service in Azure. 

Use this [file](https://github.com/HTTP2916/azure-devops-project2.1/blob/main/commands.sh) to create new App Services

```
az webapp up -n azure-devops-project2
```

Next, create the pipeline in Azure DevOps. The basic steps are:

- Go to [https://dev.azure.com](https://dev.azure.com) and sign in.
- Create a new private project.
- Create a new service connection to ARM, select subscription and the app service.
- Create a new pipeline linked to your GitHub repo using GiThub YAML File.

Screenshot of the App Service:

![My WebApp](![web_app](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/9b6fe9a3-e68b-40c7-9d5c-015794feb94c)
)

Screenshot of Azure DevOps Project:

![My_DevOps](![azure_devops](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/fc7b1330-8928-4cb7-bac9-d3ee849f64eb)
)

To test the app running in Azure App Service, edit line 28 of the make_predict_azure_app.sh script with the DNS name of your app. Then run the script:
```
./make_predict_azure_app.sh 
```

If it's working you should see the following output:

![screenshot-prediction](![prediction](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/4d03e8bb-cb05-4210-82ba-7e5713fe991a)
)

You can also visit the URL of the App Service via the browser and you should see the following page:

![screenshot-browser](![app](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/f613a5d0-ec2b-4f20-a57e-9296dacb5808)
)

View the app logs:

To view the log in Cloud Shell
```
az webapp log tail -g Azuredevops -n azure-devops-project2-phunghtt
```
![screenshot-log-webapp](![webapp_trail](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/b13c76cb-73a8-47b5-bc4d-e47c11e0e39f)
)


> 

## Load test

I use locust to perform load test on my local computer. 

Install locust:
```
pip install locust
```

Start load test:
```
locust -f locustfile.py --host https://azure-devops-project2-phunghtt.azurewebsites.net/ --users 500 --spawn-rate 5 
```
Open a browser and go to [http://localhost:8089](http://localhost:8089) then click Start Swarming:

![screenshot-loadtest#1](![locust1](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/34e3edb0-c7fd-4ce0-8592-5d4acce73b2e)
)
![screenshot-loadtest#2](![locust2](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/48c94e1d-bf58-4d18-bafb-586f9bf83e47)
)
![screenshot-loadtest#3](![locust3](https://github.com/HTTP2916/azure-devops-project2.1/assets/50509460/9f0aaeaf-4bcb-4433-9b00-f15935099005)
)

## Future Enhancements
- Creating a UI for making predictions.
- Adding test cases.
- Deploying my app with AKS.

## Demo 
Demo Video on Youtube 
link
