# Network Configuration for Compute Instances<a name="network-config-ec2"></a>

After you launch your compute instances on a Snow Family device, you must provide it with an IP address by creating a network interface\. Snow Family devices support two kinds of network interfaces, a virtual network interface and a direct network interface\. 

**Virtual network interface \(VNI\)**

A virtual network interface is the standard network interface for connecting to an EC2 instance on your Snow Family device\. You must create a VNI for each of your EC2 instances regardless of whether you also use a direct network interface or not\. The traffic passing through a VNI is protected by the security groups that you set up\. You can only associate VNIs with the physical network port you use to control your Snow Family device\.

**Note**  
VNI: All physical interfaces \(RJ45, SFP\+, and QSFP\) are supported\.

**Direct network interface \(DNI\)**

A direct network interface \(DNI\) is an advanced network feature that enables use cases like multicast streams, transitive routing, and load balancing\. By providing instances with layer 2 network access without any intermediary translation or filtering, you can gain increased flexibility over the network configuration of your Snow Family device and improved network performance\. DNIs support VLAN tags and customizing the MAC address\. Traffic on DNIs is not protected by security groups\.

On Snowball Edge devices, DNIs can be associated with the SFP or QSFP ports\. DNIs cannot be associated with RJ45 ports\. Each optical port supports a maximum of seven DNIs\. DNIs do not have to be associated to the physical network port you use to control your Snow Family device\. One EC2 instance can support four DNIs and another instance can support three, for a maximum of seven per device\. 

**Note**  
Snowball Edge storage optimized \(with EC2 compute functionality\) devices don't support DNIs\.

