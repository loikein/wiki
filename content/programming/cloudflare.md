---
title: "Cloudflare"
---
## Pages

While using [longern/FlareDrive](https://github.com/loikein/FlareDrive) \(link points to my fork with more detailed instructions\)[^flaredrive], I tried out Cloudflare Pages.

[^flaredrive]: The only problem with this project is that the contextual menu does not work at all on iOS devices.

### Authentication

Any custom domain needs to use Cloudflare as its DNS in order for it to be added as a self hosted application in Zero Trust.  
That means, you need to add the domain \(not subdomain, the whole domain\) to your Cloudflare websites, switch its DNS to Cloudflare \(instructions will be given\), and then jump back and forth between Pages \& Zero Trust dashboards a few times to setup the authentication policy. Not ideal.

> Make sure you export all your DNS settings from your previous DNS provider before pushing the confirm switch button! The Cloudflare DNS auto-migration process has dropped several subdomain settings of mine.
{.book-hint .danger}

### Binding your R2 bucket

Go to {{< menu `Project` `Settings` `Functions` `R2 bucket bindings` >}}, then add variable names and select buckets. Do not use Environment variables.


## R2

### Location hint

According to [docs](https://developers.cloudflare.com/r2/buckets/data-location/#current-limitations), currently, if you have set a location hint for bucket named `name`, then even if you delete it and create another bucket called `name`, it will still keep the previous location hint. This cannot be changed.


### PicGo S3 plugin

Reference: [S3 API compatibility · Cloudflare R2 docs](https://developers.cloudflare.com/r2/api/s3/api/)

**Generate access token**:

Go to {{< menu `R2 Overview` `Manage R2 API Tokens` `Create API token` >}}, choose `Write` permission, and then note down the Access Key ID and Secret Access Key.

**PicGo S3 settings**:

应用密钥 ID / accessKeyID
: \<Access Key ID\>

应用密钥 / secretAccessKey
: \<Secret Access Key\>

桶名 / bucketName
: \<Name of your bucket\>

文件路径 / uploadPath
: Customisable name, see [plugin docs](https://github.com/wayjam/picgo-plugin-s3#%E9%85%8D%E7%BD%AE-configuration). I have `{year}-{month}-{day}-{fullName}`.

地区 / region
: `auto`

自定义节点 / endpoint
: `https://<Account ID>.r2.cloudflarestorage.com`, the link in bucket page, minus the bucket name

自定义域名 / urlPrefix
: Link prefix you would like to copy. I have `https://<Random ID>.r2.dev` for now.


### uPic

ver 0.21.1, `AWSSDKSwiftCore.AWSReponseError error 1`. I suspect it is because there is no `auto` region in [uPic/uPic/Models/S3/S3Region.swift](https://github.com/gee1k/uPic/blob/master/uPic/Models/S3/S3Region.swift), but I do not speak Swift.


## Zero Trust

In order to use Zero Trust, you must fill out the payment method form \(even for the free tier\).
