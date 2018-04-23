--------

This guide is for the Snowball Edge \(100 TB of storage space\)\. If you are looking for documentation for the Snowball, see the [AWS Snowball User Guide](http://docs.aws.amazon.com/snowball/latest/ug/whatissnowball.html)\.

--------

# AWS Snowball Edge Specifications<a name="specifications"></a>

The following table outlines hardware specifications for the AWS Snowball Edge appliance\.


| Item | Specification | 
| --- | --- | 
| Storage capacity | 100 TB Snowballs have about 82 TB of usable space\. | 
| Data and network connections | Network connections:  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/specifications.html) To use the AWS Snowball Edge appliance, you need your own network cables\. For RJ45 cables, there are no specific recommendations\. SFP\+ and QSFP\+ cables and modules from Mellanox and Finisar have been verified to be compatible with the appliance\.  | 
| Cables | Each AWS Snowball Edge appliance ships country\-specific power cables\. No other cables or optics are not provided\. | 
| Thermal requirements | AWS Snowball Edge appliances are designed for office operations, and are ideal for data center operations\. | 
| Decibel output | On average, an AWS Snowball Edge appliance produces 68 decibels of sound, typically quieter than a vacuum cleaner or living\-room music\. | 
| Weight | 49\.5 pounds \(22\.6 Kg\) | 
| Height | 15\.25 inches \(386 mm\) | 
| Width | 10\.375 inches \(259 mm\) | 
| Length | 26\.00 inches \(671 mm\) | 
| Power | In the US regions: NEMA 5–15p 100–220 volts\. In all regions, a power cable is included\. | 
| Power consumption | 400 watts | 
| Voltage | 100 – 240V AC | 
| Frequency | 47/63 Hz | 
| Power conversion efficiency | 89 – 92% at 25C, 230Vac | 
| Temperature range | 0 – 40°C \(operational\) | 
| Non\-Operational Vibration | ASTM D4169 Truck Level I 0\.73 GRMS | 
| Non\-Operational Shock | Drop Test \(12” all sides \+ 24” 1 side\) | 
| Non\-operational Altitude | 0 – 12,000 meters | 
| Operational Altitude | 0 to 3,000m \(0 to 10,000’\) | 

## Supported Network Hardware<a name="network-hardware"></a>

After you open the back panel of the AWS Snowball Edge appliance, you'll see the network ports shown in the following photograph\.

![\[The available network ports.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/snowball-edge-back-connectors.png)

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
This port provides a 40G QSFP\+ interface compatible with QSFP\+ transceiver modules and DAC cables\. You need to provide your own transceivers or DAC cables\. Examples include the following:
+ 40Gbase\-LR4 \(single mode fiber\) transceiver
+ 40Gbase\-SR4 \(multi\-mode fiber\) transceiver
+ QSFP\+ DAC

![\[QSFP+\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/qsfp.png)

**RJ45**  
This port provides 1Gbase\-TX/10Gbase\-TX operation\. It is connected via UTP cable terminated with a RJ45 connector\.

1G operation is indicated by a blinking amber light\. 1G operation is not recommended for large\-scale data transfers to the Snowball Edge device, as it dramatically increases the time it takes to transfer data\.

10G operation is indicated by a blinking green light\. It requires a Cat6A UTP cable with a maximum operating distance of 180 feet \(55 meters\)\.

![\[RJ45\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/rj45.png)

## Network Converter for a Second Connection to the Snowball Edge<a name="network-other-hardware"></a>

For applications requiring a second 10G BASE\-T connection to the Snowball Edge, you can install an SFP\+ to 10G BASE\-T media converter module in the SFP\+ port\. 

AWS has qualified the ProLabs model SFP\-10G\-T\-NC media converter for this purpose\. You can purchase this converter from Anixter, Graybar, and other distributors\.

![\[ProLabs model SFP-10G-T-NC media converter\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/ProLabs-model-SFP-10G-T-NC.png)

The following procedure outlines how to set up this media converter for use with a Snowball Edge\.

**To set up the media converter for use with a Snowball Edge**

1. Insert the module into the SFP\+ port\.

1. Connect a Cat6A cable to the Snowball Edge and to your network\.

1. Restart the power for the Snowball Edge\.

**Important**  
Remove the media converter before returning your Snowball Edge to AWS\.