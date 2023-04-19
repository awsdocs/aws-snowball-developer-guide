# Powering Off the Snowball Edge<a name="turnitoff"></a>

When you've finished transferring data on to the AWS Snowball Edge device, prepare it for its return trip to AWS\. Before you continue, make sure that all data transfer to the device has stopped\. If you were using the file interface to transfer data, disable it before you power off the device\. For more information, see [Disabling the File Interface](using-fileinterface.md#fileinterface-cleanup)\.

When all communication with the device has ended, turn it off by pressing the power button located above the LCD screen\. It takes about 20 seconds for the device to shut down\. While the device is shutting down, the LCD screen displays a message indicating the device is shutting down\.

![\[Shutdown message on LCD screen.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/shutdown-screen.png)

**Note**  
If the LCD screen is displaying the shutdown message when the device is not actually being shut down, press the **Restart display** button on the screen to return the screen to normal operation\.  

![\[Shutdown message on LCD screen with Restart display button near bottom center.\]](http://docs.aws.amazon.com/snowball/latest/developer-guide/images/shutdown-screen-restart.png)

After the device shuts down, the shipping information appears on the E Ink display\.

If you've powered off and unplugged your Snowball Edge device and the shipping information doesn't appear on the E Ink screen after about a minute, see [Troubleshooting problems returning Snow Family devices](troubleshooting.md#return-shipping-troubleshooting)\.

**Next:** [Returning the Snowball Edge Device](return-device.md) 