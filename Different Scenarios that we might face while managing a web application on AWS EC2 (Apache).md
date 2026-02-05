# **Different Scenarios that we might face while managing a web application on AWS EC2 (Apache)**

---

## **1\. Website Not Accessible**

### **Issue:**

The web application is not loading in the browser.

### **Symptoms:**

Users see a “Site can’t be reached” message or experience a connection timeout.

### **Root Cause:**

The EC2 instance may be stopped, the Apache service may be down, or the public IP address may have changed after a restart.

### **Fix:**

Start the EC2 instance, restart the Apache service, and use an Elastic IP to maintain a stable public address.

---

## **2\. Apache Service Stopped**

### **Issue:**

The EC2 instance is running, but the application is not accessible.

### **Symptoms:**

Port 80 does not respond, even though the server is up.

### **Root Cause:**

Apache may have stopped due to configuration errors, system updates, or resource issues.

### **Fix:**

Restart the Apache service and review Apache logs to identify and resolve the issue.

---

## **3\. Apache Running but Port 80 Blocked by UFW**

### **Issue:**

Apache service is active but the website does not load.

### **Symptoms:**

`systemctl status apache2` shows running, but the site is inaccessible.

### **Root Cause:**

UFW is active but HTTP or Apache port 80 is not allowed.

### **Fix:**

Allow Apache port 80 through UFW.

## 

---

## **4\. Disk Space Exhausted**

### **Issue:**

The web application stops responding unexpectedly.

### **Symptoms:**

Apache fails to start and file operations fail on the server.

### **Root Cause:**

Log files grow continuously or the root volume size is insufficient.

### **Fix:**

Clean old log files or extend the EBS volume to increase disk space.

---

## **5\. Security Group Blocking HTTP Traffic**

### **Issue:**

The website is unreachable from the internet.

### **Symptoms:**

Apache is running, but the site does not load externally.

### **Root Cause:**

Port 80 is not allowed in the EC2 security group or the source IP is incorrect.

### **Fix:**

Update the security group to allow inbound HTTP traffic on port 80 from all required sources.

---

## **6\. Application Changes Not Visible**

### **Issue:**

Recent updates to the web application do not appear in the browser.

### **Symptoms:**

The old version of the page continues to display.

### **Root Cause:**

Browser caching or files not placed in the Apache document root directory.

### **Fix:**

Clear the browser cache and verify that files are deployed in `/var/www/html`.

---

## **7\. EC2 Instance Restarted Automatically**

### **Issue:**

The application experiences unexpected downtime.

### **Symptoms:**

The website goes down and the public IP address changes.

### **Root Cause:**

System maintenance, instance failure, or manual reboot.

### **Fix:**

Assign an Elastic IP and enable CloudWatch alarms to monitor instance health.

---

## **8\. Website Not Reachable Due to Network Issue**

### **Issue:**

The web application is not reachable from the internet.

### **Symptoms:**

The browser shows a connection timeout even though the EC2 instance is running.

### **Root Cause:**

The instance is placed in a private subnet or does not have a public IP assigned.

### **Fix:**

Ensure the instance is in a public subnet and has a public or Elastic IP associated.

---

## **9\. Internet Gateway Not Attached**

### **Issue:**

The EC2 instance cannot communicate with the internet.

### **Symptoms:**

Outbound traffic fails and the website is inaccessible externally.

### **Root Cause:**

The VPC does not have an Internet Gateway attached or the route table is not configured correctly.

### **Fix:**

Attach an Internet Gateway to the VPC and add a route to `0.0.0.0/0` in the route table.

---

## **10\. Route Table Misconfiguration**

### **Issue:**

Network traffic does not reach the EC2 instance.

### **Symptoms:**

Inbound and outbound connections fail despite correct security group rules.

### **Root Cause:**

The subnet route table does not have a valid route to the Internet Gateway.

### **Fix:**

Update the route table to route internet traffic through the Internet Gateway.

---

## **11\. Security Group Allows Traffic but Network ACL Blocks It**

### **Issue:**

The website is still unreachable even though security group rules are correct.

### **Symptoms:**

HTTP traffic fails intermittently or completely.

### **Root Cause:**

Network ACL rules are blocking inbound or outbound traffic on required ports.

### **Fix:**

Allow inbound and outbound traffic on ports 80, 443, and 22 in the Network ACL.

---

## **12\. Incorrect Port Access Over Network**

### **Issue:**

The application is partially accessible.

### **Symptoms:**

HTTP works but HTTPS or SSH fails.

### **Root Cause:**

Required ports are not allowed at one or more network layers.

### **Fix:**

Ensure ports are allowed in Security Groups, Network ACLs, and UFW consistently.

---

## **13\. Public IP Changed After Restart**

### **Issue:**

Users cannot access the website after instance reboot.

### **Symptoms:**

Old IP address no longer works.

### **Root Cause:**

Public IP addresses change when an EC2 instance is stopped and started.

### **Fix:**

Assign an Elastic IP to the instance for a fixed network address.

---

**Conclusion**

Even a basic EC2 and Apache web application can face multiple operational issues in real-world scenarios. Understanding the issue, identifying symptoms, finding the root cause, and applying the correct fix are essential skills for anyone starting in DevOps or cloud engineering.

