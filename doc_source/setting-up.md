# Setting Up Your AWS Access for AWS Snowball Edge<a name="setting-up"></a>

Before you use AWS Snowball Edge for the first time, you need to complete the following tasks:

1. [Sign Up for AWS](#setting-up-signup)\.
**Note**  
In the Asia Pacific \(Mumbai\) AWS Region service is provided by Amazon on Internet Services Private Limited \(AISPL\)\. For information on signing up for Amazon Web Services in the Asia Pacific \(Mumbai\) AWS Region, see [Signing Up for AISPL](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-account-payment-aispl.html#aisplsignup)\.

1. [Create an IAM User](#setting-up-iam)\.

## Sign Up for AWS<a name="setting-up-signup"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including AWS Snow Family\. You are charged only for the services that you use\. For more information about pricing and fees, see [AWS Snowball Edge Pricing](http://aws.amazon.com/snowball-edge/pricing)\. AWS Snowball Edge is not free to use\. For more information on what AWS services are free, see [AWS Free Usage Tier](http://aws.amazon.com/free/)\.

If you have an AWS account already, skip to the next task\. If you don't have an AWS account, use the following procedure to create one\.

**To create an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

   When you sign up for an AWS account, an *AWS account root user* is created\. The root user has access to all AWS services and resources in the account\. As a security best practice, [assign administrative access to an administrative user](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html), and use only the root user to perform [tasks that require root user access](https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html)\.

Note your AWS account number, because you'll need it for the next task\.

## Create an IAM User<a name="setting-up-iam"></a>

Services in AWS, such as AWS Snowball Edge, require that you provide credentials when you access them, so that the service can determine whether you have permission to access its resources\. AWS recommends not using the root credentials of your AWS account to make requests\. Instead, create an AWS Identity and Access Management \(IAM\) user, and grant that user full access\. We refer to these users as IAM users with administrator\-level credentials\.

You can use the administrator user credentials, instead of root credentials of your account, to interact with AWS and perform tasks, such as to create an Amazon S3 bucket, create users, and grant them permissions\. For more information, see [Comparing AWS account root user credentials and IAM user credentials](https://docs.aws.amazon.com/general/latest/gr/root-user-vs-iam.html) in the *AWS General Reference* and [IAM Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPractices.html) in *IAM User Guide*\. 

If you signed up for AWS but have not created an IAM user for yourself, you can create one using the IAM console\.

To create an administrator user, choose one of the following options\.


****  

| Choose one way to manage your administrator | To | By | You can also | 
| --- | --- | --- | --- | 
| In IAM Identity Center \(Recommended\) | Use short\-term credentials to access AWS\.This aligns with the security best practices\. For information about best practices, see [Security best practices in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html#bp-users-federation-idp) in the *IAM User Guide*\. | Following the instructions in [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the AWS IAM Identity Center \(successor to AWS Single Sign\-On\) User Guide\. | Configure programmatic access by [Configuring the AWS CLI to use AWS IAM Identity Center \(successor to AWS Single Sign\-On\)](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html) in the AWS Command Line Interface User Guide\. | 
| In IAM \(Not recommended\) | Use long\-term credentials to access AWS\. | Following the instructions in [Creating your first IAM admin user and user group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the IAM User Guide\. | Configure programmatic access by [Managing access keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html) in the IAM User Guide\. | 

To sign in as this new IAM user, sign out of the AWS Management Console, then use the following URL, where *your\_aws\_account\_id* is your AWS account number without the hyphens \(for example, if your AWS account number is `1234-5678-9012`, your AWS account ID is `123456789012`\)\.

```
https://your_aws_account_id.signin.aws.amazon.com/console/
```

Type the IAM user name and sign\-in credentials that you just created\. When you're signed in, the navigation bar displays "*your\_user\_name* @ *your\_aws\_account\_id*"\.

If you don't want the URL for your sign\-in page to contain your AWS account ID, you can create an account alias\. From the IAM dashboard, choose **Create Account Alias** and type an alias, such as your company name\. To sign in after you create an account alias, use the following URL\.

```
https://your_account_alias.signin.aws.amazon.com/console/
```

To verify the sign\-in link for IAM users for your account, open the IAM console and check under **AWS account Alias** on the dashboard\.

If you're going to create AWS Snowball Edge jobs through an IAM user that is not an administrator user, that user needs certain permissions to use the AWS Snow Family Management Console effectively\. For more information on those permissions, see [Permissions Required to Use the AWS Snowball Console](access-control-managing-permissions.md#additional-console-required-permissions)\.

## Next Step<a name="setting-up-next-step"></a>

[Getting Started](getting-started.md)