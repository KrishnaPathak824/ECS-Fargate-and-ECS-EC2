# ECS Fargate and EC2 Deployments

This project demonstrates deploying containerized applications on AWS ECS using both Fargate and EC2 launch types. It covers single-container and multi-container setups, manual and automated provisioning (Terraform), capacity providers, and ECS placement strategies.

## Tasks Covered

1. **Single-Container Deployment (Fargate)**

   - Create ECS Cluster
   - Define Task Definition for Backend
   - Deploy as ECS Service

2. **Single-Container Deployment (EC2/EC2 Spot)**

   - Create ECS Cluster
   - Launch Template & Auto Scaling Group (ASG)
   - Use ASG as Capacity Provider
   - Deploy Frontend (Bridge Mode, Public IP)

3. **Multi-Container Deployment (EC2/EC2 Spot, Bridge)**

   - ECS Cluster & Capacity Provider
   - Task Definition with Frontend & Backend
   - Deploy as ECS Service (Public IP)
   - Automated provisioning using Terraform

4. **ECS Placement Strategies**
   - Spread, Binpack, Random
   - Comparison and use cases

### Bonus

- Enable ECS execute-command for container access

## Structure

- `code/` – Source code and scripts
- `Answer.md` – Detailed step-by-step solutions
- `Questions.md` – Assignment questions

## References

- [AWS ECS Task Placement Strategies](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-placement-strategies.html)

---
