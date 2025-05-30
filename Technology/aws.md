Constraints and Environment Standards: 
1. IPv4 addresses are rare and constrained. Prefer IPv6 addresses whenever possible.
2. All subnets shall be private except when approved by a security team. Load balancers may be public facing.
3. Data must be encrypted at rest and in transit. If encryption at rest is not specified, default to a customer managed key of the highest length possible.
4. Security groups must be limited to the minimum open ports. Https is allowed for web services and port 80 should redirect to port 443.
5. When possible, default to serverless infrastructure such as ECS Fargate or Aurora Postgres Serverless.
6. Our default region is US-East-2, Ohio. Always generate infrastructure in this region unless specifically instructed otherwise.
7. We default to using three availability zones or AZs per VPC.
8. VPCs will default to no more than a /25 worth of IPv4 addresses. Public and private subnets in AZs will default to a /28 or 14 IPs. Perfer IPv6 addresses by default.
9. Mandatory tagging for all resources (e.g., owner, environment, cost center) to aid cost tracking and governance.
10. All accounts should have an S3 bucket for logging. The name of the s3 bucket should be a sudo-random 12 character string, followed by a dash, then the application name. Versioning and encryption should be enabled.
11. Centralized logging and monitoring using CloudWatch Logs and CloudTrail; store logs in the dedicated S3 bucket.
12. Least‑privilege IAM policies for all users, roles, and services, and require MFA for human users.
13. Automated backup and recovery plans for persistent data stores, including periodic snapshots and lifecycle policies.
14. Use of AWS Config or other compliance tooling to enforce standards (private subnets, encryption, etc.).
15. Web Application Firewall (WAF) in front of public load balancers to help mitigate common web threats.
16. Standardized infrastructure as code (CloudFormation/Terraform) with code review requirements.
