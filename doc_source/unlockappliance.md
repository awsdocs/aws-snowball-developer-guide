--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Unlock the Snowball Edge<a name="unlockappliance"></a>

To unlock the AWS Snowball Edge appliance, run the `snowballEdge unlock` command\. To run this command, the AWS Snowball Edge appliance that you use for your job must be onsite, plugged into power and network, and turned on\. In addition, the LCD display on the AWS Snowball Edge appliance's front must indicate that the appliance is ready for use\.

**To unlock the appliance with the Snowball client**

1. Get your manifest and unlock code\.

   1. Download a copy of the manifest from the AWS Snowball Management Console\. Your job's manifest is encrypted so that only the job's unlock code can decrypt it\. Make a note of the path to the manifest file on your local server\.

   1. Get the unlock code, a 29\-character code that also appears when you download your manifest\. We recommend that you write down the unlock code and keep it in a separate location from the manifest that you downloaded, to prevent unauthorized access to the AWS Snowball Edge appliance while it’s at your facility\.

1. Find the IP address for the AWS Snowball Edge appliance on the AWS Snowball Edge appliance's LCD display, under the **Connections** tab\. Make a note of that IP address\.

1. Run the `snowballEdge unlock` command to authenticate your access to the AWS Snowball Edge appliance with the AWS Snowball Edge appliance's IP address and your credentials, as follows:

   ```
   snowballEdge unlock -i [IP Address] -m [Path/to/manifest/file] -u [29
                           character unlock code]
   ```

Following is an example of the command to unlock the Snowball client\.

```
snowballEdge unlock -i 192.0.2.0 -m /Downloads/JID2EXAMPLE-0c40-49a7-9f53-916aEXAMPLE81-manifest.bin  -u 12345-abcde-12345-ABCDE-12345
```

In this example, the IP address for the appliance is `192.0.2.0`, the job manifest file that you downloaded is `JID2EXAMPLE-0c40-49a7-9f53-916aEXAMPLE81-manifest.bin`, and the 29\-character unlock code is `12345-abcde-12345-ABCDE-12345`\.

When you've entered the preceding command with the right variables for your job, you get a confirmation message\. This message means that you're authorized to access the appliance for this job\.

**Job\-Type Specific Consideration**

If you're unlocking a cluster, you'll need to specify the `-s` option for each of the secondary nodes\. For more information, see [Using the Snowball Client](using-client.md)\.

Now you can begin using the AWS Snowball Edge appliance\. 

**Next:** [Use the Snowball Edge](transfer-data.md) 