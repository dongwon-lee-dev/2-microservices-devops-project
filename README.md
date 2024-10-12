# Microservice DevOps Project

✨ **Technologies**: AWS Elastic Kubernetes Service (EKS), Postgres, MongoDB, RabbitMQ, Gmail

# <span style="background-color: cyan;">1) Configure Kubernetes</span>
### 1. Create VPC

IAM - Roles - Create eksClusterRole for cluster, AmazonEKSNodeRole for node

Create AWS EKS
Create and assign Microservices 1.28v myAmazonEKSClusterRole

Create AWS EKS NodeGroup

# <span style="background-color: cyan;">2) Deploy with Helm</span>
### 1. Create VPC
```bash
git clone https://github.com/N4si/microservices-python-app.git
```

Gmail App Password - Postgres init.sql and src notification manifest secret.yaml Write

postgres 5433

Connect to postgres and enter init.sql

```bash
mongosh mongodb://nasi:nasi1234@54.81.116.127:30005/mp3s?authSource=admin
```
```bash
psql 'postgres://admin:lee@54.81.116.127:30003/authdb'
```
# <span style="background-color: cyan;">3) Deploy Microservices</span>
### 1. Create a docker image

auth-service / gateway-service / notification-service (enter my email and app password)
```bash
docker built -t auth:latest . docker tag auth:latest mapleliberty:auth
docker push mapleliberty:auth
```

### 2. Change the docker file name of manifest

### 3. Deploy to Kubernetes
```bash
cd manifest
kubectl apply -f .
```

# <span style="background-color: cyan;">4) Use the app</span>
### 1. Get JWT with the login endpoint
```bash
curl -X POST http://54.81.116.127:30002/login -u robertleecnd@gmail.com:lee
```

JWT token Example
```bash
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InJvYmVydGxlZWNuZEBnbWFpbC5jb20iLCJleHAiOjE3Mjg3MDU5NTcsImlhdCI6MTcyODYxOTU1NywiYWRtaW4iOnRydWV9.sqpTzOAPiRqxauE5t27jYXgHBbBKIiTfpCFP18Z5DWY
```

### 2. Upload a video file to convert to the upload endpoint
```bash
curl -X POST -F "file=@./video.mp4" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InJvYmVydGxlZWNuZEBnbWFpbC5jb20iLCJleHAiOjE3Mjg3MDU5NTcsImlhdCI6MTcyODYxOTU1NywiYWRtaW4iOnRydWV9.sqpTzOAPiRqxauE5t27jYXgHBbBKIiTfpCFP18Z5DWY" http://54.81.116.127:30002/upload
```
If you get a success response, you can receive an email with the converted mp3 id.

### 3. Download converted mp3 file to download endpoint
```bash
curl --output video.mp3 -X GET -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InJvYmVydGxlZWNuZEBnbWFpbC5jb20iLCJleHAiOjE3Mjg3MDU5NTcsImlhdCI6MTcyODYxOTU1NywiYWRtaW4iOnRydWV9.sqpTzOAPiRqxauE5t27jYXgHBbBKIiTfpCFP18Z5DWY" "http://54.81.116.127:30002/download?fid=6708a471de79aa1f05288cdf" ```
