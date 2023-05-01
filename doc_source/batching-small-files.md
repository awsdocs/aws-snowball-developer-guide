# Batching small files<a name="batching-small-files"></a>

Each copy operation has some overhead because of encryption\. To speed up the process of transferring small files to your AWS Snowball Edge device, you can batch them together in a single archive\. When you batch files together, they can be auto\-extracted when they are imported into Amazon S3, if they were batched in one of the supported archive formats\.

Typically, files that are 1 MB or smaller should be included in batches\. There's no hard limit on the number of files you can have in a batch, though we recommend that you limit your batches to about 10,000 files\. Having more than 100,000 files in a batch can affect how quickly those files import into Amazon S3 after you return the device\. We recommend that the total size of each batch be no larger than 100 GB\.

Batching files is a manual process, which you manage\. After you batch your files, transfer them to a Snowball Edge device using the AWS CLI `cp` command with the `--metadata snowball-auto-extract=true` option\. Specifying `snowball-auto-extract=true` automatically extracts the contents of the archived files when the data is imported into Amazon S3, so long as the size of the batched file is no larger than 100 GB\.

**Note**  
Any batches larger than 100 GB are not extracted when they are imported into Amazon S3\.

**To batch small files**

1. Decide on what format you want to batch your small files in\. The auto\-extract feature supports the `TAR`, `ZIP`, and `tar.gz` formats\.

1. Identify which small files you want to batch together, including their size and the total number of files that you want to batch together\.

1. Batch your files on the command line as shown in the following examples\.
   + For Linux, you can batch the files in the same command line used to transfer your files to the device\. 

     ```
     tar -cf - /Logs/April | aws s3 cp - s3://mybucket/batch01.tar --metadata snowball-auto-extract=true --endpoint http://192.0.2.0:8080
     ```
**Note**  
Alternatively, you can use the archive utility of your choice to batch the files into one or more large archives\. However, this approach requires extra local storage to save the archives before you transfer them to the Snowball\.
   + For Windows, use the following example command to batch the files when all files are in the same directory from which the command is run:

     ```
     7z a -tzip -so "test" | aws s3 cp - s3://mybucket/batch01.zip --metadata snowball-auto-extract=true --endpoint http://192.0.2.0:8080
     ```

     To batch files from a different directory from which the command is run, use the following example command:

     ```
     7z a -tzip -so "test" "c:\temp" | aws s3 cp - s3://mybucket/batch01.zip --metadata snowball-auto-extract=true --endpoint http://10.x.x.x:8080
     ```
**Note**  
For Microsoft Windows 2016, tar is not available, but you can download it from the *Tar for Windows* website\.  
You can download 7 ZIP from the   7ZIP website\.

1. Repeat until you've archived all the small files that you want to transfer to Amazon S3 using a Snowball Edge\.

1. Transfer the archived files to the Snowball\. If you want the data to be auto\-extracted, and you used one of the supported archive formats mentioned previously in step 1, use the AWS CLI `cp` command with the `--metadata snowball-auto-extract=true` option\.
**Note**  
If there are non\-archive files, don't use this command\.

When creating the archive files, the extraction will maintain the current data structure\. This means if you create an archive file that contains files and folders, Snowball Edge will recreate this during the ingestion to Amazon S3 process\.

The archive file will be extracted in the same directory it is stored in and the folder structures will be built out accordingly\. Keep in mind that when copying archive files, it is important to set the flag `--metadata snowball-auto-extract=true`\. Otherwise, Snowball Edge will not extract the data when it's imported into Amazon S3\.

Using the example in step 3, if you have the folder structure of /Logs/April/ that contains files `a.txt`, `b.txt` and `c.txt`\. If this archive file was placed in the root of /mybucket/ then the data would look like the following after the extraction:

```
/mybucket/Logs/April/a.txt
/mybucket/Logs/April/b.txt
/mybucket/Logs/April/c.txt
```



If the archive file was placed into /mybucket/Test/, then the extraction would look as like the following:

```
/mybucket/Test/Logs/April/a.txt
/mybucket/Test/Logs/April/b.txt
/mybucket/Test/Logs/April/c.txt
```