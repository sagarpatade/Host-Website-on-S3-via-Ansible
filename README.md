# Day 16: AWS S3 Static Website Deployment via Ansible

This repository contains an Ansible Playbook and Role designed to automatically provision an Amazon S3 bucket, configure it for static website hosting, apply the necessary public read policies, and sync local HTML files to the bucket.

##  Directory Structure

This project uses Ansible Roles for modularity and best practices.

```text
day16-task/
├── playbook.yml                 # The main playbook that calls the role
└── roles/
    └── s3_website/              # The Ansible Role
        ├── files/
        │   └── index.html       # The website content to be uploaded
        ├── tasks/
        │   └── main.yml         # The AWS API execution tasks
        └── vars/
            └── main.yml         # Variables (bucket name, region)

Prerequisites

Before running this playbook, ensure your control node (e.g., Ubuntu WSL) has the following installed:

Ansible: The core automation tool.
Python AWS SDK: Required for Ansible to talk to the AWS API.

pip3 install boto3 botocore

Ansible AWS Collections:

ansible-galaxy collection install amazon.aws
ansible-galaxy collection install community.aws

AWS Authentication
Ansible needs your AWS credentials to create the infrastructure. Export your keys in your terminal before running the playbook:


export AWS_ACCESS_KEY_ID="your_access_key_here"
export AWS_SECRET_ACCESS_KEY="your_secret_key_here"


How to Run

Clone this repository or navigate to the project folder.

(Optional) Update the index.html file inside roles/s3_website/files/ with your custom website code.

(Optional) Adjust the aws_region in roles/s3_website/vars/main.yml.

Execute the playbook from the root directory:

ansible-playbook playbook.yml

Expected Output

When the playbook finishes successfully, you will see a debug message at the very end of your terminal output. It will provide the exact, live URL where your static website is hosted:

Plaintext
TASK [s3_website : Output the live website URL] *****************************
ok: [localhost] => {
    "msg": "Your website is live at: [http://sagar-day16-website-4829.s3-website-us-east-1.amazonaws.com](http://sagar-day16-website-4829.s3-website-us-east-1.amazonaws.com)"
}