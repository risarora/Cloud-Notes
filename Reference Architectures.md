# AWS architecture for use case: Rekognition to choose 3x "best" thumbnail images when a selfie-style video is uploaded to an S3 bucket.


![AWS Lambda Architecture](https://user-images.githubusercontent.com/4485129/116670268-27686c00-a9bd-11eb-9212-e8cd3fe9d0b4.png)
Context:

* Have an app. Want to add a feature to that app that automatically suggests image thumbnails for a selfie-style video.
* App is an MVP and so is this feature. Expect low user volume for foreseeable future. Don't need perfection. Want to keep it simple and low cost.

### Requirements: Each time a video hits S3_Bucket_1 my app's API endpoint is gets an error or success message. For each thumbnail, success message sends:

* S3 URLs for the thumbnail
* S3 URL of the video that initiated the process
* Rekognition label (eyes open, happy, smile) predictions



## Proposed Architecture:

* Video_1 hitting S3_Bucket_1 triggers Lambda_1 which triggers MediaConvert_1
* MediaConvert_1 creates a first 15 second clip of Video_1. The clip, Video_2 is saved in S3_Bucket_2.
* Goal of clip is to cap Rekognition cost at 15 seconds.
* S3_Bucket 2_event triggers Lambda_2 which triggers Rekognition.
* Rekognition analyzes Video_2 and assigns labels (eyes open, happy, smile). Rekognition publishes SNS topic which triggers Lambda_3
* Lambda_3 uses Rekognition labels to determine which 3x timestamps are best for thumbnail purposes and triggers MediaConvert_2
* MediaConvert_2 creates 3x thumbnails and saves each to S3_Bucket_3
* S3_Bucket_3 event triggers Lambda_4 which deletes the Video_2 and sends data about the 3x thumbnail images back to my app's API.



[AWS Lambda Architecture.svg.zip](https://github.com/risarora/Cloud-Notes/files/6403984/AWS.Lambda.Architecture.svg.zip)
