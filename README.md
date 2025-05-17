# Ec2-WebApp-Deployment
This repository contains documentation and scripts for deploying a web application on Amazon EC2
Deploying a Web Application on Amazon EC2

Prerequisites
* An AWS account with an EC2 instance running.
* Basic knowledge of Linux commands.
* An SSH client (e.g., Terminal on macOS/Linux, PuTTY on Windows).
* A web application (in my case, a website packaged as a zip file).
* AWS Region and Availability Zone: (Specify the region and AZ)
* Lugx Gaming Website Template (Website or webapp files of your choice) 

Steps
1. Connect to the EC2 Instance via SSH
   * Use the following command in your terminal
	ssh -i /path/to/your/private_key.pem your_ec2_username@your_ec2_public_ip_or_dns

   * Replace the placeholders with your actual private key file path, EC2 username, and public IP address or DNS name.
   * This command establishes a secure connection to your EC2 instance, allowing you to execute commands on the server.

2. Update System Packages
   * Once connected, it's a good practice to update the system's packages to ensure you have the latest security updates and software.

	sudo yum update -y

   * The sudo command is used to execute commands with administrative privileges. The yum command is the package manager for Amazon Linux. The -y flag automatically answers 	"yes" to any prompts.
      
3. Install Apache Web Server
      * Install the Apache web server, which will serve your web application.
	
	sudo yum install -y httpd

4. Start and Enable Apache
      * Start the Apache service:

	sudo systemctl start httpd

 	* Enable Apache to start automatically on boot:

	sudo systemctl enable httpd

5. Upload Web Application Files
      * Use the scp (Secure Copy) command to transfer the web application files (in a zip archive) from your local machine to the EC2 instance.

	scp -i /path/to/your/private_key.pem /path/to/your/local_zip_file.zip your_ec2_username@your_ec2_public_ip_or_dns:/home/ec2-user/temp.zip

      * This command securely copies the zip file to the /home/ec2-user/ directory on the EC2 instance.
               
6. Extract and Deploy Web Application Files
      * Connect to the EC2 instance via SSH.

	ssh -i /path/to/your/private_key.pem your_ec2_username@your_ec2_public_ip_or_dns

      * Extract the uploaded zip file

	cd /home/ec2-user/

	unzip temp.zip

      * Move the extracted files to the Apache web root directory (/var/www/html/):

	cd templatemo_589_lugx_gaming  # cd into the unzipped directory

	sudo mv * /var/www/html/

      * Set the correct file ownership:

	sudo chown -R ec2-user:ec2-user /var/www/html

      * Clean up the temporary zip file:

	rm -f temp.zip

7. Configure Security Group
      * In the AWS Management Console, configure the security group associated with your EC2 instance to allow inbound HTTP traffic on port 80. This allows users to access your web application through a web browser.
                  
8. Access the Web Application
      * Open a web browser and enter the public IP address or public DNS name of your EC2 instance. Your web application should now be live.

	http://13.244.63.82/product-details.html

Conclusion

By following these steps, I successfully deployed a web application on an Amazon EC2 instance. This process involves setting up the server environment, installing the web server, deploying the application files, and configuring security settings.
