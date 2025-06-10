# 🛠️ AWS CloudFormation Template – Multi-AZ VPC with Public & Private Subnets

This CloudFormation template provisions a production-ready **VPC** with the following features:

- 2 **Availability Zones**
- 2 **Public Subnets** (1 per AZ)
- 2 **Private Subnets** (1 per AZ)
- **NAT Gateway** (in AZ1) for secure internet access from private subnets
- **Internet Gateway** for public subnets
- Route tables and subnet associations

---

## 📌 Prerequisites

- AWS CLI configured
- IAM permissions to create networking resources
- [CloudFormation Stack Limits](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/cloudformation-limits.html)

---

## 🚀 Deploy via AWS CLI

```bash
aws cloudformation deploy \
  --template-file template.yaml \
  --stack-name MyVpcStack \
  --capabilities CAPABILITY_NAMED_IAM
```

---

## 💡 Notes

- The template uses hardcoded CIDR blocks. You can fork it and parameterize the CIDRs as needed.
- The NAT Gateway is deployed in **AZ1** only, which simplifies routing and reduces cost.
- Public subnets are configured with `MapPublicIpOnLaunch: true`, so instances launched there automatically receive public IPs.

---

## 🔐 Security Considerations

- This template does **not** create any EC2 instances or security groups. If you add them later, follow the **principle of least privilege**.
- Public subnets allow internet-bound traffic via the **Internet Gateway**—use **Security Groups** and **NACLs** to control exposure.
- Private subnets use a **NAT Gateway** for outbound-only internet access, protecting them from inbound connections.
- **VPC Flow Logs** are not enabled—consider enabling them for improved visibility and auditing.

---

## 💰 Cost Optimization Tips

- **NAT Gateways** incur hourly and data transfer charges.
- For low-cost, low-throughput environments, consider using **NAT Instances** instead.
- Reduce NAT usage by using **VPC Interface Endpoints** for AWS services like **S3** and **DynamoDB**.
- Monitor traffic and charges using **AWS Cost Explorer**, and set up **Budgets** or **Billing Alarms**.

---

## 🧩 Extend This Template

Ideas for customization and expansion:

- Parameterize **AZs** and **CIDR ranges**
- Add **EC2 Auto Scaling Groups**, **ALB**, or **RDS** clusters
- Enable **VPC Flow Logs** for security auditing
- Add **private DNS** and **Route 53 Resolver Endpoints**
- Create **Security Groups**, **NACLs**, or **VPC Endpoints**

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙋 Author

**Built by Ashhad Ali, DevOps Engineer**

- 📩 [Connect on LinkedIn](https://linkedin.com/in/ashhadali1)
- 🌐 [Visit ashhadali.com](https://ashhadali.com)

---

## 🤝 Contributing

Feel free to **fork** this repository, **open issues**, or **submit pull requests** for improvements.
