# Serverless Image Sharing API (AWS)

A serverless REST API for an image sharing app, where users create groups and upload images to them. Built in 2020 while learning AWS serverless development in Udacity's Cloud Developer nanodegree.

## Tech
* AWS Lambda (Node.js, TypeScript)
* Amazon API Gateway with request body validation
* Amazon DynamoDB (on demand tables with a global secondary index)
* Amazon S3 with presigned upload URLs
* Serverless Framework and webpack
* Infrastructure defined as code in `serverless.yml`

## Endpoints
| Method | Path | Description |
|---|---|---|
| GET | /groups | List all groups |
| POST | /groups | Create a group |
| GET | /groups/{groupId}/images | List images in a group |
| POST | /groups/{groupId}/images | Create an image record and return a presigned S3 upload URL |
| GET | /images/{imageId} | Get a single image |

## How it works
* Groups are stored in a DynamoDB table keyed by group id.
* Images are stored by group id and timestamp, with a secondary index on image id for direct lookups.
* Creating an image checks that the group exists, saves the record, and returns a short lived presigned URL so the client uploads the file straight to S3.
* IAM permissions are scoped per function to only the table and bucket actions each one needs.

## Running it
1. Install dependencies: `npm install`
2. Configure AWS credentials.
3. Deploy: `npx serverless deploy --stage dev --region us-east-1`

A Postman collection (`Udacity Serverless.postman_collection.json`) is included for testing the endpoints.

## Note
Started from course exercise material and extended as practice. Uses Node.js 12 and older package versions from 2020, so dependencies would need updating before deploying today.
