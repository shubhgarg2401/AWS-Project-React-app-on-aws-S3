# AWS-Project-React-app-on-aws-S3
React App on AWS S3 with Static Hosting + Cloudfront . AWS PROJECT

------------

## SERVICES USED

- S3 Bucket
- AWS CloudFront
- AWS Route53
- React App

------------



### THE APPROACH

The idea was to host(static hosting) a react app on AWS S3 using CloudFront. The React App is stored inside a s3 bucket and route53 is used for dns Resolution, CloudFront for distribution and better accessibility. 


------------

### PROJECT WALKTHROUGH 


------------

##### Creating the React App in folder of our choice

`npx create-react-app shubh-app`

`cd shubh-app`

`npm start`

This should open up a localhost with our React App

![output of creating a react app](https://user-images.githubusercontent.com/53488130/121655408-36623400-cabc-11eb-8b70-5a3ae825547a.PNG)

`npm run build`

This will create our static files.

![npm run build command](https://user-images.githubusercontent.com/53488130/121655417-39f5bb00-cabc-11eb-9967-ef8c61166e80.PNG)


##### Create two S3 bucket  :

We create two S3 bucket with the bucket names as our domain name(shubhgarg.tk & www.shubhgarg.tk) and upload our React App into our second S3 bucket(www.shubhgarg.tk).

![creating a bucket](https://user-images.githubusercontent.com/53488130/121655450-41b55f80-cabc-11eb-94bc-29f785d3c1d0.PNG)
![created two s3 buckets](https://user-images.githubusercontent.com/53488130/121655460-42e68c80-cabc-11eb-8d4f-b45ffa9d0236.PNG)
![add files and folder to s3 bucket www shubhgarg tk](https://user-images.githubusercontent.com/53488130/121655513-4b3ec780-cabc-11eb-9f99-0fdb238f7600.PNG)


- We add the bucket Policy to specify our resource as the domain name and bucket.

![edit the bucket policy](https://user-images.githubusercontent.com/53488130/121655527-4da12180-cabc-11eb-9221-9c1bdabe83fa.PNG)

- We go to properties and edit the "static website hosting" settings.

 For **shubhgarg.tk bucket**, We redirect our requests to the second bucket(www.shubhgarg.tk).
For** www.shubhgarg.tk**, We enable static hosting.

![enable static website hosting redirect fro the second bucket](https://user-images.githubusercontent.com/53488130/121655549-51cd3f00-cabc-11eb-9394-4294221b0ac9.PNG)


##### Create  a Hosted Zone in Route53
 
 We Create a hosted Zone in route53 with our domain name (shubhgarg.tk).
 
 ![create a hosted zone](https://user-images.githubusercontent.com/53488130/121655648-64477880-cabc-11eb-8fe9-506971d048bb.PNG)

 We add two simple Record sets to route traffic to our subdomain.
 
![creating a simple record set](https://user-images.githubusercontent.com/53488130/121655672-67daff80-cabc-11eb-9953-35e1c88f0787.PNG)
![second record for other bucket](https://user-images.githubusercontent.com/53488130/121655686-6ad5f000-cabc-11eb-882b-336a5daf605b.PNG)
![records successfully created](https://user-images.githubusercontent.com/53488130/121655714-70cbd100-cabc-11eb-9859-acbbefa6d4e9.PNG)


**We should now be able to see our website being hosted but without the ssl certificate (https)**

![the node js website working](https://user-images.githubusercontent.com/53488130/121655741-75908500-cabc-11eb-8c22-9aa83944d9be.PNG)


##### WE CREATE THE SSL CERTIFICATE
![get the ssl certificate through dns](https://user-images.githubusercontent.com/53488130/121655767-7b866600-cabc-11eb-94bf-9e56e1cc92b4.PNG)


##### Creating a CloudFront Distribution

We create a CloudFront distribution with origin Domain name as our bucket (www.shubhgarg.tk). 
We change the viewer Protocol Policy to direct http requests to https.

![create cloudfront distribution](https://user-images.githubusercontent.com/53488130/121655796-80e3b080-cabc-11eb-96e5-e00469355d40.PNG)


For distribution Settings, We add our SSL certificate and CNAME so that we can now get a secure https response.

![adding the custom ssl certificate to our domain in cloudfront](https://user-images.githubusercontent.com/53488130/121655802-82ad7400-cabc-11eb-88c5-c9ce84e9feab.PNG)

We Create two CloudFront Distributions. One for www.shubhgarg.tk and the other for shubhgarg.tk to redirect requests to the https domain.

![cloud front distribution deployed](https://user-images.githubusercontent.com/53488130/121655881-922cbd00-cabc-11eb-81df-1c4b04e9709b.PNG)


##### EDIT THE RECORD SETs FOR OUR DOMAIN TO ROUTE TRAFFIC TO OUR CLOUDFRONT DISTRIBUTION.

![change the routing on route53 record to cloudFront](https://user-images.githubusercontent.com/53488130/121655906-98229e00-cabc-11eb-9e03-993494a08ec2.PNG)
![alias record changed in route53](https://user-images.githubusercontent.com/53488130/121655912-99ec6180-cabc-11eb-9e3d-af037b59d769.PNG)

WE SHOULD NOW BE ABLE TO GET A SECURE RESPONSE TO OUR REQUEST WITH A HTTPS SECURED DOMAIN.

![https secured website final step](https://user-images.githubusercontent.com/53488130/121655956-a1136f80-cabc-11eb-949c-72f692df026d.PNG)


**

------------

**PROJECT COMPLETE**
![architecture diagram](https://user-images.githubusercontent.com/53488130/121655977-a5d82380-cabc-11eb-8f3a-b1ac24dfbc29.PNG)


------------


**Other Resources Used :-**

For free Domain Name (freenom) : http://https://www.freenom.com/en/index.html?lang=en**