**Topics**
+ [Prerequisites](#snowcone-configuration-prerequisites)
+ [Setting Up a Virtual Network Interface \(VNI\)](#snowcone-setup-vni)
+ [Setting Up a Direct Network Interface \(DNI\)](#snowcone-setup-dni)

## Prerequisites<a name="snowcone-configuration-prerequisites"></a>

Before you configure a VNI or a DNI, be sure that you've done the following prerequisites\.

****

1. Make sure there's power to your device and that one of your physical network interfaces, like the RJ45 port, is connected with an IP address\.

1. Get the IP address associated with the physical network interface that you're using on the Snow Family device\.

1. Configure your Snowball Edge client\. For more information, see [Configuring a Profile for the Snowball Edge Client](https://docs.aws.amazon.com/snowball/latest/developer-guide/using-client-commands.html#client-configuration)\.

1. Unlock the device\. We recommend using AWS OpsHub for Snow Family to unlock your device\. For instructions, see [Unlocking a Device](https://docs.aws.amazon.com/snowball/latest/developer-guide/connect-unlock-device-sbe.html)\.

   If you want to use the CLI command, run the following command, and provide the information that appears in the dialog box\.

   ```
   snowballEdge configure 
   ```

   `Snowball Edge Manifest Path: manifest.bin`

   `Unlock Code: unlock code`

   `Default Endpoint: https://device ip`

1. Run the following command\.

   ```
   snowballEdge unlock-device
   ```

   The device display update indicates that it is unlocked\.

1. Launch an EC2 instance on the device\. You will associate the VNI with this instance\.

1. Run the `snowballEdge describe-device` command to get the list of physical network interface IDs\.

1. Identify the ID for the physical network interface that you want to use, and make a note of it\.

## Setting Up a Virtual Network Interface \(VNI\)<a name="snowcone-setup-vni"></a>

 After you have identified the ID for your physical network interface, you can set up a virtual network interface \(VNI\)\. Use the following procedure set up a VNI\. Make sure that you perform the prerequisite tasks before you create a VNI\.

**Create a VNI and associate IP address**

1. Run the `snowballEdge create-virtual-network-interface` command\. The following examples show running this command with the two different IP address assignment methods, either `DHCP` or `STATIC`\. The `DHCP` method uses Dynamic Host Configuration Protocol \(DHCP\)\.

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

   The command returns a JSON structure that includes the IP address\. Make a note of that IP address for the `ec2 associate-address` AWS CLI command later in the process\.

   Anytime you need this IP address, you can use the `snowballEdge describe-virtual-network-interfaces` Snowball Edge client command, or the `aws ec2 describe-addresses` AWS CLI command to get it\.

1. To associate your newly created IP address with your instance, use the following command, replacing the red text with your values:

   ```
   aws ec2 associate-address --public-ip 192.0.2.0 --instance-id s.i-01234567890123456 --endpoint http://Snow Family device physical IP address:8008
   ```

## Setting Up a Direct Network Interface \(DNI\)<a name="snowcone-setup-dni"></a>

**Note**  
 The direct network interface feature is available on or after January 12, 2021 and is available in all AWS Regions where Snow Family devices are available\.

### Prerequisites<a name="use-snowwire-prerequisites"></a>

Before you set up a direct network interface \(DNI\), you must perform the tasks in the prerequisites section\.

1. Perform the prerequisite tasks before setting up the DNI\. For instructions, see [Prerequisites](#snowcone-configuration-prerequisites)\.

1. Additionally, you must launch an instance on your device, create a VNI, and associate it with the instance\. For instructions, see [Setting Up a Virtual Network Interface \(VNI\)](#snowcone-setup-vni)\.
**Note**  
If you added direct networking to your existing device by performing an in\-the\-field software update, you must restart the device twice to fully enable the feature\.

**Create a DNI and associate IP address**

1. Create a direct network interface and attach it to the Amazon EC2 instance by running the following command\. You will need the MAC address of the device for the next step\.

   ```
   create-direct-network-interface [--endpoint endpoint] [--instance-id instanceId] [--mac macAddress]
                                   [--physical-network-interface-id physicalNetworkInterfaceId] 
                                   [--unlock-code unlockCode] [--vlan vlanId]
   ```

   OPTIONS

   ** \-\-endpoint <endpoint>** The endpoint to send this request to\. The endpoint for your devices will be a URL using the `https` scheme followed by an IP address\. For example, if the IP address for your device is 123\.0\.1\.2, the endpoint for your device would be https://123\.0\.1\.2\.

   ** \-\-instance\-id <instanceId>** The EC2 instance ID to attach the interface to \(optional\)\.

   ** \-\-mac <macAddress>** Sets the MAC address of the network interface \(optional\)\.

   **\-\-physical\-network\-interface\-id <physicalNetworkInterfaceId>** The ID for the physical network interface on which to create a new virtual network interface\. You can determine the physical network interfaces available on your Snowball Edge using the `describe-device` command\.

    **\-\-vlan <vlanId>** Set the assigned VLAN for the interface \(optional\)\. When specified, all traffic sent from the interface is tagged with the specified VLAN ID\. Incoming traffic is filtered for the specified VLAN ID, and has all VLAN tags stripped before being passed to the instance\.

1. If you didn't associate your DNI with an instance in step 1, you can associate it by running the [Updating a Direct Network Interface](using-client-commands.md#sbe-networking-update-dni) command\.

1. After you create a DNI and associate it with your EC2 instance, you must make two configuration changes inside your Amazon EC2 instance\. 
   + The first is to change ensure that packets meant for the VNI associated with the EC2 instance are sent through eth0\. 
   + The second change configures your direct network interface to use either DCHP or static IP when booting\. 

   The following are examples of shell scripts for Amazon Linux 2 and CentOS Linux that make these configuration changes\.

------
#### [ Amazon Linux 2 ]

   ```
   # Mac address of the direct network interface. 
   # You got this when you created the direct network interface.
   DNI_MAC=[MAC ADDRESS FROM CREATED DNI]
   
   # Configure routing so that packets meant for the VNI always are sent through eth0.
   PRIVATE_IP=$(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)
   PRIVATE_GATEWAY=$(ip route show to match 0/0 dev eth0 | awk '{print $3}')
   ROUTE_TABLE=10001
   echo "from $PRIVATE_IP table $ROUTE_TABLE" > /etc/sysconfig/network-scripts/rule-eth0
   echo "default via $PRIVATE_GATEWAY dev eth0 table $ROUTE_TABLE" > /etc/sysconfig/network-scripts/route-eth0
   echo "169.254.169.254 dev eth0" >> /etc/sysconfig/network-scripts/route-eth0
   
   # Query the persistent DNI name, assigned by udev via ec2net helper.
   #   changable in /etc/udev/rules.d/70-persistent-net.rules
   DNI=$(ip --oneline link | grep -i $DNI_MAC | awk -F ': ' '{ print $2 }')
   
   # Configure DNI to use DHCP on boot.
   cat << EOF > /etc/sysconfig/network-scripts/ifcfg-$DNI
   DEVICE="$DNI"
   NAME="$DNI"
   HWADDR=$DNI_MAC
   ONBOOT=yes
   NOZEROCONF=yes
   BOOTPROTO=dhcp
   TYPE=Ethernet
   MAINROUTETABLE=no
   EOF
   
   # Make all changes live.
   systemctl restart network
   ```

------
#### [ CentOS Linux ]

   ```
   # Mac address of the direct network interface. You got this when you created the direct network interface.
   DNI_MAC=[MAC ADDRESS FROM CREATED DNI]
   # The name to use for the direct network interface. You can pick any name that isn't already in use.
   DNI=eth1
   
   # Configure routing so that packets meant for the VNIC always are sent through eth0 
   PRIVATE_IP=$(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)
   PRIVATE_GATEWAY=$(ip route show to match 0/0 dev eth0 | awk '{print $3}')
   ROUTE_TABLE=10001
   echo from $PRIVATE_IP table $ROUTE_TABLE > /etc/sysconfig/network-scripts/rule-eth0
   echo default via $PRIVATE_GATEWAY dev eth0 table $ROUTE_TABLE > /etc/sysconfig/network-scripts/route-eth0
   
   # Configure your direct network interface to use DHCP on boot.
   cat << EOF > /etc/sysconfig/network-scripts/ifcfg-$DNI
   DEVICE="$DNI"
   NAME="$DNI"
   HWADDR="$DNI_MAC"
   ONBOOT=yes
   NOZEROCONF=yes
   BOOTPROTO=dhcp
   TYPE=Ethernet
   EOF
   
   # Rename DNI device if needed.
   CURRENT_DEVICE_NAME=$(LANG=C ip -o link | awk -F ': ' -vIGNORECASE=1 '!/link\/ieee802\.11/ && /'"$DNI_MAC"'/ { print $2 }')
   ip link set $CURRENT_DEVICE_NAME name $DNI
   
   # Make all changes live.
   systemctl restart network
   ```

------