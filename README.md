# AWS-setup

---

# AWS EC2 Setup Guide - Ubuntu AMI

This guide will walk you through signing up for AWS, launching an EC2 instance, connecting to it via SSH using a PEM file, and installing essential tools like Java, pip, and Jenkins on an Ubuntu-based EC2 instance.

## Prerequisites

- AWS Account (Sign up at [AWS](https://aws.amazon.com/))
- PEM file to connect via SSH to EC2
- Windows/Mac terminal for connecting to EC2
- Basic knowledge of Linux commands

## Table of Contents

1. [Sign Up for AWS](#sign-up-for-aws)
2. [Launch EC2 Instance](#launch-ec2-instance)
3. [Connect to EC2 via SSH](#connect-to-ec2-via-ssh)
4. [Install Java, pip, and Jenkins](#install-java-pip-and-jenkins)

---

### Sign Up for AWS

1. **Create an AWS Account**:
   - Go to [AWS Sign Up](https://aws.amazon.com/) and create a new account.
   - Follow the steps for entering personal details and payment information.
   - Once done, you'll have access to the AWS Management Console.

2. **Log in to AWS Console**:
   - Go to [AWS Console Login](https://aws.amazon.com/console/).
   - Enter your credentials and log in.

---

### Launch EC2 Instance

1. **Navigate to EC2 Dashboard**:
   - After logging in, search for **EC2** in the search bar and click on "EC2" under Services.

2. **Launch Instance**:
   - Click on **Launch Instance** to start the creation of your EC2 instance.
   - Select the **Ubuntu** AMI (Amazon Machine Image).
   - Choose an instance type, for example, **t2.micro** (eligible for the free tier).
   - Configure your instance (for most users, default settings should work fine).
   - Add storage if needed.
   - In the **Configure Security Group**, ensure you allow **SSH (port 22)** so you can connect to the instance via terminal.

3. **Generate a Key Pair**:
   - Under **Key Pair**, select **Create a new key pair**.
   - Give your key pair a name (e.g., `my-aws-key`).
   - Download the `.pem` file. This file will allow you to securely connect to the EC2 instance via SSH.
   - **Important:** Store the `.pem` file securely, as it will not be available for download after the creation process.

4. **Launch the Instance**:
   - After selecting the key pair, click **Launch**.
   - Your EC2 instance will now be up and running.

---

### Connect to EC2 via SSH

#### Windows (Using Git Bash or Windows Terminal)

1. **Change Permissions for PEM File**:
   - Open **Git Bash** or **Windows Terminal**.
   - Navigate to the directory where your `.pem` file is located:
     ```bash
     cd path/to/your/pem/file
     ```

   - Run the following command to change the permissions of the PEM file (this ensures the file is only readable by you):
     ```bash
     chmod 400 my-aws-key.pem
     ```

2. **SSH into EC2**:
   - Find the **Public IP Address** of your EC2 instance in the EC2 dashboard.
   - Run the following command to connect via SSH:
     ```bash
     ssh -i "my-aws-key.pem" ubuntu@<EC2_PUBLIC_IP>
     ```

   - You will be logged into the EC2 instance.

#### MacOS (Terminal)

1. **Change Permissions for PEM File**:
   - Open **Terminal**.
   - Navigate to the folder where your `.pem` file is saved:
     ```bash
     cd path/to/your/pem/file
     ```

   - Change the file permissions:
     ```bash
     chmod 400 my-aws-key.pem
     ```

2. **SSH into EC2**:
   - Use the Public IP of your EC2 instance to connect:
     ```bash
     ssh -i "my-aws-key.pem" ubuntu@<EC2_PUBLIC_IP>
     ```

   - You will be connected to the EC2 instance.

---

### Install Java, pip, and Jenkins on EC2 (Ubuntu)

Once you have connected to your EC2 instance, follow these steps to install Java, pip, and Jenkins:

#### 1. **Update Package Lists**
```bash
sudo apt update -y
```

#### 2. **Install Java**

- First, update the repository:
  ```bash
  sudo apt install openjdk-11-jdk -y
  ```

- Check if Java is installed:
  ```bash
  java -version
  ```

#### 3. **Install pip**

- Install pip for Python 3:
  ```bash
  sudo apt install python3-pip -y
  ```

- Verify installation:
  ```bash
  pip3 --version
  ```

#### 4. **Install Jenkins**

- Add Jenkins repository and key:
  ```bash
  wget -q -O - https://pkg.jenkins.io/keys/jenkins.io.key | sudo apt-key add -
  ```

- Add Jenkins repository to your system:
  ```bash
  sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable/ / > /etc/apt/sources.list.d/jenkins.list'
  ```

- Update apt and install Jenkins:
  ```bash
  sudo apt update -y
  sudo apt install jenkins -y
  ```

- Start Jenkins service:
  ```bash
  sudo systemctl start jenkins
  ```

- Enable Jenkins to start on boot:
  ```bash
  sudo systemctl enable jenkins
  ```

- Check Jenkins status:
  ```bash
  sudo systemctl status jenkins
  ```

- Open Jenkins web interface by navigating to `http://<EC2_PUBLIC_IP>:8080` in your browser.
  - Get the Jenkins unlock key:
    ```bash
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```

---

### Conclusion

You have now successfully signed up for AWS, launched an EC2 Ubuntu instance, connected to it via SSH, and installed Java, pip, and Jenkins. This EC2 instance is now ready for further configuration and use.

For more details on each of the AWS services, refer to the [AWS Documentation](https://docs.aws.amazon.com/).

---

