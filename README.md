# GCP_AWS_Terraform

#Cloud Computing projects #Multicloud #AWS #GCP #Terraform

Luxury Hotel and Resorts Company migrating application and data to the Cloud

Solution Architecture
GCP
Google container registry-Docker
The first component is VPC-virtual private cloud
Google cloud SQL
Kubernetes to deploy GKE

AWS
S3 bucket

Deploy the multicloud using Terraform

AWS -creating a user
Access AWS console and go to IAM
under Access mgt, click in "Users", then "Add User" and create a programmatic user "terraform-en-1"

on Set permissions, click on "Attach exisiting policies directly" button
select AmazonS3FullAccess
click on Next : Tags
click on Next Review
Click on Create User
Click on Download .csv
after download, rename .csv to accessKeys.csv

GCP

Access GCP Console and open Cloud Shell
Upload accessKeys.csv and mission1.zip hands.on file to GCP Cloud Shell
check if upload has been done ls -la

files preparation

mkdir mission1-en
mv mission1.zip mission1-en

cd mission1-en
unzip mission1.zip

mv ~/accessKeys.csv mission1/en
cd mission1/en
chmod +x \*.sh

scripts to prepare AWS and GCP env

./aws_set_credentials.sh accessKeys.csv
gcloud config set project <project_id>

./gcp_set_project.sh

enable the container registery API , Kubernetes engine API and the clould SQL API

glcloud services enable containerregistry.googleapis.com
gcloud services enable container.googleapis.com
gcloud services enable sqladmin.googleapis.com

- **Before executing the Terraform commands, open the Google Editor and update the file tcb_aws_storage.tf replacing the bucket name with an unique name (AWS requires unique bucket names).**
  - Open the **tcb_aws_storage.tf** using Google Editor
  - On **line 4** of the file **tcb_aws_storage.tf**:
    - Replace **xxxx** with your name initials, using **5 letters** plus **5 random numbers**:
      Example: **luxxy-covid-testing-system-pdf-en-jerod29292**

finsih provision infracstructure with the ff steps

cd ~/mission1_en/mission1/en/terraform/

terraform init
terraform plan
terraform apply
type Yes and go ahead

access the cloud SQL service
click on Cloud SQL instance

on the left side, under Primary instance, click on Connections

Go to Networking tab

Under Instance IP assignment, slect Private Ip to enable

under Associated networiking select "Default"

click Set up connection

click on enable API , to enable service networking API (if asked)

select USE an automatically allocated IP range in your network

click continue

click create connecton and wait a minute until conclude
You will see the message: “Private services access connection for network default
 has been successfully created.”

Under Authorized Networks, click "Add Network".
Under New Network, enter the following information:
Name: Public Access (For testing purposes only)
Network: 0.0.0.0/0
Click Done.
Click Save and wait to finish the update.
This update may take from 10 to 20 minutes to finish

PS: For production environments, it is recommended to use only the Private Network for database access.
⚠️ Never grant public network access (0.0.0.0/0) to production databases.
