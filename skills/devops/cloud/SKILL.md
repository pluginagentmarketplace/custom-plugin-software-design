---
name: cloud-platforms
description: Cloud platforms including AWS, GCP, and Azure. Master cloud services, serverless, containers, and cloud architecture.
---

# Cloud Platforms & DevOps

## Quick Start

Cloud platforms provide on-demand computing resources:

### AWS Example
```bash
# EC2 Instance
aws ec2 run-instances --image-id ami-12345 --count 1 --instance-type t3.micro

# S3 Storage
aws s3 cp myfile.txt s3://my-bucket/

# Lambda Function
aws lambda create-function --function-name myFunc --runtime python3.9 --handler index.handler
```

### Docker Containerization
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

### Kubernetes Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: myapp:1.0
        ports:
        - containerPort: 3000
```

## Cloud Services

**AWS**
- **Compute** - EC2, Lambda, ECS, EKS
- **Storage** - S3, EBS, EFS
- **Databases** - RDS, DynamoDB, Elasticache
- **Networking** - VPC, CloudFront, Route 53

**GCP**
- **Compute** - Cloud Run, Cloud Functions, GKE
- **Storage** - Cloud Storage, Firestore
- **Analytics** - BigQuery, Dataflow
- **AI/ML** - Vertex AI, Vision API

**Azure**
- **Compute** - Virtual Machines, App Service, Functions
- **Storage** - Blob Storage, Cosmos DB
- **Analytics** - Synapse Analytics, Data Factory

## Best Practices

- Use Infrastructure as Code (Terraform)
- Implement proper security (IAM, encryption)
- Monitor and log everything
- Plan for high availability
- Optimize costs regularly
- Backup critical data
- Use CI/CD pipelines
- Document infrastructure

## Resources

- [AWS Documentation](https://docs.aws.amazon.com)
- [Google Cloud Docs](https://cloud.google.com/docs)
- [Azure Documentation](https://docs.microsoft.com/azure)
- [Docker Docs](https://docs.docker.com)
- [Kubernetes Docs](https://kubernetes.io/docs)
