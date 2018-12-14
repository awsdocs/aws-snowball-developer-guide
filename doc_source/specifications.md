--------

This guide is for the Snowball Edge\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](https://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# AWS Snowball Edge Specifications<a name="specifications"></a>

Find hardware specifications for Snowball Edge Storage Optimized devices in the following table\. 


| Item | Specification | 
| --- | --- | 
| Storage capacity | Snowball Edge devices have up to 80 TB of usable space\. | 
| Data and network connections | Network connections:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/specifications.html)  | 
| Cables | Each AWS Snowball Edge device ships country\-specific power cables\. No other cables or optics are provided\. | 
| Thermal requirements | AWS Snowball Edge devices are designed for office operations, and are ideal for data center operations\. | 
| Decibel output | On average, an AWS Snowball Edge device produces 68 decibels of sound, typically quieter than a vacuum cleaner or living\-room music\. | 
| Weight | 49\.5 pounds \(22\.45 Kg\) | 
| Height | 15\.25 inches \(386 mm\) | 
| Width | 10\.6 inches \(269 mm\) | 
| Length | 26\.00 inches \(671 mm\) | 
| Power | In AWS Regions in the US: NEMA 5–15p 100–220 volts\. In all AWS Regions, a power cable is included\. | 
| Power consumption | 400 watts | 
| Voltage | 100 – 240V AC | 
| Frequency | 47/63 Hz | 
| Temperature range | 0 – 40°C \(operational\) | 
| Nonoperational vibration | ASTM D4169 Truck Level I 0\.73 GRMS | 
| Nonoperational shock | Drop test \(12 inches all sides \+ 24 inches one side\) | 
| Nonoperational altitude | 0–12,000 meters | 
| Operational altitude | 0–3,000 meters \(0–10,000 feet\) | 

Find hardware specifications for Snowball Edge Compute Optimized devices in the following table\.


| Item | Specification | 
| --- | --- | 
| Storage capacity | 42 TB of usable space plus 7\.68 TB of dedicated NVMe SSD storage for instances\. | 
| Data and network connections |  Network connections:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/specifications.html)  | 
| Cables | Each AWS Snowball Edge device ships country\-specific power cables\. No other cables or optics are provided\. | 
| Thermal requirements | AWS Snowball Edge devices are designed for office operations, and are ideal for data center operations\. | 
| Decibel output | On average, an AWS Snowball Edge device produces 68 decibels of sound, typically quieter than a vacuum cleaner or living\-room music\. | 
| Weight | 49\.7 pounds \(22\.54 Kg\) | 
| Height | 15\.5 inches \(394 mm\) | 
| Width | 10\.6 inches \(265 mm\) | 
| Length | 28\.3 inches \(718 mm\) | 
| Power | In AWS Regions in the US: NEMA 5–15p 100–220 volts\. In all AWS Regions, a power cable is included\. | 
| Power consumption | 304 watts for an average use case, though the power supply is rated for 1200 watts\. | 
| Voltage | 100 – 240V AC | 
| Frequency | 47/63 Hz | 
| Temperature range | 0 – 40°C \(operational\) | 
| Nonoperational vibration | ASTM D4169 Truck level I 0\.73 GRMS | 
| Nonoperational shock | Drop test \(12 inches all sides \+ 24 inches one side\) | 
| Nonoperational altitude | 0 – 12,000 meters | 
| Operational altitude | 0–3,000 meters \(0–10,000 feet\) | 

## Supported Network Hardware<a name="network-hardware"></a>

To use the AWS Snowball Edge device, you need your own network cables\. For RJ45 cables, there are no specific recommendations\. SFP\+ and QSFP\+ cables and modules from Mellanox and Finisar have been verified to be compatible with the device\.

After you open the back panel of the AWS Snowball Edge device, you see the network ports shown in the following photograph\.

![\[The available network ports\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/snowball-edge-back-connectors.png)

These ports support the following network hardware\.

**SFP**  
This port provides a 10G/25G SFP28 interface compatible with SFP28 and SFP\+ transceiver modules and direct\-attach copper \(DAC\) cables\. You need to provide your own transceivers or DAC cables\.
+ For 10G operation, you can use any SFP\+ option\. Examples include:
  + 10Gbase\-LR \(single mode fiber\) transceiver
  + 10Gbase\-SR \(multi\-mode fiber\) transceiver
  + SFP\+ DAC cable
+ For 25G operation, you can use any SFP28 option\. Examples include:
  + 25Gbase\-LR \(single mode fiber\) transceiver
  + 25Gbase\-SR \(multi\-mode fiber\) transceiver
  + SFP28 DAC cable

![\[SFP+ Copper\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/sfp.png)

**QSFP**  
This port provides a 40G QSFP\+ interface on storage optimized devices and a 40/50/100G QSFP\+ interface on compute optimized devices\. Both are compatible with QSFP\+ transceiver modules and DAC cables\. You need to provide your own transceivers or DAC cables\. Examples include the following:
+ 40Gbase\-LR4 \(single mode fiber\) transceiver
+ 40Gbase\-SR4 \(multi\-mode fiber\) transceiver
+ QSFP\+ DAC

![\[QSFP+\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/qsfp.png)

**RJ45**  
This port provides 1Gbase\-TX/10Gbase\-TX operation\. It is connected via UTP cable terminated with a RJ45 connector\. Compute optimized devices have two RJ45 ports\.

1G operation is indicated by a blinking amber light\. 1G operation is not recommended for large\-scale data transfers to the Snowball Edge device, as it dramatically increases the time it takes to transfer data\.

10G operation is indicated by a blinking green light\. It requires a Cat6A UTP cable with a maximum operating distance of 180 feet \(55 meters\)\.

![\[RJ45\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/rj45.png)

## Network Converter for a Second Connection to the Snowball Edge Storage Optimized<a name="network-other-hardware"></a>

Compute optimized devices have two RJ45 10G BASE\-T ports\. However, for applications requiring a second 10G BASE\-T connection to a Snowball Edge storage optimized, you can install an SFP\+ to 10G BASE\-T media converter module in the SFP\+ port\. 

AWS has qualified the ProLabs model SFP\-10G\-T\-NC media converter for this purpose\. You can purchase this converter from Anixter, Graybar, and other distributors\.

![\[ProLabs model SFP-10G-T-NC media converter\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/ProLabs-model-SFP-10G-T-NC.png)

The following procedure outlines how to set up this media converter for use with a Snowball Edge\.

**To set up the media converter for use with a Snowball Edge**

1. Insert the module into the SFP\+ port\.

1. Connect a Cat6A cable to the Snowball Edge and to your network\.

1. Restart the power for the Snowball Edge\.

**Important**  
Remove the media converter before returning your Snowball Edge to AWS\.