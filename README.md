# AWS VPC Peering Setup

## Overview
This document provides a detailed explanation of the AWS Virtual Private Cloud (VPC) peering setup illustrated in the provided diagram. The architecture consists of two VPCs, Test-VPC-01 and Test-VPC-02, connected via a peering connection to enable secure communication between resources in both networks.
![vpc drawio](https://github.com/user-attachments/assets/efb3a72c-7bcb-48f7-9e74-009445b51a8a)


## Architecture Components

### 1. **VPCs**
- **Test-VPC-01**: Contains an EC2 instance within a public subnet.
- **Test-VPC-02**: Contains an EC2 instance within a private subnet.
- Both VPCs are configured with CIDR blocks within the 12.0.0.0/16 and 13.0.0.0/16 range.
  <img width="1187" alt="Screenshot 2025-03-28 at 10 46 22" src="https://github.com/user-attachments/assets/91fc7e70-f81d-400d-b33d-168665dbe3d0" />


### 2. **Subnets**
- **Public Subnet (Test-VPC-01)**: Provides public access via an Internet Gateway.
- **Private Subnet (Test-VPC-02)**: Secured from direct internet access.
<img width="1191" alt="Screenshot 2025-03-28 at 10 53 58" src="https://github.com/user-attachments/assets/25ad9e9e-1e52-4b6b-8897-daf95c317f7d" />

### 3. **Internet Gateways**
- Both VPCs have Internet Gateways attached, allowing external communication for public resources.
<img width="1172" alt="Screenshot 2025-03-28 at 10 55 53" src="https://github.com/user-attachments/assets/7c086b7a-d4a1-4ecd-91ae-e1575202502d" />

### 4. **Peering Connection**
- A VPC Peering Connection is established between Test-VPC-01 and Test-VPC-02 to enable inter-VPC communication.
- The peering connection is configured in the route tables of both VPCs.
<img width="246" alt="Screenshot 2025-03-28 at 11 17 40" src="https://github.com/user-attachments/assets/b2d5a2dd-52e2-44f4-88f1-9f9c27d705be" />

### 5. **Routing Table**
- Routes are configured to direct traffic between the VPCs over the peering connection.
- The routing table in each VPC includes entries for the corresponding CIDR blocks of the peered VPC.
<img width="1199" alt="Screenshot 2025-03-28 at 10 47 59" src="https://github.com/user-attachments/assets/43b597c4-baa6-433a-b7a8-b445f7fdd22d" />

### 6. **Security Associations**
- Security groups and network ACLs are configured to allow traffic flow between the peered VPCs.
- Each EC2 instance has appropriate inbound and outbound rules to permit inter-VPC communication.
<img width="1437" alt="Screenshot 2025-03-28 at 11 02 29" src="https://github.com/user-attachments/assets/afd9c38e-6d9f-4c09-b6c1-d59ca57ee582" />

## Network Flow
1. The EC2 instance in Test-VPC-01 can communicate with the EC2 instance in Test-VPC-02 via the peering connection.
2. The Internet Gateway allows external access to public resources.
3. Private resources in Test-VPC-02 remain isolated while still being accessible from Test-VPC-01 through the peering connection.

## Configuration Steps
### **Step 1: Create VPCs**
1. Create two VPCs: Test-VPC-01 and Test-VPC-02.
2. Define CIDR ranges for both VPCs.

### **Step 2: Create Subnets**
1. Create a public subnet in Test-VPC-01.
2. Create a private subnet in Test-VPC-02.

### **Step 3: Attach Internet Gateways**
1. Attach an Internet Gateway to each VPC.
2. Update the route table to allow external communication (only for public subnets).

### **Step 4: Configure Peering Connection**
1. Create a VPC Peering Connection between Test-VPC-01 and Test-VPC-02.
2. Accept the peering request in the AWS Console.
3. Update the routing tables in both VPCs to route traffic via the peering connection.

### **Step 5: Configure Security Groups**
1. Allow inbound and outbound traffic for necessary ports (e.g., SSH, HTTP, etc.).
2. Ensure security groups allow communication between peered VPCs.

### **Step 6: Test Connectivity**
1. SSH into the EC2 instance in Test-VPC-01.
2. Ping or connect to the EC2 instance in Test-VPC-02 to verify peering connection functionality.

## Best Practices
- Use least privilege access when configuring security groups and network ACLs.
- Regularly monitor VPC peering connections and network traffic.
- Enable logging for better visibility and troubleshooting.
- Consider using AWS Transit Gateway for scaling beyond two VPCs.

## Conclusion
This VPC peering setup allows seamless, secure communication between two VPCs while maintaining isolation and controlled access. Proper configuration of routing tables and security groups ensures a functional and secure architecture.

<img width="1067" alt="Screenshot 2025-03-28 at 11 15 54" src="https://github.com/user-attachments/assets/9ad8e98e-77da-42f0-b4c3-fbdc1931e231" />
<img width="1172" alt="Screenshot 2025-03-28 at 11 15 02" src="https://github.com/user-attachments/assets/573f6f82-69b9-4a95-b7e5-15c22141e737" />
<img width="1113" alt="Screenshot 2025-03-28 at 11 10 23" src="https://github.com/user-attachments/assets/67f6fa63-11c0-4122-bed7-c6906a0a79ab" />
<img width="1170" alt="Screenshot 2025-03-28 at 11 09 43" src="https://github.com/user-attachments/assets/22d4f71f-28a9-4002-8ae9-a6f45bb43ca5" />
<img width="723" alt="Screenshot 2025-03-28 at 11 26 50" src="https://github.com/user-attachments/assets/e489c30b-dbdd-4b79-a1f3-06ce58003ea0" />
<img width="710" alt="Screenshot 2025-03-28 at 11 26 43" src="https://github.com/user-attachments/assets/e39ec18a-7160-4ff0-a70a-4f9836126e58" />
<img width="1432" alt="Screenshot 2025-03-28 at 11 25 31" src="https://github.com/user-attachments/assets/28085feb-d6fc-4ca2-a455-f1bcf7d1dc05" />
