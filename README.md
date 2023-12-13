# AWS ECS: How to deploy .NET 7 Web API

## 1. Create a Web API .NET 7 in Visual Studio 2022 Community Edition

Run Visual Studio 2022 and create a new Web API

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/f5d8cb5d-cdc2-4fcd-b2e0-4572914e5a22)

Select the Web API .NET Core template

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/792c5b66-9ace-401f-bb8f-6cef1bdca463)

We set the solution name and the location

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/62ed9296-46da-4f0f-b32b-733ed1c7ffb9)

We select the framework .NET 7, we Enable Docker(for automatically create the dockerfile), we Enable OpenAPI and Use controllers

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/aa807d3b-fac4-4986-a7df-8e09467dac3a)


## 2. Create the docker image and upload it to AWS ECR




## 3. Create a new Cluster in AWS ECS




## 4. Create a new Task definition in AWS ECS




## 5. Create a new Service in AWS ECS



## 6. Access to the Web API application enpoint




