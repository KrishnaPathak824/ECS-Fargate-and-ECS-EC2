# Assignment:

#### 1. Single-Container Deployment (Type: Fargate)

- Create an ECS Cluster
- Define a Task Definition for your BE Application(from previous assignment)
- Launch an ECS Service:
- Deploy the task definition as an ECS service and ensure it's running successfully.

**_Answer:_**

- Created an ECS Cluster named `cluster-krishna`.
- Chose the Fargate infrastructure in the cluster

![alt text](materials/image.png)

- Chose the container insights option to monitor the cluster.

![alt text](materials/image-1.png)

- Added tags to the cluster.

![alt text](materials/image-2.png)

- The cluster was created successfully.

![alt text](materials/image-3.png)

- Created Task Definition with Fargate launch type. It uses the `awsvpc` mode by default by the AWS Fargate launch type.

![alt text](materials/image-4.png)

- The task definition was given 1 vCPU and 3 GB of memory.

![alt text](materials/image-5.png)

- The container was created `backend` and the image is `jhinga/backend-1:latest-2`.

![alt text](materials/image-6.png)

- The container port is set to 3000 since the backend application runs on port 3000.

![alt text](materials/image-7.png)

![alt text](materials/image-8.png)

- The task definition was created successfully.

![alt text](materials/image-9.png)

- The task definition was created with the fargate launch type and the awsvpc network mode.

![alt text](materials/image-10.png)

- The task definition had one container backend1.

![alt text](materials/image-11.png)

- Navigated to the ECS service and created a new service.

![alt text](materials/image-12.png)

- Chose the created task definition and the launch type as Fargate.

![alt text](materials/image-13.png)

![alt text](materials/image-14.png)

- The desired number of tasks is set to 1 which means one task will be running even if one task fails.

![alt text](materials/image-15.png)

- The vpc was selected of my group and the public subnets were selected.

- The security group was selected that allows inbound traffic on port 3000.

![alt text](materials/image-16.png)

- The service was created successfully.

![alt text](materials/image-18.png)

![alt text](materials/image-19.png)

- The service was active and the task was running but I had given a wrong docker image name so the task was not running.

![alt text](materials/image-21.png)

- Created a new task definition revision with the correct docker image name.

![alt text](materials/image-23.png)

- Updated the ECS service to use the new task definition revision and the task was running successfully.

![alt text](materials/image-24.png)

- The public IP of the task was used to access the backend application.

![alt text](materials/image-28.png)

- At / the backend threw an error not found.

![alt text](materials/image-25.png)

- I had created an api endpoint /backend which returns a message which was running successfully.

![alt text](materials/image-26.png)

- I tried to stop the task but it was running again since the desired number of tasks is set to 1.

![alt text](materials/image-29.png)

![alt text](materials/image-30.png)

![alt text](materials/image-31.png)

- So I updated the service to 0 desired tasks and the task was stopped.

![alt text](materials/image-32.png)

---

#### 2. Single-Container Deployment (Type: EC2 / EC2 Spot)

- Create an ECS Cluster
- Create Launch Template & ASG Manually
- Use ASG as an capacity Provider
- FE Application(from previous assignment) (Bridge Mode: Should get a Public IP)
- Deploy the task definition as a single task and ensure it's running successfully.

**_Answer:_**

- Navigated to the Launch Templates and created a new launch template.

![alt text](materials/image-33.png)

- The launch template was created and i selected the auto scaling guidance.

![alt text](materials/image-34.png)

- I chose the AMI as Amazon Linux and the instance type as t2.micro.

![alt text](materials/image-35.png)

![alt text](materials/image-37.png)

- I then selected the existing security group which allows inbound traffic on port 80.

![alt text](materials/image-38.png)

![alt text](materials/image-39.png)

- The launch template was created successfully.

![alt text](materials/image-40.png)

- I then created an Auto Scaling Group with the launch template.

![alt text](materials/image-42.png)

![alt text](materials/image-43.png)

- I chose the VPC of my group and the public subnets.

![alt text](materials/image-44.png)

![alt text](materials/image-45.png)

- I configured the auto scaling group to have a minimum of 1 instance and a maximum of 21 instance mistakenly. Later I changed it to 3.

![alt text](materials/image-46.png)

- Added the tags to the auto scaling group.

![alt text](materials/image-47.png)

- The auto scaling group was reviewed and created successfully.

![alt text](materials/image-48.png)

![alt text](materials/image-49.png)

![alt text](materials/image-50.png)

- I then created an ECS cluster with the EC2 launch type.

