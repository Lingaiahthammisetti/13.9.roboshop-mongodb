# MongoDB

We use bastion host as Docker server and EKS client.
Make sure `aws configure` is done in bastion and connected to EKS cluster.
```
aws eks update-kubeconfig --region us-east-1 --name roboshop-dev
```
```
kubectl create namespace roboshop
```
```
git clone https://github.com/Lingaiahthammisetti/13.9.roboshop-mongodb.git
```
```
cd 13.9.roboshop-mongodb
```

* Login to ECR
```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 730335449147.dkr.ecr.us-east-1.amazonaws.com
```
* Build MongoDB image.
```
docker build -t 730335449147.dkr.ecr.us-east-1.amazonaws.com/roboshop/dev/mongodb:v1.0.2 .
```
* Push image
```
docker push 730335449147.dkr.ecr.us-east-1.amazonaws.com/roboshop/dev/mongodb:v1.0.2
```
* Now install using Helm. move to helm directory
```
cd helm
```

```
helm upgrade --install mongodb . -n roboshop
```