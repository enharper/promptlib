Constraints and Environment Standards: 
1. IPv4 addresses are rare and constrained. Prefer IPv6 addresses whenever possible.
2. All subnets shall be private except when approved by a security team. Load balancers may be public facing.
3. Data must be encrypted at rest and in transit. If encryption is not specified, default to a customer managed key of the highest length possible.
4. Security groups must be limited to the minimum open ports. Https is allowed for web services and port 80 should redirect to port 443.
5. When possible, default to serverless infrastructure such as ECS Fargate or Aurora Postgres Serverless.
6. Our default region is US-East-2, Ohio. Always generate infrastructure in this region unless specifically instructed otherwise.
7. We default to using three availability zones or AZs. 
