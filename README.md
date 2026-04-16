🚀 S3 Static Site CI/CD Pipeline

This project demonstrates how to build a CI/CD pipeline using GitHub Actions to automatically deploy a static website to AWS S3. Whenever code is pushed, the pipeline runs, sets up the environment, and uploads the files to S3, ensuring continuous deployment.

📌 Features
⚡ Automated deployment using GitHub Actions
🪣 Static website hosting on AWS S3
🔐 Secure AWS authentication using IAM credentials or OIDC
🔄 Continuous deployment on every push to main
🌍 Optional CloudFront integration for CDN caching
🧹 Easy cache invalidation support (if CloudFront is used)
🏗️ Architecture
GitHub Repository
        ↓
GitHub Actions (CI/CD Pipeline)
        ↓
Build static files (HTML/CSS/JS)
        ↓
Upload to AWS S3 bucket
        ↓
(Optional) CloudFront distribution
        ↓
Live Website
⚙️ Prerequisites

Before using this project, ensure you have:

AWS Account
S3 bucket configured for static website hosting
IAM user/role with S3 permissions
GitHub repository secrets configured
🔐 Required GitHub Secrets

Add the following in GitHub → Settings → Secrets and variables → Actions:

AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_REGION
S3_BUCKET_NAME
🚀 Deployment Workflow

The CI/CD pipeline is defined in:

.github/workflows/deploy.yml
Example Workflow Steps:
Checkout repository
Install dependencies (if any)
Build static site
Sync files to S3 bucket
📦 Example GitHub Actions Workflow
name: Deploy to S3

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: ${{ secrets.AWS_REGION }}

      - name: Sync files to S3
        run: |
          aws s3 sync . s3://${{ secrets.S3_BUCKET_NAME }} --delete
🌐 Static Website Hosting (S3 Setup)

Enable static hosting on your S3 bucket:

Index document: index.html
Error document: error.html (optional)
Make bucket publicly accessible or serve via CloudFront
🔄 Optional: CloudFront Setup

To improve performance and caching:

Create a CloudFront distribution
Set S3 bucket as origin
Enable HTTPS using ACM certificate
Add cache invalidation step in CI/CD
🧪 Local Development

If your project is a simple static site:

# Open locally
open index.html

If using a framework:

npm install
npm run build
📈 Benefits
No servers required
Fully automated deployments
Fast global content delivery
Cost-efficient hosting on AWS S3
🛠️ Tech Stack
AWS S3
GitHub Actions
AWS CLI
(Optional) CloudFront
HTML / CSS / JavaScript or any static framework
📌 License

This project is licensed under the MIT License.
