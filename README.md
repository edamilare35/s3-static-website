# S3 Static Website Hosting

This project demonstrates how to host a static website on Amazon S3 with a custom domain and HTTPS.

## Table of Contents

- [Introduction](#introduction)
- [Setup Instructions](#setup-instructions)
  - [Prerequisites](#prerequisites)
  - [Steps](#steps)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This repository contains a static website with HTML, CSS, and JavaScript files. The website will be hosted on Amazon S3 with a custom domain and HTTPS.

## Setup Instructions

### Prerequisites

- AWS account
- AWS CLI installed and configured
- Registered domain name
- Access to Route 53 or another DNS service

### Steps

1. **Clone the Repository**
    ```sh
    git clone https://github.com/yourusername/s3-static-website.git
    cd s3-static-website
    ```

2. **Create an S3 Bucket**
    - Open the AWS Management Console.
    - Navigate to the S3 service.
    - Click on "Create bucket" and name it after your domain (e.g., `http://yourdomain.com`).
    - Choose a region and proceed with the default settings.
    - Enable public access in the permissions tab (for static site hosting).

3. **Enable Static Website Hosting**
    - In the S3 bucket settings, select the "Properties" tab.
    - Scroll down to "Static website hosting" and click "Edit."
    - Choose "Enable," set the index document to `index.html`, and the error document to `error.html`.
    - Save changes.

4. **Upload Website Files**
    - Use the AWS Management Console or AWS CLI to upload `index.html`, `error.html`, `styles.css`, and `scripts.js` to the bucket.

    ```sh
    aws s3 cp . s3://yourdomain.com/ --recursive
    ```

5. **Set Bucket Policy for Public Access**
    - In the S3 bucket settings, select the "Permissions" tab.
    - Click on "Bucket Policy" and add the following policy:

    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": "*",
          "Action": "s3:GetObject",
          "Resource": "arn:aws:s3:::http://yourdomain.com/*"
        }
      ]
    }
    ```

6. **Configure a CNAME Record for Custom Domain**
    - Go to Route 53 or your DNS provider.
    - Create a CNAME record pointing your domain to the S3 website endpoint.

7. **Set Up HTTPS with CloudFront and AWS Certificate Manager (ACM)**
    - Request a certificate in ACM for your domain.
    - Create a CloudFront distribution, set the origin as your S3 bucket, and use the ACM certificate.
    - Update your DNS records to point to the CloudFront distribution.

8. **Access the Website**
    - Use your custom domain to access the static website with HTTPS.

## Usage

Access the static website at your custom domain.

## Contributing

Contributions are welcome. Please open an issue or submit a pull request.

## License

This project is licensed under the MIT License.