# Creating a Static Website Using Amazon S3
## Introduction
In this AWS hands-on lab, we will create and configure a simple static website hosted in S3.  This demonstrates how to create a cost-efficient website hosting for sites that consist of files like HTML, CSS, JavaScript, fonts, and images.

## Instructions
1. Create S3 Bucket
   * Navigate to S3 and create a bucket (remember to use a unique name).
   * In the Bucket settings for Block Public Access section, un-check Block all public access.  Ensure all four permissions restrictions beneath it are also un-checked.  Check the box to acknowledge that turning off all public access might result in the bucket and its objects becoming public.  
   * Create the bucket.
2. Upload Your Files
   * Select the bucket you just created and add the files (`index.html` and `error.html`)
   * Upload them  
3. Enable Static Website Hosting for the S3 Bucket
   * When viewing your bucket, select the Properties tab and scroll to the bottom of the screen to find the Static website hosting section.
   * Click Edit, then set the following values:
   
      ```
      Static website hosting: Enable
      Hosting type: Host a static website
      Index document: index.html
      Error document: error.html
      ```
      
    * Save the changes.
 4. Edit Bucket Policy
    * Without this policy, you'll see a 403 Forbidden error message when atempting to view the listed endpoint URL under the Static website hosting section.
    * Back in S3, click the Permissions tab and click Edit in the Bucket policy section.
    * In the Policy box, enter the following JSON statement (replacing <BUCKET_ARN> with the bucket ARN provided _right above_ the Policy box):

      ```
      {
        "Version":"2012-10-17",
        "Statement":[{
           "Sid":"PublicReadGetObject",
           "Effect":"Allow",
           "Principal": "*",
           "Action":["s3:GetObject"],
           "Resource":["<BUCKET_ARN>/*"]
         }]
       }
      ```
      
      _Note: Ensure the trailing /* is present so the policy applies to all objects within the bucket_
      
    * Click Save changes.
5.  View Your Website
   * The listed endpoint URL within the Static website hosting section of the Bucket Properties tab will be what you use to access your static site.
   * `index.html` will be your homepage and you can view the `error.html` file if you navigate to a URL that's invalid... like `<endpoint URL>/<some fake page>`
