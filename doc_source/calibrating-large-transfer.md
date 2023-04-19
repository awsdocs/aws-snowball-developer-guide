# Calibrating a Large Transfer<a name="calibrating-large-transfer"></a>

You can calibrate a large transfer by transferring a representative set of your data transfer segments\. Choose a number of the data segments that you have defined and transfer them to a Snowball Edge device\. Make a record of the transfer speed and total transfer time for each operation\. If the calibration's results are less than the target transfer rate, you may be able to copy multiple parts of your data transfer at the same time\. In this case, repeat the calibration with the additional data transfer segment\.

Continue adding parallel copy operations during calibration until you see diminishing returns in the sum of the transfer speed of all instances currently transferring data\. End the last active instance and make a note of your new target transfer rate\.

You can transfer data faster with the AWS Snowball Edge device by transferring data in parallel using one of the following scenarios:
+ Using multiple sessions of the S3 interface on a workstation against a single Snowball Edge device\.
+ Using multiple sessions of the S3 interface on multiple workstations against a single Snowball Edge device\.
+ Using multiple sessions of the S3 interface \(using a single or multiple workstations\) targeting multiple Snowball Edge devices\.

When you complete these steps, you should know how quickly you can transfer data to an AWS Snowball Edge device\.