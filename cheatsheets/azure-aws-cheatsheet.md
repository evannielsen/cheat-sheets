---
layout: default
title: Azure to AWS Resource Mapping
---

<div class="coversheet">
  <h1><span class="icon">&#x1F4D6;</span> Azure to AWS Resource Mapping</h1>
  <p>A comprehensive guide to understanding equivalent cloud resources between Microsoft Azure and Amazon Web Services</p>
</div>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4E6;</span> <span class="accent-blue">Compute Resources</span></h3>
    <ul>
      <li><strong>Azure Virtual Machines</strong> ↔ <strong>AWS EC2 Instances</strong></li>
      <li><strong>Azure Virtual Machine Scale Sets</strong> ↔ <strong>AWS Auto Scaling Groups</strong></li>
      <li><strong>Azure Container Instances</strong> ↔ <strong>AWS Fargate</strong></li>
      <li><strong>Azure Functions</strong> ↔ <strong>AWS Lambda</strong></li>
      <li><strong>Azure Batch</strong> ↔ <strong>AWS Batch</strong></li>
      <li><strong>Azure App Service</strong> ↔ <strong>AWS Elastic Beanstalk</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4CA;</span> <span class="accent-green">Storage Services</span></h3>
    <ul>
      <li><strong>Azure Blob Storage</strong> ↔ <strong>AWS S3</strong></li>
      <li><strong>Azure Files</strong> ↔ <strong>AWS EFS</strong></li>
      <li><strong>Azure Disk Storage</strong> ↔ <strong>AWS EBS</strong></li>
      <li><strong>Azure Table Storage</strong> ↔ <strong>AWS DynamoDB</strong></li>
      <li><strong>Azure Queue Storage</strong> ↔ <strong>AWS SQS</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F50D;</span> <span class="accent-purple">Networking</span></h3>
    <ul>
      <li><strong>Azure Virtual Network</strong> ↔ <strong>AWS VPC</strong></li>
      <li><strong>Azure Subnet</strong> ↔ <strong>AWS Subnet</strong></li>
      <li><strong>Azure Load Balancer</strong> ↔ <strong>AWS ELB</strong></li>
      <li><strong>Azure Application Gateway</strong> ↔ <strong>AWS Application Load Balancer</strong></li>
      <li><strong>Azure DNS</strong> ↔ <strong>AWS Route 53</strong></li>
      <li><strong>Azure CDN</strong> ↔ <strong>AWS CloudFront</strong></li>
      <li><strong>Azure ExpressRoute</strong> ↔ <strong>AWS Direct Connect</strong></li>
      <li><strong>Azure Virtual WAN</strong> ↔ <strong>AWS Transit Gateway</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E5;</span> <span class="accent-orange">Databases</span></h3>
    <ul>
      <li><strong>Azure SQL Database</strong> ↔ <strong>AWS RDS (PostgreSQL/MySQL)</strong></li>
      <li><strong>Azure Cosmos DB</strong> ↔ <strong>AWS DynamoDB</strong></li>
      <li><strong>Azure Redis Cache</strong> ↔ <strong>AWS ElastiCache (Redis)</strong></li>
      <li><strong>Azure Database for MySQL/PostgreSQL</strong> ↔ <strong>AWS RDS (MySQL/PostgreSQL)</strong></li>
      <li><strong>Azure PostgreSQL Server</strong> ↔ <strong>AWS RDS (PostgreSQL)</strong></li>
      <li><strong>Azure MariaDB</strong> ↔ <strong>AWS RDS (MariaDB)</strong></li>
    </ul>
  </div>
