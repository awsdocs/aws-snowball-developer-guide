# Setting the NTP time servers for your device<a name="setting-ntp"></a>

 Follow these steps to view and update which time servers your device must synchronize time with\.

**To check time sources**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Choose the device to open the device details page\.

1. You will see a list of time sources that your device is synchronizing time with in the **Time sources** table\.

   The **Time sources** table has four columns: 
   + **Address**: The DNS name / IP address of the time source
   + **State**: The current connection status between the device and that time source, there are 5 possible states:
     + **CURRENT**: Time source is currently being used to synchronize time
     + **COMBINED**: Time source is combined with the current source
     + **EXCLUDED**: Time source is excluded by the combining algorithm
     + **LOST**: Connection with the time source has been lost
     + **UNAVAILABILITY**: An invalid time source where the combining algorithm has deemed to be either a falseticker or has too much variability
   + **Type**: Network Time Protocol \(NTP\) sources can be a server or peer\. A server can be set by the user using the update\-time\-server command, whereas a peer can only be set up using other Snowball Edge devices in the cluster and are automatically set up when the cluster is associated\.
   + **Stratum**: The stratum of the source\. **Stratum 1** indicates a source with a locally attached reference clock\. A source that is synchronized to a Stratum 1 source is set at **Stratum 2**\. A source that is synchronized to a stratum 2 source is set at **Stratum 3**, and so on\.

**To update the time servers**

1. On the AWS OpsHub dashboard, find your device under **Devices**\. Choose the device to open the device details page\.

1. You will see a list of time sources that your device is synchronizing time with in the **Time sources** table\.

1. Choose **Update time servers** on the **Time sources** table\.

1. Provide the DNS name or the IP address of the time servers you would like your device to synchronize time with, and choose **Update**\.  
![\[Update time servers showing NTP time server IP address field and Update button.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/opshub-update-time-console.png)

**Supported NTP device types and software versions**  
NTP isn't available on any version 2 storage and compute device types\. Snowball Edge version 3 storage and compute device types with software version 77 or later support NTP, however\. To check if NTP is enabled, use the Snowball Edge CLI command `describe-time-sources`\.