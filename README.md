# High-Availability Web Application Deployment on AWS 🚀

This project demonstrates deploying a **scalable and reliable web application** on **Amazon Web Services (AWS)**. The setup ensures high availability, fault tolerance, and scalability, making it suitable for handling variable traffic while ensuring the application stays online.

---

## **Key Features**

- **Auto Scaling**: Automatically adjusts the number of servers (EC2 instances) based on traffic to maintain performance and cost efficiency.
- **Elastic Load Balancer (ELB)**: Distributes incoming traffic across multiple servers, preventing overloading.
- **RDS (Relational Database Service)**: A managed MySQL database with high availability to ensure reliable data storage.
- **Security**: Configures secure connections between application servers and the database using AWS security settings.
- **Scalable Design**: Seamlessly scales to handle traffic spikes without downtime.

---

## **Technologies Used**

- **AWS EC2**: Virtual servers for hosting the PHP website.
- **AWS RDS**: Managed MySQL database for data storage.
- **AWS Auto Scaling**: Dynamically adjusts the number of EC2 instances based on demand.
- **AWS Elastic Load Balancer**: Ensures even traffic distribution across servers.
- **MySQL**: Database technology for structured data storage.
- **PHP**: Programming language for building the web application.

---

## **Architecture Overview**

```plaintext
User Requests
     |
     v
Elastic Load Balancer
     |
Auto Scaling Group (EC2 Instances)
     |
     v
Amazon RDS (MySQL Database)
```

---

## **Setup Instructions**

### **Step 1: Launch an EC2 Instance**
1. Log in to the AWS Management Console.
2. Navigate to the **EC2 Dashboard** and launch an instance:
   - Select **Amazon Linux 2** or another preferred OS.
   - Configure instance details and choose a **t2.micro** instance type for testing.
3. Install necessary software:
   ```bash
   sudo yum update -y
   sudo yum install -y httpd php php-mysqlnd
   sudo systemctl start httpd
   sudo systemctl enable httpd
   ```
4. Upload your PHP application to the `/var/www/html/` directory.

### **Step 2: Create an RDS Instance**
1. Navigate to the **RDS Dashboard** and create a database:
   - Select **MySQL** and choose a **db.t2.micro** instance type for testing.
   - Enable Multi-AZ deployment for high availability.
2. Note the endpoint, username, and password for the database.
3. Update your PHP application’s database configuration file to use the RDS instance:
   ```php
   $db_host = "<RDS_ENDPOINT>";
   $db_user = "<USERNAME>";
   $db_pass = "<PASSWORD>";
   $db_name = "<DATABASE_NAME>";
   ```

### **Step 3: Configure Security Groups**
1. **EC2 Security Group**:
   - Allow **HTTP (port 80)** and **SSH (port 22)** access from your IP.
2. **RDS Security Group**:
   - Allow MySQL/Aurora traffic (port 3306) from the EC2 security group.

### **Step 4: Set Up Auto Scaling**
1. Create a launch template or configuration for EC2 instances:
   - Include the AMI ID, instance type, and startup script for PHP.
2. Configure an Auto Scaling Group:
   - Set the minimum and maximum number of instances.
   - Attach the Elastic Load Balancer to distribute traffic.

### **Step 5: Configure Elastic Load Balancer**
1. Navigate to the **Load Balancer Dashboard** and create an Application Load Balancer:
   - Add the EC2 instances to the target group.
   - Configure health checks to monitor instance availability.
2. Update the DNS record for your domain to point to the Load Balancer.

---

## **Testing the Setup**
1. Access your web application using the Load Balancer's DNS name.
2. Simulate high traffic to test Auto Scaling:
   - Use tools like **Apache JMeter** or **Locust** to generate traffic.
3. Verify database connectivity and data persistence in RDS.

---

## **Enhancements**
- **HTTPS Support**: Use AWS Certificate Manager to enable SSL/TLS.
- **Monitoring**: Configure CloudWatch alarms for CPU utilization and Auto Scaling events.
- **Backup**: Enable RDS automated backups and snapshots.
- **Content Delivery**: Integrate Amazon CloudFront for faster content delivery.

---

## **License**
This project is licensed under the MIT License. Feel free to use and modify it for your own projects!

---

## **Feedback**
We welcome contributions and feedback! Feel free to open an issue or submit a pull request. If this project helped you, give it a ⭐️ on GitHub!