</div>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4DC;</span> <span class="accent-blue">Identity & Security</span></h3>
    <ul>
      <li><strong>Azure Active Directory</strong> ↔ <strong>AWS IAM</strong></li>
      <li><strong>Azure Key Vault</strong> ↔ <strong>AWS Secrets Manager</strong></li>
      <li><strong>Azure AD B2C</strong> ↔ <strong>AWS Cognito (User Pools)</strong></li>
      <li><strong>Azure Security Center</strong> ↔ <strong>AWS Inspector</strong></li>
      <li><strong>Azure Sentinel</strong> ↔ <strong>AWS GuardDuty + CloudTrail</strong></li>
      <li><strong>Azure Dedicated HSM</strong> ↔ <strong>AWS CloudHSM</strong></li>
      <li><strong>Azure Web Application Firewall (WAF)</strong> ↔ <strong>AWS WAF</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4C8;</span> <span class="accent-green">Monitoring & Management</span></h3>
    <ul>
      <li><strong>Azure Monitor</strong> ↔ <strong>AWS CloudWatch</strong></li>
      <li><strong>Azure Log Analytics</strong> ↔ <strong>AWS CloudWatch Logs</strong></li>
      <li><strong>Azure Automation</strong> ↔ <strong>AWS Systems Manager</strong></li>
      <li><strong>Azure Advisor</strong> ↔ <strong>AWS Trusted Advisor</strong></li>
      <li><strong>Azure Application Insights</strong> ↔ <strong>AWS X-Ray + CloudWatch Logs</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F501;</span> <span class="accent-purple">Containers & Orchestration</span></h3>
    <ul>
      <li><strong>Azure Kubernetes Service (AKS)</strong> ↔ <strong>AWS EKS</strong></li>
      <li><strong>Azure Container Registry</strong> ↔ <strong>AWS ECR</strong></li>
      <li><strong>Azure App Service</strong> ↔ <strong>AWS Elastic Beanstalk</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F500;</span> <span class="accent-orange">AI & Machine Learning</span></h3>
    <ul>
      <li><strong>Azure Cognitive Services</strong> ↔ <strong>AWS AI/ML Services</strong></li>
      <li><strong>Azure Machine Learning</strong> ↔ <strong>AWS SageMaker</strong></li>
      <li><strong>Azure Bot Service</strong> ↔ <strong>AWS Lex</strong></li>
      <li><strong>Azure Translator Text</strong> ↔ <strong>AWS Translate</strong></li>
      <li><strong>Azure Computer Vision</strong> ↔ <strong>AWS Rekognition</strong></li>
      <li><strong>Azure Speech Services</strong> ↔ <strong>AWS Transcribe + Polly</strong></li>
    </ul>
  </div>
</div>

<div class="card-grid" style="margin-bottom: 1rem;">
  <div class="card-item">
    <div class="note"><strong>Tip:</strong> Both platforms offer similar concepts but with different naming conventions and UI layouts.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Best Practice:</strong> When migrating between clouds, identify equivalent services and understand their feature differences.</div>
  </div>
  <div class="card-item">
    <div class="note"><strong>Key Difference:</strong> Azure typically offers more managed services compared to AWS which provides more building blocks.</div>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4D8;</span> Detailed Mapping Guide</h2>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F680;</span> Virtual Machines</h3>
    <p><strong>Azure:</strong> Azure Virtual Machines (VMs) provide scalable, secure cloud computing resources.</p>
    <p><strong>AWS:</strong> EC2 instances are virtual servers in the AWS cloud with different instance types and configurations.</p>
    <p><strong>Key Similarities:</strong></p>
    <ul>
      <li>Both support multiple operating systems</li>
      <li>Offer similar pricing models (on-demand, reserved, spot)</li>
      <li>Support virtual networking and security groups</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E2;</span> Storage Solutions</h3>
    <p><strong>Azure:</strong> Blob storage for unstructured data, file shares for file-level access, and disk storage for block-level storage.</p>
    <p><strong>AWS:</strong> S3 for object storage, EFS for file storage, and EBS for block storage.</p>
    <p><strong>Key Similarities:</strong></p>
    <ul>
      <li>Both provide scalable, durable storage solutions</li>
      <li>Support data replication across regions</li>
      <li>Offer similar access controls and encryption options</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F512;</span> Networking</h3>
    <p><strong>Azure:</strong> Virtual Networks, Subnets, Load Balancers, Application Gateways, DNS, CDN, ExpressRoute, Virtual WAN.</p>
    <p><strong>AWS:</strong> VPCs, Subnets, ELBs, Application Load Balancers, Route 53, CloudFront, Direct Connect, Transit Gateway.</p>
    <p><strong>Key Similarities:</strong></p>
    <ul>
      <li>Both provide virtual networking capabilities</li>
      <li>Support private/public IP addressing</li>
      <li>Offer similar routing and security features</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4A5;</span> Databases</h3>
    <p><strong>Azure:</strong> SQL Database, Cosmos DB, Redis Cache, and managed MySQL/PostgreSQL instances.</p>
    <p><strong>AWS:</strong> RDS (for relational), DynamoDB (NoSQL), ElastiCache (Redis), and managed database services.</p>
    <p><strong>Key Similarities:</strong></p>
    <ul>
      <li>Both offer managed database services</li>
      <li>Support backup, restore, and monitoring</li>
      <li>Provide scaling options and high availability</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4C3;</span> Monitoring & Logging</h3>
    <p><strong>Azure:</strong> Monitor for metrics and logs, Log Analytics for query capabilities.</p>
    <p><strong>AWS:</strong> CloudWatch for monitoring and logging, CloudTrail for audit trails.</p>
    <p><strong>Key Similarities:</strong></p>
    <ul>
      <li>Both provide real-time monitoring capabilities</li>
      <li>Support custom metrics and alarms</li>
      <li>Offer integration with alerting systems</li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F50E;</span> Container Services</h3>
    <p><strong>Azure:</strong> AKS for Kubernetes orchestration, Container Registry for image storage.</p>
    <p><strong>AWS:</strong> EKS for Kubernetes orchestration, ECR for container registry.</p>
    <p><strong>Key Similarities:</strong></p>
    <ul>
      <li>Both support container orchestration</li>
      <li>Provide managed service offerings</li>
      <li>Support CI/CD integration</li>
    </ul>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4AC;</span> Migration Considerations</h2>

