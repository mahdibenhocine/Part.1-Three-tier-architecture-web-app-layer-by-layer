<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Website Delivery with CloudFront

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-cloudfront)

**Author:** Mahdi Ben  
**Email:** hocine.mohamed213@gmail.com

---

## Website Delivery with CloudFront

![Image](http://learn.nextwork.org/grateful_brown_glamorous_centaur/uploads/aws-networks-cloudfront_1dddddwe)

---

## Introducing Today's Project!

In this project, I’m setting up the foundation of a fast, globally distributed website and it all begins with the presentation layer of a three-tier architecture.

Here’s what I’m going to do:

- Create an S3 bucket to store my website’s files
- Set up CloudFront to distribute my site with low latency across the globe
- Manage permissions for both S3 and CloudFront to keep everything secure
- Compare different website hosting methods and evaluate their performance

This is Project 1 in a hands-on series focused on building a complete three-tier web application.

Here’s what’s coming up next:

Part 2 (Logic Tier): Build APIs using Lambda and API Gateway
Part 3 (Data Tier): Fetch and store data with AWS Lambda
Part 4: Combine all three layers into a complete three-tier web application


### Tools and concepts

Services I used were Amazon S3 for static website hosting and Amazon CloudFront for content delivery and caching. I also worked with IAM for permissions, S3 bucket policies, and public access settings.

Key concepts I learnt include:

- Content Delivery Network (CDN): How CloudFront distributes content through edge locations to reduce latency and improve load times globally.

- S3 Bucket Policies: How to control access to objects, including enabling public read access for website files.

- Static Website Hosting: Using S3 to host HTML, CSS, and JS files with a simple configuration.

- Public vs Private Access: Understanding when to allow open access and when to restrict it using CloudFront with Origin Access Control (OAC).

- Latency & Performance Optimization: How caching and edge distribution in CloudFront significantly improve website speed compared to direct S3 access.



### Project reflection

This project took me approximately 40 minutes to complete.

The most challenging part was understanding and configuring the correct S3 bucket policy and ensuring that Block Public Access settings didn’t conflict with my goal of making the site publicly available. It was also a bit tricky to distinguish between the permissions needed for S3 static hosting vs CloudFront access.

It was most rewarding to finally see the website load successfully in the browser and understand how CDNs like CloudFront enhance performance. Watching my configuration changes translate into a working, publicly accessible site gave me confidence in managing AWS services more independently.

I did this project today to gain hands-on experience with hosting and delivering static websites on AWS, and yes; it successfully met my goal of understanding how S3 and CloudFront work together to serve web content efficiently.

---

## Set Up S3 and Website Files

I started the project by creating an S3 bucket to host the front-end files. I can't use CloudFront for this task because it's not meant to host files, instead it uses S3 as a source to deliver them globally.

The three files that make up my website are index.html, which is the main page of the website; style.css it's styling, and script.js where the fun happens :) 

I validated that my website files work by opening the index.html in a browser while 3 of the files are in the same folder on my local machine.

![Image](http://learn.nextwork.org/grateful_brown_glamorous_centaur/uploads/aws-networks-cloudfront_qgo7wcd3)

---

## Exploring Amazon CloudFront

Amazon CloudFront is a content delivery network, which means it delivers websites, videos, and other content to users faster by using servers that are closer to them geographically.

Businesses and developers use CloudFront because it improves website speed, enhances security, and reduces load on their main servers.

To use Amazon CloudFront, you set up distributions, which are configurations that tell CloudFront where to find your content and how to deliver it to users.

I set up a distribution for delivering images and videos on my website to make them load faster for users around the world.

The origin is the source of the content in my case, an Amazon S3 bucket where the media files are stored.

My CloudFront distribution's default root object is `/index.html`. This means that when someone accesses my domain without specifying a file (like `example.com/`), CloudFront automatically serves the `index.html` file from the origin.

![Image](http://learn.nextwork.org/grateful_brown_glamorous_centaur/uploads/aws-networks-cloudfront_qgo7wcdt)

---

## Handling Access Issues

When I tried visiting my distributed website, I ran into an access denied error because CloudFront needs explicit permission to access the files in my bucket.

My distribution's origin access settings were set to Public.

This caused the Access Denied error because the S3 bucket still needs the correct bucket policy or object permissions to allow CloudFront to access the content.

To resolve the error, I set up origin access control (OAC). OAC is a special user for CloudFront that prevents this. An OAC lets you keep your S3 bucket and objects not publicly accessible, while still making sure they can be accessed through CloudFront.



![Image](http://learn.nextwork.org/grateful_brown_glamorous_centaur/uploads/aws-networks-cloudfront_egrhntyu)

---

## Updating S3 Permissions

Once I set up my OAC, I still needed to update my bucket policy because the bucket must explicitly allow access from the CloudFront origin access control identity, without this, CloudFront still can't retrieve the content, even with OAC in place.

Creating an OAC automatically gives me a policy I can copy, which grants CloudFront permission to access my S3 bucket on my behalf. This simplifies the setup and ensures only CloudFront can fetch content from the bucket not the public internet.

![Image](http://learn.nextwork.org/grateful_brown_glamorous_centaur/uploads/aws-networks-cloudfront_eg98ntyu)

---

## S3 vs CloudFront for Hosting

For my project extension, I'm comparing S3 Static Website Hosting and CloudFront. I initially had an error with static website hosting because the bucket permissions weren’t set correctly to allow public access. 

I tried resolving this by disabeling Block all public access, I still ran into an error because Public Read Bucket Policy is not properly set yet

I could finally see my S3 hosted website when I updated the S3 bucket policy. This worked because the Public Read Bucket Policy allowed anonymous users (everyone on the internet) to access the objects in my bucket via HTTP, which is essential for static website hosting on S3.

Compared to the permission settings for my CloudFront distribution, using S3 meant simpler and more direct access control. I preferred S3 for quick testing and public access because all I needed was to update the bucket policy to allow public reads, and my website was instantly accessible via the S3 static website endpoint.

---

## S3 vs CloudFront Load Times

Load time means the amount of time it takes for a web page or file (like HTML, CSS, JS, images) to be delivered to and rendered by the user's browser.

The load times for the CloudFront site were faster than the S3 site because CloudFront is a Content Delivery Network (CDN) , it caches your content at edge locations that are geographically closer to your users. This reduces latency and minimizes the round-trip time between the client and the origin (S3 bucket).

A business would prefer CloudFront when performance, security, and scalability are key priorities. CloudFront is ideal when. S3 static website hosting might be sufficient when the use case is simpler, such as: Hosting a basic site for internal use, a portfolio, documentation, or a temporary landing page.

![Image](http://learn.nextwork.org/grateful_brown_glamorous_centaur/uploads/aws-networks-cloudfront_12verpuh)

---

---
