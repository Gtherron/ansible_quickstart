In an AWS Instance Role (EC2):

    If you're using an EC2 instance, you may rely on an IAM role attached to the instance to automatically provide 
     credentials, rather than manually specifying the access key.

Best Practice for Security:

    Do not hardcode access keys in scripts or playbooks.
    Instead, use IAM roles (for EC2 or ECS tasks) or environment variables.
    If you must store keys, ensure they're stored securely and permissions are properly managed.

Using IAM roles for EC2 instances allows you to securely grant AWS permissions without needing to 
hardcode access keys (aws_access_key_id and aws_secret_access_key). When you attach an IAM role to an EC2 instance, 
it automatically assumes the role and can use temporary credentials to access AWS services like CloudWatch, S3, etc.

Steps:

    Create an IAM Role for your EC2 instance with the necessary permissions.
    Attach the IAM Role to the EC2 instance.
    Use the playbook to deploy or configure services on the EC2 instance, without specifying the access key and secret key.

Step 1: Create an IAM Role for EC2

    Go to the AWS Management Console and navigate to IAM.
    Select Roles and click on Create role.
    Select AWS Service and choose EC2.
    Click Next: Permissions and attach a policy like CloudWatchAgentServerPolicy or any custom policy you 
    need for the instance.
    Review and create the role.
    Attach this IAM role to your EC2 instance.

Step 2: Attach the IAM Role to the EC2 Instance

    Navigate to EC2 in the AWS Console.
    Select the instance you want to modify.
    Click Actions > Security > Modify IAM Role.
    Choose the IAM role you created and attach it to the instance.

Step 3: Example Ansible Playbook

This playbook will configure the CloudWatch agent on the EC2 instance, and the instance will use the 
attached IAM role for permissions without needing access keys.