<H1>☁️ Automated AWS Café Infrastructure with CloudFormation and CodePipeline</H1>

This project demonstrates how to **automate and replicate the café's AWS infrastructure** using **CloudFormation, CodeCommit, and CodePipeline** to ensure consistency, scalability, and global readiness as the café expands to new countries.

---

<h2>🚀 Project Overview</h2>

The café team previously used manual AWS Management Console setups for deploying their application. However, with planned international expansion and the need for consistent **Dev and Prod environments**, this project shifts to **Infrastructure as Code (IaC)** and **CI/CD automation**.

Using **AWS CloudFormation**, **AWS CodeCommit**, and **AWS CodePipeline**, we:
- Automate VPC and application deployments
- Maintain configurations in version control
- Automatically replicate environments across AWS Regions

---

<h2>🛠️ Technologies Used</h2>

- **AWS CloudFormation** (IaC)
- **AWS CodeCommit** (version control)
- **AWS CodePipeline** (CI/CD automation)
- **AWS CLI**
- **Git**

---

<h2>⚙️ Deployment Steps</h2>

---

1️⃣ Write CloudFormation Templates
- **`vpc-template.yaml`**:
  - VPC with CIDR block (e.g., `10.0.0.0/16`)
  - Public and private subnets across multiple AZs
  - Internet Gateway, route tables
- **`app-template.yaml`**:
  - EC2 instances with user data bootstrap scripts
  - Security groups
  - (Optional) ALB + Auto Scaling configuration

---

### 2️⃣ Validate Templates
``bash
aws cloudformation validate-template --template-body file://vpc-template.yaml
aws cloudformation validate-template --template-body file://app-template.yaml

3️⃣ Deploy Stacks Manually for Testing
bash
aws cloudformation create-stack --stack-name cafe-vpc-stack --template-body file://vpc-template.yaml --region <region>
aws cloudformation create-stack --stack-name cafe-app-stack --template-body file://ap

4️⃣ Push to AWS CodeCommit
Create a CodeCommit repository (cafe-infra-repo).

Initialize Git locally:

bash
git init
git remote add origin <CodeCommit-HTTPS-URL>
Push:

bash
git add .
git commit -m "Initial commit with CloudFormation templates"
git push -u origin main

5️⃣ Set Up CodePipeline
- Source: CodeCommit (main branch)
- Build: (optional validation with CodeBuild)
- Deploy: AWS CloudFormation to create/update stacks automatically.
- ✅ Each push to main will update your AWS stacks automatically.

6️⃣ Replicate to Another AWS Region
Change CLI region:

bash
aws configure set region <new-region>
Re-run stack creation commands in the new Region or create a new CodePipeline in the new Region for full automation.

✅ Outcomes
- Fully automated AWS infrastructure deployment
- Easily replicable across Regions for café expansion
- Consistent Dev and Prod environments
- All configurations are version-controlled and trackable
- Automatic deployments and updates on Git push

👨‍💻 Author
Project by: Covenant Urch
Email: covenanturch@gmail.com
