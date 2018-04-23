--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Using the Snowball Client<a name="using-client"></a>

Following, you can find information about how to get and use the Snowball client with your AWS Snowball Edge appliance\. The Snowball client is a standalone terminal application that you run on your local server to unlock the appliance and get credentials, logs, and status information\. You can also use the client for administrative tasks for a cluster\. While using the Snowball client, you can get additional support information by running the `snowballEdge help` command\.

When you read and write data to the AWS Snowball Edge appliance, you use the Amazon S3 Adapter for Snowball or the file interface\.

**Note**  
In January 2018, there was a feature update for clusters, making them leaderless\. The cluster update is backward\-compatible with older clusters\. However, if you're looking for documentation for the original Snowball client for Snowball Edge, see [Using the Snowball Client](old-using-client.md) in the Appendices\.

## Downloading and Installing the Snowball Client<a name="download-client"></a>

You can download and install the Snowball client from the [AWS Snowball Tools Download](http://aws.amazon.com/snowball/tools) page\. On that page, you can find the installation package for your operating system and follow the instructions to install the Snowball client\. Running the Snowball client from a terminal in your workstation might require using a specific path, depending on your operating system:
+ **Microsoft Windows** – When the client has been installed, you can run it from any directory without any additional preparation\.
+ **Linux** – The Snowball client must be run from the \~/snowball\-client\-linux\-*build\_number*/bin/ directory\.
+ **Mac** – The `install.sh` script copies folders from the Snowball client \.tar file to the /usr/local/bin/snowball directory\. If you run this script, you can then run the Snowball client from any directory if /usr/local/bin is a path in your bash\_profile\. You can verify your path with the `echo $PATH` command\.