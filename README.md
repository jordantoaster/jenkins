## Overview

This sample repository is to outline a basic setup for a remotr Jenkins server on AWS alongside a basic CI pipeline.

This example has a single primary aster node for Jenkins, with no secondary nodes for autoscaling..

## Jenkins on AWS Setup

1. In your AWS console create a micro EC2 Linux instance - Add a security group for TCP access to port 8080

2. SSH into your EC2 Machine.

3. Update the stock packages - ``sudo yum update –y``

4. Ensure you have the 1.8 version of Java - ``sudo yum install java-1.8.0`` + ``sudo yum remove java-1.7.0-openjdk``

5. Get the Jenkins Repository reference - ``sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo``

6. Get the key for the Jenkins install - ``sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key``

7. Install Jenkins - ``sudo yum install jenkins -y``

8. Start Jenkins - ``sudo service jenkins start``

9. Navigate to the IP of your machine, aiming for port 8080.

10. Run ``sudo cat /var/lib/jenkins/secrets/initialAdminPassword`` to get your initial Jenkins admin password inside your SSH terminal, enter the result into the 'unlock' screen of Jenkins.

11. Install the recommended set of plugins for Jenkins.

Now you can create users and pipelines as required.

## Pipeline Example Overview

