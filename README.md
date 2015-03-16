# S3 Directory Index

This script exploits the error document functionality of S3 static websites to create an Apache-style directory index of your bucket.


## Bucket Setup

1. Copy `list.html` into the S3 bucket where you want to serve a directory listing.
    - Edit `s3Params` to reflect the bucket name and appropriate S3 endpoint. ([reference](http://docs.aws.amazon.com/general/latest/gr/rande.html#s3_region))
    - Edit `ignoreList` to exclude any files from the directory index.


1. Grant `Everyone` List permissions.

1. Enable Static Website Hosting.
    - Set the Index Document to `index.html`.
    - Set the Error Document to `list.html`.
    - Note the endpoint.

1. Add the following CORS policy:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
    <CORSRule>
        <AllowedMethod>GET</AllowedMethod>
        <AllowedOrigin>http://{{ endpoint }}</AllowedOrigin>
    </CORSRule>
</CORSConfiguration>
```

## License

See [LICENSE](./LICENSE)

## Inspiration

Idea based on <https://github.com/rgrp/s3-bucket-listing> (which was itself based on <http://aws.amazon.com/code/Amazon-S3/1713>). Styles taken from the default [vsftpd](https://security.appspot.com/vsftpd.html) directory index template.
