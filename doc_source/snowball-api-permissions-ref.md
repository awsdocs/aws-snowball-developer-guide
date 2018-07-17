--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# AWS Snowball API Permissions: Actions, Resources, and Conditions Reference<a name="snowball-api-permissions-ref"></a>

When you are setting up [Access Control in the AWS Cloud](authentication-and-access-control.md#access-control) and writing a permissions policy that you can attach to an IAM identity \(identity\-based policies\), you can use the following table as a reference\. The table lists each AWS Snowball job management API operation, the corresponding actions for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

You can use AWS\-wide condition keys in your AWS Snowball policies to express conditions\. For a complete list of AWS\-wide keys, see [Available Keys](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `snowball:` prefix followed by the API operation name \(for example, `snowball:CreateJob`\)\.

If you see an expand arrow \(**↗**\) in the upper\-right corner of the table, you can open the table in a new window\. To close the window, choose the close button \(**X**\) in the lower\-right corner\.


**AWS Snowball Job Management API and Required Permissions for Actions**  

| Job Management API Actions | Required Permissions | 
| --- | --- | 
|   [CancelCluster](http://docs.aws.amazon.com/snowball/latest/api-reference/API_CancelCluster.html)   | snowball:CancelCluster | 
|   [CancelJob](http://docs.aws.amazon.com/snowball/latest/api-reference/API_CancelJob.html)  |  `snowball:CancelJob`  | 
|   [CreateAddress](http://docs.aws.amazon.com/snowball/latest/api-reference/API_CreateAddress.html)  | snowball:CreateAddress | 
|   [CreateCluster](http://docs.aws.amazon.com/snowball/latest/api-reference/API_CreateCluster.html)  | This action requires the following permissions: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/snowball-api-permissions-ref.html) | 
|   [CreateJob](http://docs.aws.amazon.com/snowball/latest/api-reference/API_CreateJob.html)  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/snowball-api-permissions-ref.html) | 
|   [DescribeAddress](http://docs.aws.amazon.com/snowball/latest/api-reference/API_DescribeAddress.html)  | snowball:DescribeAddress | 
|   [DescribeAddresses](http://docs.aws.amazon.com/snowball/latest/api-reference/API_DescribeAddresses.html)  | snowball:DescribeAddresses | 
|   [DescribeCluster](http://docs.aws.amazon.com/snowball/latest/api-reference/API_DescribeCluster.html)  | snowball:DescribeCluster | 
|   [DescribeJob](http://docs.aws.amazon.com/snowball/latest/api-reference/API_DescribeJob.html)  | snowball:DescribeJob | 
|   [GetJobManifest](http://docs.aws.amazon.com/snowball/latest/api-reference/API_GetJobManifest.html)  | snowball:GetJobManifest | 
|   [GetJobUnlockCode](http://docs.aws.amazon.com/snowball/latest/api-reference/API_GetJobUnlockCode.html)  | snowball:GetJobUnlockCode | 
|   [GetSnowballUsage](http://docs.aws.amazon.com/snowball/latest/api-reference/API_GetSnowballUsage.html)  | snowball:GetSnowballUsage | 
|   [ListClusterJobs](http://docs.aws.amazon.com/snowball/latest/api-reference/API_ListClusterJobs.html)  | snowball:ListClusterJobs | 
|   [ListClusters](http://docs.aws.amazon.com/snowball/latest/api-reference/API_ListClusters.html)  | snowball:ListClusters | 
|   [ListJobs](http://docs.aws.amazon.com/snowball/latest/api-reference/API_ListJobs.html)  | snowball:ListJobs | 
|   [UpdateCluster](http://docs.aws.amazon.com/snowball/latest/api-reference/API_UpdateCluster.html)  | snowball:UpdateCluster | 
|   [UpdateJob](http://docs.aws.amazon.com/snowball/latest/api-reference/API_UpdateJob.html)  | snowball:UpdateJob | 