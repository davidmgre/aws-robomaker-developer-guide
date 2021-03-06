# Using Service\-Linked Roles for AWS RoboMaker<a name="using-service-linked-roles"></a>

AWS RoboMaker uses AWS Identity and Access Management \(IAM\)[ service\-linked roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role that is linked directly to AWS RoboMaker\. Service\-linked roles are predefined by AWS RoboMaker and include all the permissions that the service requires to call other AWS services on your behalf\. 

A service\-linked role makes setting up AWS RoboMaker easier because you don’t have to manually add the necessary permissions\. AWS RoboMaker defines the permissions of its service\-linked roles, and unless defined otherwise, only AWS RoboMaker can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

You can delete a service\-linked role only after first deleting their related resources\. This protects your AWS RoboMaker resources because you can't inadvertently remove permission to access the resources\.

For information about other services that support service\-linked roles, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes **in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-Linked Role Permissions for AWS RoboMaker<a name="slr-permissions"></a>

AWS RoboMaker uses the service\-linked role named **AWSServiceRoleForRoboMaker** – Allows RoboMaker to access EC2, Greengrass, and Lambda resources on your behalf\.

The AWSServiceRoleForRoboMaker service\-linked role trusts the following services to assume the role:
+ `robomaker.amazonaws.com`

The role permissions policy allows AWS RoboMaker to complete the following actions on the specified resources:
+ Create and cancel a simulation job created as part of a simulation job batch
+ Manage Amazon EC2 networking resources
+ Manage AWS IoT Greengrass deployments 

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a Service\-Linked Role for AWS RoboMaker<a name="create-slr"></a>

You don't need to manually create a service\-linked role\. When you SimulationJob or DeploymentJob in the AWS Management Console, the AWS CLI, or the AWS API, AWS RoboMaker creates the service\-linked role for you\. 

If you delete this service\-linked role, and then need to create it again, you can use the same process to recreate the role in your account\. When you create a SimulationJob, SimulationJobBatch, or DeploymentJob, AWS RoboMaker creates the service\-linked role for you again\. 

You can also use the IAM console to create a service\-linked role with the **RoboMaker** use case\. In the AWS CLI or the AWS API, create a service\-linked role with the `robomaker.amazonaws.com` service name\. For more information, see [Creating a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\. If you delete this service\-linked role, you can use this same process to create the role again\.

## Editing a Service\-Linked Role for AWS RoboMaker<a name="edit-slr"></a>

AWS RoboMaker does not allow you to edit the AWSServiceRoleForRoboMaker service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a Service\-Linked Role for AWS RoboMaker<a name="delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don’t have an unused entity that is not actively monitored or maintained\. However, you must clean up the resources for your service\-linked role before you can manually delete it\.

**Note**  
If the AWS RoboMaker service is using the role when you try to delete the resources, then the deletion might fail\. If that happens, wait for a few minutes and try the operation again\.

**To manually delete the service\-linked role using IAM**

Use the IAM console, the AWS CLI, or the AWS API to delete the AWSServiceRoleForRoboMaker service\-linked role\. For more information, see [Deleting a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Supported Regions for AWS RoboMaker Service\-Linked Roles<a name="slr-regions"></a>

AWS RoboMaker supports using service\-linked roles in all of the regions where the service is available\. For more information, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html)\.

AWS RoboMaker does not support using service\-linked roles in every region where the service is available\. You can use the AWSServiceRoleForRoboMaker role in the following regions\.


****  

| Region name | Region identity | Support in AWS RoboMaker | 
| --- | --- | --- | 
| US East \(N\. Virginia\) | us\-east\-1 | Yes | 
| US East \(Ohio\) | us\-east\-2 | Yes | 
| US West \(N\. California\) | us\-west\-1 | Yes | 
| US West \(Oregon\) | us\-west\-2 | Yes | 
| Asia Pacific \(Mumbai\) | ap\-south\-1 | Yes | 
| Asia Pacific \(Osaka\-Local\) | ap\-northeast\-3 | Yes | 
| Asia Pacific \(Seoul\) | ap\-northeast\-2 | Yes | 
| Asia Pacific \(Singapore\) | ap\-southeast\-1 | Yes | 
| Asia Pacific \(Sydney\) | ap\-southeast\-2 | Yes | 
| Asia Pacific \(Tokyo\) | ap\-northeast\-1 | Yes | 
| Canada \(Central\) | ca\-central\-1 | Yes | 
| Europe \(Frankfurt\) | eu\-central\-1 | Yes | 
| Europe \(Ireland\) | eu\-west\-1 | Yes | 
| Europe \(London\) | eu\-west\-2 | Yes | 
| Europe \(Paris\) | eu\-west\-3 | Yes | 
| South America \(São Paulo\) | sa\-east\-1 | Yes | 
| AWS GovCloud \(US\) | us\-gov\-west\-1 | No | 