<div style="background: #0d1117; padding: 1rem; border-radius: 6px; margin-bottom: 1rem;">
<pre><code>Migration Steps:
1. Identify equivalent services in AWS
2. Analyze feature parity and differences
3. Plan data migration strategy
4. Test applications in new environment
5. Switch production traffic gradually

Key Differences to Consider:
- Pricing models (reserved vs spot instances)
- Regional availability
- Feature sets and maturity levels
- Integration capabilities with existing tools</code></pre>
</div>

<div class="card-grid">
  <div class="card-item">
    <p><strong>Cost Management:</strong> Azure offers more integrated cost management, while AWS provides detailed cost allocation tags.</p>
  </div>
  <div class="card-item">
    <p><strong>Security:</strong> Both platforms support similar security frameworks but with different implementation approaches.</p>
  </div>
  <div class="card-item">
    <p><strong>Compliance:</strong> Each platform has specific compliance certifications that may impact your choice.</p>
  </div>
  <div class="card-item">
    <p><strong>Tooling:</strong> Azure CLI and PowerShell, AWS CLI and SDKs - different tooling ecosystems but similar functionality.</p>
  </div>
</div>

<h2 class="section-heading"><span class="icon">&#x1F4AC;</span> Additional Services</h2>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4D8;</span> DevOps & Development Tools</h3>
    <ul>
      <li><strong>Azure DevOps</strong> ↔ <strong>AWS CodePipeline / CodeBuild / CodeDeploy</strong></li>
      <li><strong>Azure Repos</strong> ↔ <strong>AWS CodeCommit</strong></li>
      <li><strong>Azure Artifacts</strong> ↔ <strong>AWS CodeArtifact</strong></li>
      <li><strong>Azure API Management</strong> ↔ <strong>AWS API Gateway</strong></li>
      <li><strong>Azure Logic Apps</strong> ↔ <strong>AWS Step Functions</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E5;</span> Migration Services</h3>
    <ul>
      <li><strong>Azure Migrate</strong> ↔ <strong>AWS Application Discovery Service + Migration Hub</strong></li>
    </ul>
  </div>
</div>

<div class="card-grid">
  <div class="card-item">
    <h3><span class="icon">&#x1F4E5;</span> IoT Services</h3>
    <ul>
      <li><strong>Azure IoT Hub</strong> ↔ <strong>AWS IoT Core</strong></li>
      <li><strong>Azure IoT Central</strong> ↔ <strong>AWS IoT Greengrass</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E5;</span> Hybrid & On-Premises</h3>
    <ul>
      <li><strong>Azure Arc</strong> ↔ <strong>AWS Outposts</strong></li>
      <li><strong>Azure Stack</strong> ↔ <strong>AWS Outposts</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E5;</span> Analytics & Big Data</h3>
    <ul>
      <li><strong>Azure Data Factory</strong> ↔ <strong>AWS Glue</strong></li>
      <li><strong>Azure HDInsight</strong> ↔ <strong>AWS EMR</strong></li>
      <li><strong>Azure Databricks</strong> ↔ <strong>AWS SageMaker (for ML) or EMR (for big data)</strong></li>
      <li><strong>Azure Data Lake Storage</strong> ↔ <strong>AWS S3 with EMR/Redshift</strong></li>
    </ul>
  </div>

  <div class="card-item">
    <h3><span class="icon">&#x1F4E5;</span> Event Processing</h3>
    <ul>
      <li><strong>Azure Event Grid</strong> ↔ <strong>AWS EventBridge</strong></li>
      <li><strong>Azure Event Hubs</strong> ↔ <strong>AWS Kinesis</strong></li>
      <li><strong>Azure Service Bus</strong> ↔ <strong>AWS SQS/SNS</strong></li>
    </ul>
  </div>
</div>

<p class="credits">Made with <span style="color: var(--accent-pink);">&#x2764;</span> for cloud developers &mdash; keep building! &#x1F680;</p>