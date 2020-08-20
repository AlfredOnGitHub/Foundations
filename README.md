Fundations

This project is made for fun, just to push harder.

We are using Ansible to do quite a few things with AWS, Jenkins, Jinja, etc.

An AWS provisioning Ansible role.
`ansible-playbook main.yml -e "status="

`ansible-playbook run.yml`

You have some test using Jinja and the template module into the 'Instances' folder, as well as some Jenkins test.
You can get one httpd server listening to a specific port and another httpd server listening to another different port, you only need to specify the publicip of both servers into the httpd.conf file and set it as a group called 'instances' into the Ansible host file.

AWS folder hold everything related with AWS.
Instances folder hold everything related with the instances.

-AWS-

Required values for "status": 

- Create
Create the entire environment.
You will get a Keypair based on -your public ip- (you need to change it into the create.yml file), 2 Instances t2.micro using CentOS, with an extra volume of 5g and 2 Elastic IPs allocated to each instance.

- Destroy
Everything will get terminated but the EIPs. The EIPs will remain and you need to release it by your own because this project is not fully automated yet and is a pain in the ass to put the EIPs everytime you want to create again everything.

- Start
Every stopped instance will be running after using this status.

- Stop
Every running instance will be stopped after using this status.


-Instances-
Into the instances folder we have three files: 'Apache.yml', 'httpd.conf' and 'jenkins.yml'.

'Apache.yml' will install and run an httpd server into the instances, and in depends of wich server EIP, will be listening to the port 8080 or 8081 due to the Jinja filter into the httpd.conf file.
You need to specify the EIPs for this to work into the Ansible hosts file, in the httpd.conf file and deal with the fingerprints.
You also need to get the EIPs defined into the Ansible hosts file in a group called 'instances'

'Jenkins.yml' will download the repository, import the key to the RPM, install and then run Jenkins on an instance.
You only need to get the EIPs defined into the Ansible hosts file in a group called 'instances'.

What you need:
- AWS.
- An user into AWS with programmatic access.
- A "keycred" file. A file with your credentials and variables so Ansible can read it.
You can call it whatever you want, but remember to modify the "main.yml" file so Ansible can get everything.
