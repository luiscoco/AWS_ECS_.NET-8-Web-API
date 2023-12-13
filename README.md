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

We log in to AWS 

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/9f3ba668-f211-4ff8-b230-8363b9c6f9c4)

We navigate to the AWS ECR service

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/8e236978-c8d5-4494-a029-b804b0611721)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/909d32cc-1239-4c33-9908-228bd3a7895a)

We create a new Public Repository

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/96748a26-35fd-4dc4-bc47-bf11acf8bbfd)

Set the Public repo name

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/e570f7c1-76b1-463b-8373-4ca2458b9f18)

We select the operating systems and system architectures that are compatible with the images in your repository

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/91d44745-9f2e-47bd-b18f-820507bfc989)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/bc52e8c5-19ac-4718-82b3-da097f14aa57)

We can see the new repo

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/3fd1a550-2198-4452-9c3c-3ee82cb1bb4b)

We have to upload the Web API docker image to the AWS ECR repo. We press in the "**View push commands**" button:

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/e23eafa3-d8f8-4729-8e58-a3d852bbf21b)

These are the commands we have to execute in the Visual Studio Terminal Window

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/3cb075c8-1951-4ea2-b817-cf96a14af358)

We right click on the project and select the option "**Open in Terminal**"

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/5015bab8-8183-482e-8cc1-436aef7091c8)

```
aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/x6y4g2f4
```

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/a22835ad-470c-412b-bc9d-f68256460429)

```
docker build -t examplepublicrepository .
```

```
docker tag examplepublicrepository:latest public.ecr.aws/x6y4g2f4/examplepublicrepository:latest
```

```
docker push public.ecr.aws/x6y4g2f4/examplepublicrepository:latest
```

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/e5c0c9b4-424f-40d9-83bf-9eafa61df0a9)

We verify in AWS ECR repo the uploaded docker image

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/5bb82c5d-8074-476b-9fd9-6f8a61290c05)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/108b0c1b-84f6-47b1-9087-b82fdfe6b45b)

## 3. Create a new Cluster in AWS ECS

We navigate to the AWS ECS service 

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/1787a21c-6ab8-4bcf-a6a1-22af5022c642)

We press the **Create cluster** button

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/afbfcd89-7e01-4d29-8ad4-9283178c5f26)

We set the cluster name and we press the **Create** button. Pay attention we selected the option **AWS Fargate (serverless)**

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/a991b7fd-2273-467a-8213-bbaf7eee748d)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/132acef8-657f-4cb5-8033-60f14efae0ff)

## 4. Create a new role in the IAM service

We navigate to the IAM service 

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/de9f0ecd-ad68-40a9-9358-9ff81af435b0)

We create a new role

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/3b68cd86-d0d8-4bc0-b499-e7d4b3cebc87)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/ee79a1b3-31fc-4711-9f26-f475e5fac3bb)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/1a4aa0be-90e6-47d3-85e6-7080a5eb93c1)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/135e8d0d-2ada-42f8-82b1-4a378253cad3)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/9785262c-9297-4702-9218-49eab3408500)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/c0cbd717-1b3b-4ab6-838b-03d0b15b7b03)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/be053297-adb5-4d3e-9594-630732a57425)


## 5. Create a new Task definition in AWS ECS

We create a new task definition

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/f5cf8e1e-8fc1-44ab-96a1-0d3fb642f160)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/4949eff0-67f3-4461-9bf2-f787f3b57556)

We set the CPU (2 Uds) and the Memory (8 GB). The "Task role" we set to "None" and in "Task execution role" we set to "ecsTaskExecutionRole"

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/d843f4ed-9502-4818-b00d-5766da231c7d)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/e5695f9b-95c6-48cb-8bfc-590107ec926b)

Copy the environmental variables values in the launchSettings.json file

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/49bde447-c8ac-47b2-909b-d0ffc108fb06)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/30885717-22f8-4e4f-a324-603ff3bc9361)

Press the **Create** button

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/d80b0aa0-af01-4187-89fc-6f19ce7f42e0)

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/332b3bc8-acd5-47ce-9057-4958d545fd22)

## 6. Create a new Service in AWS ECS

We input in the new Cluster and we create a new service

![image](https://github.com/luiscoco/AWS_ECS_deploy_.NET_7_Web_API/assets/32194879/18ea4374-a2a2-417a-a2fa-cb19f525a30b)



## 7. Access to the Web API application enpoint




