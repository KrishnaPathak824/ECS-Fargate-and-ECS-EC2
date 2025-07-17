#### 1. Single-Container Deployment (Type: Fargate)
- Create an ECS Cluster
- Define a Task Definition for your BE Application(from previous assignment)
- Launch an ECS Service:
  - Deploy the task definition as an ECS service and ensure it's running successfully.

#### 2. Single-Container Deployment (Type: EC2 / EC2 Spot)
- Create an ECS Cluster
- Create Launch Template & ASG Manually
- Use ASG as an capacity Provider
- FE Application(from previous assignment) (Bridge Mode: Should get a Public IP)
- Deploy the task definition as a single task and ensure it's running successfully.

#### 3. Using Terraform 
### Multi-Container Deployment (Type: EC2/EC2 Spot) (Bridge) (1 frontend, 1 backend)
- Create a ECS Cluster
- Create a Task Definition with multiple-container
- Create an ECS Service:
   - Deploy the task definition as an ECS service and ensure it's running successfully browsing it by its public IP
   - Use ASG On-Demand/Spot as capacity provider

#### 4. What are the placement strategies in the AWS ECS? Explain briefly. At last compare which strategy should be used in which scenario.

### Bonus:
- Configure/Update the ECS Service of Q.3 so that you will be able to execute commands inside both ECS container separately.
   - e.g. aws ecs execute-command………………………………………………………………………………………..