![alt text](materials/image-51.png)

- I chose the Amazon EC2 infrastructure option where I chose the auto scaling group as the capacity provider.

![alt text](materials/image-52.png)

- The cluster was created successfully.

- A new task definition was created with the bridge network mode and the cpu was set to 1 vCPU and 2 GB of memory.

![alt text](materials/image-53.png)

![alt text](materials/image-55.png)

- The container was created with the image `jhinga/frontend:latest` and the port of the container and the host was set to 80.

![alt text](materials/image-56.png)

- I also created a new service with the task definition and the capacity provider as the auto scaling group.

![alt text](materials/image-57.png)

![alt text](materials/image-58.png)

- The task was in provisioning state and was not running.

![alt text](materials/image-71.png)

- I used the instance public IP to manual ssh into the instance and check the logs.

![alt text](materials/image-73.png)

- **_I realized my mistakes while creating the launch template. I had not selected the ami that was ECS optimized. I also had not included the user data script to configure the ECS agent._**

- I used the key pair created in the launch template to ssh into the instance.

![alt text](materials/image-72.png)

- I installed docker in the instance.

![alt text](materials/image-74.png)

- **_I also had forgot to add the IAM instance profile for the EC2 container service._**

![alt text](materials/image-75.png)

- I started docker service inside the instance.

![alt text](materials/image-76.png)

- I then installed the ecs agent in the instance.

![alt text](materials/image-77.png)

- I then included the cluster name in the ecs config file.

![alt text](materials/image-78.png)

- The ECS agent was running successfully but the task was still not running.

![alt text](materials/image-79.png)

- **_I then realized that I had created the task definition with 1 vCPU and 2 GB of memory but the instance type was t2.micro which has only 1 GB of memory._**

---

## Final Workflow of Task 2:

1. **_First, I created the cluster without any infrastructure._**

![alt text](materials/image-82.png)

2. **_Then I created the launch template where i selected the ECS optimized AMI._**

![alt text](materials/image-80.png)

![alt text](materials/image-81.png)

- I chose the instance type as t2.micro.

![alt text](materials/image-83.png)

- Selected the existing security group which allows inbound traffic on port 80.

![alt text](materials/image-84.png)

- I also enabled auto assign public IP and added the IAM instance profile for the ECS container service.

![alt text](materials/image-86.png)

- Then used the user data script to include the ECS cluster into the config file.

```bash
#!/bin/bash
echo ECS_CLUSTER=krishna-cluster-trying >> /etc/ecs/ecs.config
```

![alt text](materials/image-87.png)

- The launch template was created successfully.

3. **_Then I created the auto scaling group with the launch template._**

- I chose the launch template created above.

![alt text](materials/image-88.png)

![alt text](materials/image-89.png)

- I then chose the VPC of my group and the public subnets.

![alt text](materials/image-90.png)

- I then configured the auto scaling group to have a minimum of 1 instance and a maximum of 2 instances.

![alt text](materials/image-91.png)

![alt text](materials/image-92.png)

- The auto scaling group was created successfully.

4. **_Created a capacity provider with the auto scaling group created above and attached it to the ECS cluster._**

- Navigated to the ECS cluster and created a new capacity provider.

![alt text](materials/image-93.png)

- The capacity provider was created with the auto scaling group.

![alt text](materials/image-94.png)

- The capacity provider was attached to the ECS cluster.

![alt text](materials/image-95.png)

![alt text](materials/image-96.png)

5. **_Created a task definition with the bridge network mode._**

- Created a new task definition with the bridge network mode.

- Selected `.25` vCPU and `.5` GB of memory.

![alt text](materials/image-98.png)

- The container was created with the image `jhinga/frontend:latest` and the port of the container and the host was set to 80.

![alt text](materials/imagee.png)

![alt text](materials/image-99.png)

6. **_Created a new service with the task definition and the capacity provider as the auto scaling group._**

![alt text](materials/image-100.png)

- The capacity provider was selected as the auto scaling group created above.

![alt text](materials/image-101.png)

- The service was created successfully and the task was running successfully.

![alt text](materials/image-102.png)

- The public IP of the task was used to access the frontend application.

![alt text](materials/image-103.png)

- The frontend application was accessible at `34.201.110.5`

![alt text](materials/image-104.png)

---

### 3. Multi-Container Deployment (Type: EC2/EC2 Spot) (Bridge) (1 frontend, 1 backend)

- Create a ECS Cluster
- Create a Task Definition with multiple-container
- Create an ECS Service:
  - Deploy the task definition as an ECS service and ensure it's running successfully browsing it by its public IP
  - Use ASG On-Demand/Spot as capacity provider

