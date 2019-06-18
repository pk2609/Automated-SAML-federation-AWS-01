# Automated-SAML-federation-AWS-01-
Automation of SAML federation using AD and ADFS servers

# Requirements:
User name: A valid user-name of your choice.
Group name: A adds forest group name
DSRM pass: A recovery password for the DC server.
UserPass: A password for the created user.
Domain name: A unique domain name to create a new forest.
SAMLProviderName: Name of the idp you wish to choose.
KeyPairName: A new key pair for the ec2 instances. (You will need to create one on your own in your AWS account/console)
IAMRoleName: The role name your users wish to assume while logging into the AWS console.
S3BucketName: The name of the S3 bucket you wish to create. (To handle the federation metadata)
VPCId: Your unique VPCId.

# AWS Services Used
1. CloudFormation: Used to create the template that provisions all the required resources and automates the process.

2. EC2: Active Directory(AD) and Active Directory Federation Service(ADFS) are set up on two EC2 Windows Server 2012 R2 Base instances.

3. S3: The Federation Metadata document provided by ADFS is stored in an S3 bucket.

4. IAM: User permissions, roles and the the identity provider are managed by IAM.

5. Lambda: Used to create the identity provider and is triggered when the federation metadata document is uploaded into the S3 bucket.

# Challenges Faced
1. Referencing the variables inside the powershell user-script. Concatenation of long string variables was also a bit challenging.

2. Creation of the custom lambda function for identity provider.

3. Referencing variables between two different user-data (Eg: using DC instance's Private IP in the ADFS EC2 instance)

4. Storing the Federation metadata. All the possibilities were looked in detail as we wanted a way to extract the metadata that was stored in a local EC2 instance.

5. Putting a wait condition.  There should be enough time to get the metadata for the idp (identity provider)before the actual creation of the resource. It was realised it's not possible to use the cfn-init and cfn-wait condition in this use-case.

6. Concluding an appropriate sleep-time in powershell so that the federation metadata is obtained before the idp creation and the claim rules are configured after the idp creation.

7. The integration of the powershell and CloudFormation proved to be one of the biggest challenge in the project.

# What Next?
1. Sharing the project with the team and collecting feedback (2-3 months).

2. Implementing any feedbacks given and improving the project accordingly.

3. Pushing the project for AppSec Review for global scope.

4. Finally, to try and push the project to customers.
