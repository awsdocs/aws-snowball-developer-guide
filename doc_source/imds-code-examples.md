# Examples of retrieving instance metadata using IMDSv1 and IMDSv2<a name="imds-code-examples"></a>

The following examples provide commands that you can use on a Linux instance\.

**Example of getting the available versions of the instance metadata**  
This example gets the available versions of the instance metadata\. Each version refers to an instance metadata build when new instance metadata categories were released\. The earlier versions are available to you in case you have scripts that rely on the structure and information present in a previous version\.  
IMDSv2  

```
    [ec2-user ~]$ TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` && curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/
    % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
    100    56  100    56    0     0   3733      0 --:--:-- --:--:-- --:--:--  3733
    *   Trying 169.254.169.254...
    * TCP_NODELAY set
    * Connected to 169.254.169.254 (169.254.169.254) port 80 (#0)
    > GET / HTTP/1.1
    > Host: 169.254.169.254
    > User-Agent: curl/7.61.1
    > Accept: */*
    > X-aws-ec2-metadata-token: MDAXcxNFLbAwJIYx8KzgNckcHTdxT4Tt69TzpKExlXKTULHIQnjEtXvD
    >
    * HTTP 1.0, assume close after body
    < HTTP/1.0 200 OK
    < Date: Mon, 12 Sep 2022 21:58:03 GMT
    < Content-Length: 274
    < Content-Type: text/plain
    < Server: EC2ws
    <
    1.0
    2007-01-19
    2007-03-01
    2007-08-29
    2007-10-10
    2007-12-15
    2008-02-01
    2008-09-01
    2009-04-04
    2011-01-01
    2011-05-01
    2012-01-12
    2014-02-25
    2014-11-05
    2015-10-20
    2016-04-19
    2016-06-30
    2016-09-02
    2018-03-28
    2018-08-17
    2018-09-24
    2019-10-01
    2020-10-27
    2021-01-03
    2021-03-23
    * Closing connection 0
```
IMDSv1  

```
    [ec2-user ~]$ curl http://169.254.169.254/
    1.0
    2007-01-19
    2007-03-01
    2007-08-29
    2007-10-10
    2007-12-15
    2008-02-01
    2008-09-01
    2009-04-04
    2011-01-01
    2011-05-01
    2012-01-12
    2014-02-25
    2014-11-05
    2015-10-20
    2016-04-19
    2016-06-30
    2016-09-02
    2018-03-28
    2018-08-17
    2018-09-24
    2019-10-01
    2020-10-27
    2021-01-03
    2021-03-23
    latest
```

**Example of getting the top‐level metadata items**  
This example gets the top‐level metadata items\. For information on top‐level metadata items, see [Supported Instance Metadata and User Data](https://docs.aws.amazon.com/snowball/latest/developer-guide/edge-compute-instance-metadata.html) in this guide\.  
IMDSv2  

```
    [ec2-user ~]$ TOKEN=`curl -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600"` \ && curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/ 
    ami-id
    hostname
    instance-id
    instance-type
    local-hostname
    local-ipv4
    mac
    network/
    reservation-id
    security-groups
```
IMDSv1  

```
    [ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/ 
    ami-id
    hostname
    instance-id
    instance-type
    local-hostname
    local-ipv4
    mac
    network/
    reservation-id
    security-groups
```

**Example of getting values of top‐level metadata**  
The following examples get the values of some of the top‐level metadata items that were obtained in the preceding example\. The IMDSv2 requests use the stored token that was created in the preceding example command, assuming it has not expired\.  
`ami‐id` IMDSv2  

```
    curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/ami-id \
    ami-0abcdef1234567890
```
`ami-id` IMDSv1  

```
    curl http://169.254.169.254/latest/meta-data/ami-id \
    ami-0abcdef1234567890
```
`reservation-id` IMDSv2  

```
    [ec2-user ~]$ curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/reservation-id \
    r-0efghijk987654321
```
`reservation-id` IMDSv1  

```
    [ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/reservation-id \
    r-0efghijk987654321
```
`local-hostname` IMDSv2  

```
    [ec2-user ~]$ curl -H "X-aws-ec2-metadata-token: $TOKEN" -v http://169.254.169.254/latest/meta-data/local-hostname \
    ip-00-000-00-00
```
`local-hostname` IMDSv1  

```
    [ec2-user ~]$ curl http://169.254.169.254/latest/meta-data/local-hostname \
    ip-00-000-00-00
```