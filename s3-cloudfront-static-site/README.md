# AWS Project: Serverless Static Website (S3 + CloudFront CDN)

## Project Overview

Designed and deployed a serverless static website using Amazon S3 for content storage and Amazon CloudFront as a global Content Delivery Network (CDN).

The project explored how AWS managed services can deliver static web content without requiring traditional server administration. It also provided hands-on experience with configuring cloud resources, connecting an S3 origin to CloudFront, and enforcing HTTPS for client-facing traffic.

**Project Status:** Completed — Original AWS deployment no longer active.

## Project Objectives

- Host a static website using Amazon S3.
- Configure Amazon CloudFront to distribute website content through its global edge network.
- Redirect incoming HTTP requests to HTTPS at the CloudFront distribution.
- Understand the relationship between origin storage, content caching, and client-facing content delivery.
- Gain practical experience configuring AWS services through a serverless architecture.

## Technologies Used

| Technology | Purpose |
|---|---|
| Amazon S3 | Static website hosting and origin storage |
| Amazon CloudFront | Content delivery network and edge caching |
| HTTPS / TLS | Encryption between visitors and CloudFront |
| Git & GitHub | Project documentation and version control |

## Architecture

The deployment followed this request flow:

```text
             Website Visitor
                    |
                    | HTTPS
                    v
          Amazon CloudFront
          (Global CDN / Cache)
                    |
                    | HTTP
                    v
           Amazon S3 Bucket
          (Static Website Origin)
                    |
                    v
          HTML / CSS / Assets
```

Amazon S3 served as the origin for the static website. The CloudFront distribution was configured to use the S3 static website endpoint as a custom origin.

When visitors requested website content, CloudFront could serve cached objects from an edge location or retrieve content from the S3 origin when necessary.

The CloudFront Viewer Protocol Policy was configured to redirect HTTP requests to HTTPS.

**Architecture Limitation:** Because this implementation used an S3 static website endpoint, communication between CloudFront and the S3 origin used HTTP. HTTPS was enforced between the visitor and CloudFront, not across the entire request path.

A potential future improvement would be to configure a private S3 REST endpoint with CloudFront Origin Access Control (OAC), allowing restricted access to the bucket and HTTPS communication between CloudFront and S3.

## Implementation

### 1. Amazon S3 Configuration

- Created an S3 bucket to store static website files.
- Enabled static website hosting.
- Configured the bucket's website endpoint for use as the CloudFront origin.
- Used Amazon S3 to serve static website content without maintaining a traditional web server.

### 2. Amazon CloudFront Configuration

- Created a CloudFront distribution.
- Configured the distribution to reference the S3 website endpoint as its origin.
- Used CloudFront's edge caching capabilities for content delivery.
- Configured the Viewer Protocol Policy to **Redirect HTTP to HTTPS**.

### 3. HTTPS Configuration

Configured CloudFront to redirect client HTTP requests to HTTPS, helping protect traffic between visitors and the CDN.

This setting applied to viewer connections. Because the origin was an S3 website endpoint, the origin connection itself was not encrypted with HTTPS.

## Original Deployment Information

The project was originally deployed using the following AWS endpoints:

**CloudFront Distribution:**
`dilvtue9whwoc.cloudfront.net`

**Amazon S3 Website Endpoint:**
`http://abdullah-cloudfront-site.s3-website-us-east-1.amazonaws.com`

**Deployment Status:** Archived / No Longer Active

The original AWS account and its associated resources are no longer available. These addresses are retained for historical documentation and are not presented as functioning live demos.

## Technical Concepts Demonstrated

### Serverless Hosting

Used Amazon S3 to host static website assets without provisioning or administering a traditional application server.

### Content Delivery Networks

Configured Amazon CloudFront to distribute static website content through its CDN architecture.

CloudFront can cache objects at edge locations, reducing repeated requests to the origin and potentially improving content delivery performance.

### HTTP and HTTPS

Configured CloudFront to redirect HTTP viewer requests to HTTPS.

This demonstrated the distinction between securing client-facing connections and securing connections between a CDN and its origin.

### Origin Configuration

Connected a CloudFront distribution to an Amazon S3 static website endpoint, gaining practical familiarity with how cloud storage and content delivery services interact.

## Lessons Learned

Through this project, I gained experience with:

- Configuring Amazon S3 for static website hosting.
- Creating and configuring an Amazon CloudFront distribution.
- Understanding how an origin server and CDN work together.
- Applying viewer protocol policies to redirect HTTP traffic to HTTPS.
- Recognizing architectural security limitations associated with public S3 website endpoints.
- Understanding the distinction between a functional cloud deployment and a production-hardened architecture.

The project strengthened my foundational understanding of cloud infrastructure and AWS content delivery services.

## Limitations and Future Improvements

This implementation was intended as an introductory AWS learning project rather than a production-ready deployment.

Potential improvements include:

- **Private S3 Origin:** Use CloudFront Origin Access Control (OAC) to restrict direct access to S3 content.
- **Origin Encryption:** Replace the S3 website endpoint with an S3 REST endpoint that supports HTTPS origin connections.
- **Infrastructure as Code:** Use AWS CloudFormation or Terraform to define and reproduce the deployment configuration.
- **Monitoring:** Integrate Amazon CloudWatch for distribution monitoring and operational visibility.
- **Deployment Automation:** Create a GitHub Actions workflow for repeatable website updates and deployments.

These enhancements were not part of the original implementation.

## Project Status and Documentation

This repository documents a previously completed AWS learning project.

The original AWS environment has been decommissioned, so the deployment cannot currently be accessed or independently tested through its former endpoints.

The documentation preserves the project's architecture, configuration approach, and technical lessons learned.
