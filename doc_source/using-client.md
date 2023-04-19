# Using the Snowball Edge Client<a name="using-client"></a>

Following, you can find information about how to get and use the Snowball Edge client with your AWS Snowball Edge device\. The Snowball Edge client is a standalone terminal application that you run on your local server to unlock the device and get credentials, logs, and status information\. You can also use the client for administrative tasks for a cluster\. While using the Snowball Edge client, you can get additional support information by running the `snowballEdge help` command\.

When you read and write data to the AWS Snowball Edge device, you use the Amazon S3 interface or the file interface\.

**Note**  
In January 2018, there was a feature update for clusters, making them leaderless\. The cluster update is backward\-compatible with older clusters\. 

## Downloading and Installing the Snowball Edge Client<a name="download-client"></a>

You can download and install the Snowball Edge client from [AWS Snowball resources](https://aws.amazon.com/snowball/resources/)\.

You can download and install the Snowball Edge client from [AWS Snowball Edge Resources](http://aws.amazon.com/snowball-edge/resources/)\. On that page, you can find the installation package for your operating system\. Follow the instructions to install the Snowball Edge client\. Running the Snowball Edge client from a terminal in your workstation might require using a specific path, depending on your operating system:
+ **Microsoft Windows** – When the client has been installed, you can run it from any directory without any additional preparation\.
+ **Linux** – The Snowball Edge client must be run from the `~/snowball-client-linux-build_number/bin/` directory\. The Snowball Edge client is only supported on 64\-bit Linux distributions\.
+ **macOS** – The `install.sh` script copies folders from the Snowball Edge client \.tar file to the `/usr/local/bin/snowball` directory\. If you run this script, you can then run the Snowball Edge client from any directory if `/usr/local/bin` is a path in your `bash_profile`\. You can verify your path using the `echo $PATH` command\.