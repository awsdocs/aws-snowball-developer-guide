--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](https://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Network Configuration for Compute Instances<a name="network-config-ec2-edge"></a>

After you’ve launched your compute instances on a Snowball Edge device, you need to set up your network configuration for each instance\. Use the following procedure whenever you launch a new instance to give that instance a virtual network interface and IP address\.

1. Make sure there's power to your device and that one of your physical network interfaces, like the RJ45 port, are connected with an IP address\.

1. Get the IP address associated with the physical network interface that you're using on the Snowball Edge\. For more information, see [Connect to Your Local Network](getting-started-connect.md)\.

1. Configure your Snowball client\. For more information, see [Configuring a Profile for the Snowball Client](using-client-commands.md#client-configuration)\.

1. Unlock the device\. For more information, see [Unlocking Snowball Edge Devices](using-client-commands.md#setting-up-client)\.

1. Run the `snowballEdge describe-device` command to get the list of physical network interface IDs\.

1. Identify the ID for the physical network interface that you want to use, and make a note of it\.

1. Run the `snowballEdge create-virtual-network-interface` command\. The following examples show running this command with the two different IP address assignment methods, either DHCP or STATIC\.

   ```
   snowballEdge create-virtual-network-interface \
   --physical-network-interface-id s.ni-abcd1234 \
   --ip-address-assignment DHCP
            
           //OR//
           
   snowballEdge create-virtual-network-interface \
   --physical-network-interface-id s.ni-abcd1234 \
   --ip-address-assignment STATIC \
   --static-ip-address-configuration IpAddress=192.0.2.0,Netmask=255.255.255.0
   ```

1. The command returns a JSON structure that includes the IP address\. Make a note of that IP address for the `ec2 associate-address` AWS CLI command later in the process\.

1. Anytime you need this IP address, you can use the `snowballEdge describe-virtual-network-interfaces` Snowball client command, or the `aws ec2 describe-addresses` AWS CLI command to get it\.

1. Associate your newly created IP address with the instance, using the following AWS CLI command\.

   ```
   aws ec2 associate-address --public-ip 192.0.2.0 --instance-id s.i-01234567890123456 --endpoint <physical IP address for your Snowball Edge>:8008
   ```