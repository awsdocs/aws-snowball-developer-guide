# Limitations on Transferring On\-Premises Data with a Snowball Edge Device<a name="transfer-limits"></a>

The following limitations exist for transferring data to or from an AWS Snowball Edge device on\-premises:
+ Files must be in a static state while being written\. Files that are modified while being transferred are not imported into Amazon S3\.
+ Jumbo frames are not supported—that is, Ethernet frames with more than 1500 bytes of payload\.
+ When selecting what data to export, keep in mind that objects with trailing slashes in their names \(`/` or `\`\) are not transferred\. Before exporting any objects with trailing slashes, update their names to remove the slash\.
+ When using multipart data transfer, the maximum part size is 512 megabytes \(MB\)\.