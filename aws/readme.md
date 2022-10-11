# Setting up S3 bucket for hosting the MkDocs documantation site.

This document is about creating a public bucket to host the documents we use CloudFormation template.

Deploy the cloud formation using aws cli.
```bash
aws cloudformation create-stack --template-body file://help-site.yaml --stack-name Help-Site
```
Verify that the stack creation is successful. We only need to do this step once.

Deploying the site to S3:
https://learn.openwaterfoundation.org/owf-learn-mkdocs/deploy/#deploy-to-amazon-s3

