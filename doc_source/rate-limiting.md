# Rate Limits on AWS Snowball Edge<a name="rate-limiting"></a>

The Rate Limiter is used to control the rate of requests in a server cluster environment\.

## Amazon Snow S3 Adapter Connection Limit<a name="connection-limit"></a>

The maximum connection limit is 1000 for Snowball Edge on Amazon S3\. Any connections beyond 1000 are dropped\.