**_Answer:_**

1. **_Created a new ECS cluster and selected no infrastructure._**

![alt text](materials/image-117.png)

2. **_Created a new launch template with the ECS optimized AMI and the instance type as t3.medium._**

![alt text](materials/image-108.png)

- Chose the instance type as t3.medium.

![alt text](materials/image-109.png)

- Selected the existing security group which allows inbound traffic on port 80 for frontend and 3000 for backend.

![alt text](materials/image-110.png)

- The IAM instance profile for the ECS container service was selected.

![alt text](materials/image-111.png)

- Then used the user data script to include the ECS cluster into the config file.

```bash
#!/bin/bash
echo ECS_CLUSTER=krishna-fe-be-cluster >> /etc/ecs/ecs.config
```

![alt text](materials/image-112.png)

- The launch template was created successfully.

![alt text](materials/image-113.png)

3. **_Created an auto scaling group with the launch template._**

- Chose the launch template created above.

![alt text](materials/image-114.png)

- I chose the VPC of my group and the public subnets.

![alt text](materials/image-115.png)

- The auto scaling group was configured to have a minimum of 1 instance and a maximum of 2 instances.

![alt text](materials/image-116.png)

- The auto scaling group was created successfully.

4. **_Created a capacity provider with the auto scaling group and attached it to the ECS cluster._**

- Navigated to the ECS cluster and created a new capacity provider.

![alt text](materials/image-118.png)

- The capacity provider was created with the auto scaling group created earlier.

![alt text](materials/image-119.png)

- It was successfully attached to the ECS cluster.

5. **_Created a task definition with multiple containers._**

- Created a new task definition with the bridge network mode and the launch type as EC2.

![alt text](materials/image-120.png)

- The task definition was given 1 vCPU and 2 GB of memory.

![alt text](materials/image-121.png)

- The first container was created with the image `jhinga/frontend:latest` and the port of the container and the host was set to 80.

![alt text](materials/image-122.png)

- The second container was created with the image `jhinga/backend-1:latest-2` and the port of the container and the host was set to 3000.

![alt text](materials/image-123.png)

6. **_Created a new service with the task definition and the capacity provider as the auto scaling group._**

- The task definition created above was selected while creating the service.

![alt text](materials/image-124.png)

- The capacity provider was selected as the auto scaling group created earlier.

![alt text](materials/image-125.png)

- The service was created successfully and the task was in provisioning state for a minute before it was running successfully.

![alt text](materials/image-126.png)

- The public IP of the task was used to access the frontend and backend applications.

![alt text](materials/image-127.png)

- The frontend application was accessed using the public IP `3.238.0.153`.

![alt text](materials/image-128.png)

- The backend application was also accessed using the public IP and the port 3000.

At / it threw an error not found.

![alt text](materials/image-129.png)

- At /api/users it returned database error since the database is not connected.

![alt text](materials/image-130.png)

The multi-container deployment was successful with one frontend and one backend container running in the same task.

---

#### 4. What are the placement strategies in the AWS ECS? Explain briefly. At last compare which strategy should be used in which scenario.

**_Answer:_**

[Reference to placement strategies](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-strategies.html)

Placement strategies in AWS ECS are used to determine how tasks are placed on container instances within a cluster.

A task placement strategy is an algorithm for selecting instances for task placement or tasks for termination. When a task that uses the EC2 launch type is launched, Amazon ECS must determine where to place the task based on the requirements specified in the task definition, such as CPU and memory.

Task placement strategy types:

1. **Spread**: This strategy spreads tasks across available instances based on specified attributes (e.g., instance ID, availability zone). It is useful for maximizing availability and fault tolerance.

2. **Binpack**: This strategy places tasks on the least utilized instances based on specified resource requirements like CPU, memory. It is useful for optimizing resource utilization and reducing costs.

3. **Random**: This strategy places tasks randomly across available instances. It is useful for testing and development purposes.

The choice of placement strategy depends on the specific requirements of the application and the desired trade-offs between availability, resource utilization, and cost.

For example, a web application with high availability requirements may benefit from the spread strategy, while a batch processing application with flexible resource requirements may benefit from the binpack strategy.

---

### Bonus:

- Configure/Update the ECS Service of Q.3 so that you will be able to execute commands inside both ECS container separately.
  - e.g. aws ecs execute-command

**_Answer:_**

![alt text](image.png)

![alt text](image-2.png)

![alt text](image-3.png)
