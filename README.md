# capstone_apprepo_code

Things that we would need to create: 
1. Images - Already done by Olivia 
2. Workflow that will take the images from ECR and deploy them to EKS (need to do separate workflows for Dev and Prod) 
3. Security (Separate levels of scrutiny for Dev and Prod)

It maybe useful to use Helm for Production environment workflows, so that rollback is more structured, and there is easier release management (setup two different yaml files for ease of deployement)
this is what the current dev and prod workflows are doing 
Dev environment
Developer
     │
git push develop
     │
     ▼
GitHub Actions
     │
     ├── Build Docker image
     ├── Push to ECR
     ├── Connect to Dev EKS cluster
     ├── Update Deployment image
     └── Wait for rollout

Prod environment 
Developer
      │
Merge into main
      │
      ▼
GitHub Actions
      │
      ├── Build image
      ├── Push image to ECR
      ├── Connect to Production EKS
      ├── Helm upgrade
      ├── Kubernetes rolling update
      └── Verify rollout

need to do -1606202: 
the structure for how the push to eks workflow to run only when trying to push to the appropriate branches for dev and prod (fix indentation)
test the respective codes 
