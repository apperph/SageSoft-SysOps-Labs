## Overview:

This lab will demonstrate how a resource-based IAM policy works.
We will use an S3 bucket policy to allow and deny permissions to the objects inside the bucket.


## 0  Prerequisite:

0-a Create an IAM User and put it in the Group1 IAM Group. 

You can choose to create a custom password or autogenerated password. You can also uncheck the "users must create a new password at sign-in" but it is recommended specially in real-life use cases to leave it on so the user can create their own password for account privacy.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-0a.png)

0-b Once IAM user is created, copy the IAM user ARN since we are going to use this later on the lab. Paste it on a text editor or notes on your local machine.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-0b.png)

0-c Create an S3 bucket.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-1.png)

Once you have created your S3 bucket, follow the steps below.

## 1. Configure S3 Bucket Policy

1-a.  Create 2 folders inside the S3 buckets named:
accessible
not-accessible

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-2.png)

Then upload any file or document on both of the folders, you can upload even an empty text file.



1-b. Right now you have full access to the S3 bucket as the IAM group where your IAM user belongs allows S3 access.

We will change the S3 permissions with an S3 bucket policy which is an IAM resourced based policy, navigate to the permission tab on the S3 console.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-3.png)

Scroll down, and click on edit bucket policy.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-4.png)



1-c. Copy this policy: 

```
{
"Id": "demo-policy",
"Version": "2012-10-17",
"Statement": [
    {
"Sid": "accessible",
"Action": [
"s3:Get*",
"s3:List*"
      ],
"Effect": "Allow",
"Resource": [
"arn:aws:s3:::<S3 BUCKET NAME>/accessible",
"arn:aws:s3:::<S3 BUCKET NAME>/accessible/*"
                   ],
"Principal": {
"AWS": [
"<YOUR IAM USER ARN>"
        ]
      }
    },
    {
"Sid": "not-accessible",
"Action": [
"s3:Get*",
"s3:List*"
      ],
"Effect": "Deny",
"Resource": [
"arn:aws:s3:::<S3 BUCKET NAME>/not-accessible",
"arn:aws:s3:::<S3 BUCKET NAME>/not-accessible/*"
                   ],
"Principal": {
"AWS": [
"<YOUR IAM USER ARN>"
        ]
      }
    }
  ]
}
```

Modify the <S3 BUCKET NAME> and <YOUR IAM USER ARN> and paste it to the S3 bucket policy.

Examine the policy, it will provide Get and List access to the folder named accessible and deny access for the not-accessible folder.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-5.png)

Click save changes.



## 2. Checking the bucket folders.

2-a Log in using the IAM user account and go to s3.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-6a.png)


2-b. Check permissions on the accessible folder by clicking on a file stored inside it.

Check the permissions tab and you’ll be able to see it.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-6.png)

2-c. Check the permission on the not-accessible folder by clicking on a file stored inside it.

Now it says you don’t have permission.

![](https://sb-next-prod-image-bucket.s3.ap-southeast-1.amazonaws.com/public/CAMP/Session3/Lab13/image13-7.png)

Well done!

This also demonstrates the evaluation policy of IAM, even though you have access to S3, if there is a deny rule, the deny rule will always take over an allow rule.


Please copy and paste the JSON in the textbox on the left side and supply the necessary information.



```
{
 "s3_bucket-arn":"",
 "iam_user_arn": ""
}
```

**Note: You can now delete the resources you created for this lab.**

