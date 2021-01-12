# CloudFormation Template Deploy on AWS

## Source

Taken from [here](https://adamtheautomator.com/aws-cli-cloudformation/).

## Deploy

You need a configured AWS CLI on your machine to successfully deploy the static website.

Deploy the static website with:

```powershell
aws cloudformation deploy --template-file template.yaml --stack-name static-website
```

## Template

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: A simple CloudFormation template
Resources:
  Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: your-bucket-name # use your own unique name
      AccessControl: PublicRead
      WebsiteConfiguration:
        IndexDocument: index.html
Outputs:
  WebsiteURL:
    Value: !GetAtt [Bucket, WebsiteURL]
    Description: URL for website hosted on S3
```

First:

- `AWSTemplateFormatVersion` – determines the format version for the template so that AWS can interpret it correctly when deploying it.
- `Description` – contains a description of the template which will show in the AWS Console once you have deployed it.
- `Resources` – contains all of the infrastructure that you’re adding to the template. In this case, the resources will create a simple S3 bucket that will host a static site.

Moreover:

- `AccessControl` – sets the access rights to the S3 bucket to public read so that any user that visits the site can see the index.html file
- `WebsiteConfiguration` – configures the S3 bucket to act as a website that will serve the index.html file uploaded when users go to the bucket URL
- `Outputs` – can be different properties for resources that are part of the stack. In the example above, the WebsiteURL is the stack output. When you deploy the template again, you should see the website URL as an output in the AWS CloudFormation Console.
