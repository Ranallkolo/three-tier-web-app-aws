<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Three-Tier Web App

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-threetier)

**Author:** Abdulrahman Abdulkadir  
**Email:** abdabdulkadir62@gmail.com

---

## Build a Three-Tier Web App

![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-threetier_2b3c4d5e)

---

## Introducing Today's Project!

In this project, I will demonstrate how to build and deploy a Three-Tier Web Application architecture using cloud services. I'm doing this project to learn how web applications are structured across the presentation, application, and database layers, and how they can be deployed in a scalable and secure environment. This hands-on experience will help me better understand networking, compute resources, load balancing, and database management in real-world infrastructure.


### Tools and concepts

Services I used were S3, CloudFront, API Gateway, Lambda, and DynamoDB. Key concepts I learnt include Lambda functions for running backend logic without servers, API Gateway for creating RESTful APIs, DynamoDB for storing and retrieving data, and how to configure CORS to enable secure communication between different services. I also gained hands-on experience with setting up a fully functional three-tier architecture on the cloud.


### Project reflection

This project took me approximately a few hours to complete. The most challenging part was troubleshooting the CORS error and ensuring proper communication between the frontend and backend. It was most rewarding to see the entire three-tier architecture working together, with data successfully flowing from DynamoDB to the user through the API and frontend interface.


I did this project today to strengthen my understanding of how web applications are structured and deployed in the cloud using real AWS services. Yes, this project met my goals—it helped me apply theoretical knowledge in a practical way, especially around serverless architecture, API integration, and cloud-based data storage. It gave me a clearer picture of how the different layers of a modern web app work together.


---

## Presentation tier

For the presentation tier, I will set up an S3 bucket to host the static web content and use CloudFront as a content delivery network to distribute it globally. This setup ensures low latency, high availability, and secure access to the web application for users around the world.



I accessed my delivered website by using the CloudFront distribution URL, which served the static content stored in my S3 bucket. CloudFront helped improve performance and security by caching content at edge locations and providing HTTPS access.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-threetier_3a4b5c6d)

---

## Logic tier

For the logic tier, I will set up a Lambda function connected to an API Gateway because it allows me to run backend code that fetches data from a DynamoDB table without managing servers. This setup handles GET requests, processes the logic, and returns the data through a deployed RESTful API.


The Lambda function retrieves data by connecting to a DynamoDB table using the AWS SDK, executing a command (such as `GetItem`), and returning the retrieved data as a response. It is triggered through an API Gateway GET request, which passes any necessary parameters to the function.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-threetier_6a7b8c9d)

---

## Data tier

For the data tier, I will set up a DynamoDB table because it provides a fast, scalable, and serverless NoSQL database solution for storing user data. This allows the application to efficiently retrieve and manage data through the Lambda function and API Gateway.


The partition key for my DynamoDB table is userId, which means each item in the table is uniquely identified by a user ID. This allows the application to quickly retrieve specific user data by using the userId as a reference when making queries through the Lambda function.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-threetier_u1v2w3x4)

---

## Logic and Data tier

Once all three layers of my three-tier architecture are set up, the next step is to connect them because this allows the frontend to communicate with the backend and display dynamic data to users. I will update the script.js file to make a request to the API Gateway endpoint and verify that the retrieved data is displayed correctly on the website.



To test my API, I went to the API Gateway console and copied the Invoke URL for the prod stage. I then appended `/users?userId=1` to the end of the URL and ran it in my web browser. This allowed me to verify that the API correctly returned the data from the DynamoDB table for the specified userId.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-threetier_a112c3d5)

---

## Console Errors

The error in my distributed site was because the script in my index.html was trying to fetch data from the API before the API Gateway endpoint was correctly updated or deployed. It could also be due to CORS (Cross-Origin Resource Sharing) settings not being configured properly on the API Gateway, which prevented the frontend from accessing the backend response.


To resolve the error, I updated script.js by replacing the placeholder `[YOUR-PROD-API-URL]` with my actual API Gateway prod stage Invoke URL. I then reuploaded it into S3 because the website needed the correct endpoint to fetch data from the API, and updating the file in S3 ensures the latest version is served through CloudFront.


I ran into a second error after updating script.js. This was an error with CORS because API Gateway was not configured to allow requests from my CloudFront-hosted website. Without proper CORS settings, the browser blocks the frontend from accessing the backend, even though the API works when accessed directly.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-threetier_a1b2c3d5)

---

## Resolving CORS Errors

To resolve the CORS error, I first enabled CORS in my API Gateway by allowing GET requests and adding the necessary headers, such as `Access-Control-Allow-Origin`, in the method response and integration response settings. This update allows my CloudFront-hosted frontend to successfully communicate with the API without being blocked by the browser.


I also updated my Lambda function because the API needed to include proper CORS headers in its responses for the frontend to access the data without being blocked. The changes I made were adding `Access-Control-Allow-Origin` and `Access-Control-Allow-Headers` to the response headers returned by the Lambda function. This ensures that browsers accept the API response when it’s requested from a different domain, like my CloudFront-hosted site.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-threetier_1qthryj2)

---

## Fixed Solution

I verified the fixed connection between API Gateway and CloudFront by reloading my CloudFront-hosted website and checking that the data from DynamoDB was successfully displayed without any CORS errors in the browser console. This confirmed that the API requests were now going through properly and the frontend could access the backend data.


![Image](http://learn.nextwork.org/confident_turquoise_quiet_hyena/uploads/aws-compute-threetier_2b3c4d5e)

---

---
