# python-automation-on-aws-and-linode

#### We are using boto3 aws python sdk for doing some automation with python on aws services plus monitor website which is running on cloud server like linode.

#### We are also using the schedule library, automated process that triggers the program at a specific time mentioned
```
pip install schedule
```

### 1. Creating VPC using python boto3 aws sdk (since it doesn't have state, i prefer terraform for infrastructure provisioning)
Filename: create-vpc.py


### 2. EC2 Instance Status Check
Filename: ec2-status-checks.py
#### lets say we have created 100 instance on aws using terraform, and we have some auto scaling configured, since ec2 instance needs time to fully initialize, we want to know which instance are in which states (ready, initializing, running)


### 3. Add tags to EC2 Instances (All instances are created using terraform)
Filename: add-env-tags.py 
#### lets say we have 20 servers in frankfurt region, which are used as production servers, but we also have 10 servers in paris region, that we use as development servers. now we want to tags to all servers, we want to add env prod to all servers in frankfurt and env dev to all servers in paris. We want to do this using python at once.


### 4. EKS Cluster Status Check (All clusters are created using terraform)
Filename: eks-status-checks.py
#### lets say we have created 10 eks cluster in our aws account using terraform, lets say we want to have overview of all our running cluster. we want to see which status they have, are they in active state or failed or creating or whatever state. We also want to know for each cluster, which kubernetes version the cluster is running and the cluster endpoint. We want these 3 pieces of information printed out for all our clusters.. We are doing this using python, or we can also display these info in a user interface (webUI) instead of printing out on a console only


### 5. Automate BackUp for EC2 Instances:Creating Snapshots
Filename: volume-backups.py
#### We are going to create snapshots of volumes for our ec2 instances. volumes are storage components that stores the data of ec2 instance. every ec2 instane has its own volume where it writes all of its data...volume is like a hard drive for ec2 instance. When we create instance, volume get attached and when we delete, it will be deleted. Snapshots is a copy of the volume, exactly that time when we create the snapshot. snapshots are very important for data backup and creating new volumes. This is something we wnat to automate, if we have 100s of instance to ensure that we will latest backup data available incase an ec2 instance dies, or volume gets deleted or data gets corrupted in that volume. So we always need to have backup to recover the latest state of data.

#### lets say we have 50 ec2 volumes that have not been backed up, but recently some of the ec2 instance crashed and we lost some volumes and data in it.. so we think its very imp to do daily backup to avoid these from happening again... So we want to do automate backup with a python program.

#### We want to creat a python program that will create snapshots automatically everyday at a specific time


### 6. Automate Cleanup of old Snaptshots
Filename: cleanup-snapshots.py
#### If we create snapshots of volume everyday, we gonna have lots of snapshots by the end of the month depending on how many ec2 instances we have, which brings the storage demand on aws, which will bring up our bill. In terms of snapshots, we only need the most recent ones, we only need one or two latest one and we want to get rid of all the older snapshots.

#### So in addition to creating this automated backup snapshots, we are writing the program that cleans up old snapshots from your aws account. We want this clean up program to run automatically and may be decide to do this every month or week or so. We are writing python program that cleans up older snapshots, leaving only the latest two snapshots for every volume. We want to delete everything except for two most recent snapshots for each volume.

### 7. Automate restoring EC2 Volume from the Snapshots
Filename: restore-volume.py
#### Now we have a snapshot, how do we use that snapshot?.. lets say we have a instance running, and volume data got corrupted, basically sth else messed up with data, so our server is crashing cuz of the corrupted data. So we want to recover the latest working state of that ec2 instance by creating a new volume from the snapshots (snapshots = volume backup) and then attaching that volume to that ec2 instance so that it can continue running.

#### Basically we can create a new volume from the latest snapshots, which is not corrupted and attach the new volume to the instance.


### 8. Monitor Website 
Filename: monitor-website.py
#### Create a server on Linode Cloud Platform
#### Install docker on the server
#### Run NGINX container on it

#### We can access nginx application from browser... We are writing a python program that checks endpoint of the application and checks the status of the application...

#### If the response from application is not successful, either application is not accessible, server is down, if that happens, our python program will notify us through email that the website is down and we need to do something.

#### With python, we will automate fixing the problem as well, once we get notified, we will then extend the python logic to restart the docker container on the server, or if the server is not accessible, restart the server itself and docker container in ti.
