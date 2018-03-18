aws-ec2-ebs-automatic-snapshot-bash - for tagged instances
===================================

#### Bash script for Automatic EBS Snapshots and Cleanup on Amazon Web Services (AWS)
Pls note that this script need to execute from extenral server and it will run automat backup for all instances with spasific tag (Backup=True)

**How it works:**
ebs-snapshot.sh will:
- search for list of instances with tag specific tag (Backup=True)
- Gather a list of all volume IDs attached to that instance
- Take a snapshot of each attached volume
- The script will then delete all associated snapshots taken by the script that are older than 7 days

Pull requests greatly welcomed!

===================================

**REQUIREMENTS**

**IAM User:** This script requires that new IAM user credentials be created, with the following IAM security policy attached:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Stmt1426256275000",
            "Effect": "Allow",
            "Action": [
                "ec2:CreateSnapshot",
                "ec2:CreateTags",
                "ec2:DeleteSnapshot",
                "ec2:DescribeSnapshots",
                "ec2:DescribeVolumes"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```
<br />

**AWS CLI:** This script requires the AWS CLI tools to be installed.

First, make sure Python pip is installed:
```
# Ubuntu
sudo apt-get install python-pip -y

# Red Hat/CentOS
sudo yum install python-pip -y
```
Then install the AWS CLI tools: 
```
sudo pip install awscli
```
Once the AWS CLI has been installed, you'll need to configure it with the credentials of the IAM user created above:

```
sudo aws configure

AWS Access Key ID: (Enter in the IAM credentials generated above.)
AWS Secret Access Key: (Enter in the IAM credentials generated above.)
Default region name: (The region that this instance is in: i.e. us-east-1, eu-west-1, etc.)
Default output format: (Enter "text".)```
```
<br />

**Install Script**: Download the latest version of the snapshot script and make it executable.
