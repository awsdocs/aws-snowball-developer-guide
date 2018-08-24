--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# Snowball Client commands for Compute Instances<a name="using-ec2-edge-client"></a>

The Snowball client is a standalone terminal application that you run on your local server to perform some administrative tasks on your device or cluster of devices\. For more information on how to use it, including how to start and stop services with the Snowball client, see [Using the Snowball Client](using-client.md)\.

The following Snowball client commands are specific to compute instances\.

## Creating a Virtual Network Interface<a name="ec2-edge-create-vnic"></a>

To run a compute instance on your Snowball Edge or start the file interface, on your Snowball Edge, you first create a virtual network interface \(VNIC\)\. Each Snowball Edge has three network interfaces \(NICs\), the physical network interface controllers for the device\. These are the RJ45, SFP, and QSFP ports on the back of the device\.

Each VNIC is based on the physical one, and you can have any number of VNICs associated with each NIC\. To create a virtual network interface, use the `snowballEdge create-virtual-network-interface` command\. 

**Note**  
`--static-ip-address-configuration` is only a valid option when using `STATIC` for `--ip-address-assignment`\.

**Usage \(configured Snowball client\)**

```
snowballEdge create-virtual-network-interface --ip-address-assignment [DHCP or STATIC] --physical-network-interface-id [physical network interface id] --static-ip-address-configuration IpAddress=[IP address],NetMask=[Netmask]
```

**Usage \(Snowball client not configured\)**

```
snowballEdge create-virtual-network-interface --endpoint https://[ip address] --manifest-file /path/to/manifest --unlock-code [unlock code] --ip-address-assignment [DHCP or STATIC] --physical-network-interface-id [physical network interface id] --static-ip-address-configuration IpAddress=[IP address],NetMask=[Netmask]
```

**Example Creating VNICs \(DHCP\)**  

```
./snowballEdge create-virtual-network-interface --ip-address-assignment dhcp --physical-network-interface-id s.ni-8EXAMPLEaEXAMPLEd
{
  "VirtualNetworkInterface" : {
    "VirtualNetworkInterfaceArn" : "arn:aws:snowball-device:::interface/s.ni-8EXAMPLE8EXAMPLEf",
    "PhysicalNetworkInterfaceId" : "s.ni-8EXAMPLEaEXAMPLEd",
    "IpAddressAssignment" : "DHCP",
    "IpAddress" : "192.0.2.0",
    "Netmask" : "255.255.255.0",
    "DefaultGateway" : "192.0.2.1",
    "MacAddress" : "EX:AM:PL:E1:23:45"
  }
}
```

## Describing Your Virtual Network Interfaces<a name="ec2-edge-describe-vnic"></a>

To describe the VNICs you previously created on your device, you can use the `snowballEdge describe-virtual-network-interfaces` command\.

**Usage \(configured Snowball client\)**

```
snowballEdge describe-virtual-network-interfaces
```

**Usage \(Snowball client not configured\)**

```
snowballEdge describe-virtual-network-interfaces --endpoint https://[ip address] --manifest-file /path/to/manifest --unlock-code [unlock code]
```

**Example Describing VNICs**  

```
./snowballEdge describe-virtual-network-interfaces
[
  {
    "VirtualNetworkInterfaceArn" : "arn:aws:snowball-device:::interface/s.ni-8EXAMPLE8EXAMPLE8",
    "PhysicalNetworkInterfaceId" : "s.ni-8EXAMPLEaEXAMPLEd",
    "IpAddressAssignment" : "DHCP",
    "IpAddress" : "192.0.2.0",
    "Netmask" : "255.255.255.0",
    "DefaultGateway" : "192.0.2.1",
    "MacAddress" : "EX:AM:PL:E1:23:45"
  },{
    "VirtualNetworkInterfaceArn" : "arn:aws:snowball-device:::interface/s.ni-1EXAMPLE1EXAMPLE1",
    "PhysicalNetworkInterfaceId" : "s.ni-8EXAMPLEaEXAMPLEd",
    "IpAddressAssignment" : "DHCP",
    "IpAddress" : "192.0.2.2",
    "Netmask" : "255.255.255.0",
    "DefaultGateway" : "192.0.2.1",
    "MacAddress" : "12:34:5E:XA:MP:LE"
  }  
]
```

## Updating a Virtual Network Interface<a name="ec2-edge-update-vnic"></a>

After creating a virtual network interface, you can update its configuration using the `snowballEdge update-virtual-network-interface` command\. After providing the ARN for the VNIC, you only need to provide the value for whatever elements you are updating\.

**Usage \(configured Snowball client\)**

```
snowballEdge update-virtual-network-interface --virtual-network-interface-arn [virtual network-interface-arn] --ip-address-assignment [DHCP or STATIC] --physical-network-interface-id [physical network interface id] --static-ip-address-configuration IpAddress=[IP address],NetMask=[Netmask]
```

**Usage \(Snowball client not configured\)**

```
snowballEdge update-virtual-network-interface --endpoint https://[ip address] --manifest-file /path/to/manifest --unlock-code [unlock code] --virtual-network-interface-arn [virtual network-interface-arn] --ip-address-assignment [DHCP or STATIC] --physical-network-interface-id [physical network interface id] --static-ip-address-configuration IpAddress=[IP address],NetMask=[Netmask]
```

**Example Updating a VNIC \(DHCP\)**  

```
./snowballEdge update-virtual-network-interface --virtual-network-interface-arn arn:aws:snowball-device:::interface/s.ni-8EXAMPLEbEXAMPLEd --ip-address-assignment dhcp
```

## Deleting a Virtual Network Interface<a name="ec2-edge-delete-vnic"></a>

To delete a virtual network interface, you can use the` snowballEdge delete-virtual-network-interface` command\. The Amazon S3 and Amazon EC2 services may not be started using the start\-service command\. Services can only be bound to a single virtual network interface\.

**Usage \(configured Snowball client\)**

```
snowballEdge delete-virtual-network-interface --virtual-network-interface-arn [virtual network-interface-arn]
```

**Usage \(Snowball client not configured\)**

```
snowballEdge delete-virtual-network-interface --endpoint https://[ip address] --manifest-file /path/to/manifest --unlock-code [unlock code] --virtual-network-interface-arn [virtual network-interface-arn]
```

**Example Deleting a VNIC**  

```
./snowballEdge delete-virtual-network-interface --virtual-network-interface-arn arn:aws:snowball-device:::interface/s.ni-8EXAMPLEbEXAMPLEd
```