--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Supported Instance Metadata and User Data<a name="edge-compute-instance-metadata"></a>

Instance metadata is data about your instance that you can use to configure or manage the running instance\. Snowball Edge supports a subset of instance metadata categories for your compute instances\. For more information, see [Instance Metadata and User Data](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html) in the Amazon EC2 User Guide for Linux Instances\.

The following categories are supported\. Using any other categories will return a `404` error message\.


**Supported Instance Metadata Categories on a Snowball Edge**  

| Data | Description | 
| --- | --- | 
|  ami\-id  | The AMI ID used to launch the instance\. | 
| hostname | The private IPv4 DNS hostname of the instance\. | 
|  instance\-id  | The ID of this instance\. | 
|  instance\-type  | The type of instance\. | 
|  local\-hostname  | The private IPv4 DNS hostname of the instance\. | 
|  local\-ipv4  | The private IPv4 address of the instance\. | 
|  mac  | The instance's media access control \(MAC\) address\. | 
|  network/interfaces/macs/mac/local\-hostname  | The interface's local hostname\. | 
|  network/interfaces/macs/mac/local\-ipv4s  | The private IPv4 addresses associated with the interface\. | 
|  network/interfaces/macs/mac/mac  | The instance's MAC address\. | 
|  network/interfaces/macs/mac/public\-ipv4s  | The Elastic IP addresses associated with the interface\. | 
|  public\-ipv4  | The public IPv4 address\. | 
|  public\-keys/0/openssh\-key  | Public key\. Only available if supplied at instance launch time\. | 
|  reservation\-id  | The ID of the reservation\. | 


**Supported Instance Dynamic Data Categories on a Snowball Edge**  

| Data | Description | 
| --- | --- | 
| instance\-identity/document | JSON containing instance attributes\. Note that only instanceId, imageId, privateIp, and instanceType have values, while the other returned attributes are null\. For more information, see [Instance Identity Documents](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/instance-identity-documents.html) in the Amazon EC2 User Guide for Linux Instances\. | 