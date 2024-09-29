Custom NGINX Docker Image
This repository provides a simple example of how to create a custom Docker image based on NGINX. The custom image will serve an HTML file that you provide.

Prerequisites
Docker installed on your machine
Basic knowledge of Docker commands
Getting Started
Step 1: Create a Dockerfile
Create a file named Dockerfile in your project directory and add the following content:

FROM nginx
COPY index.html /usr/share/nginx/html/index.html

Step 2: Build the Docker Image
Run the following command in your terminal to build the Docker image:

docker build . -t mynginx

This command will create a new Docker image named mynginx.

Step 3: Run the Docker Container
To run the newly created Docker image, use the following command:

docker run -p 8080:80 mynginx

This command will start a container from the mynginx image and map port 8080 on your host to port 80 in the container.

Step 4: Access Your Custom HTML Page
Open your web browser and navigate to http://localhost:8080/index.html. You should see your custom HTML page displayed.

Step 5: Push Docker Image to AWS ECR by authenticate your Docker client to your registry.

aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 211125333559.dkr.ecr.us-east-1.amazonaws.com

Step 6: Tag your image so you can push the image to this repository.

docker tag mynginx:latest 211125333559.dkr.ecr.us-east-1.amazonaws.com/clowkg:
latest

Step 7: Push this image to your AWS repository.

docker push 211125333559.dkr.ecr.us-east-1.amazonaws.com/clowkg:latest

Step 8: Verify images have been push to AWS ECR.

aws ecr describe-images --repository-name clowkg --query 'sort_by(imageDetails,& imagePushedAt)[-1].imageTags[0]'

Conclusion
You’ve successfully created and run a custom Docker image based on NGINX. This image serves an HTML file that you specified. Second part upload docker image to AWS ECR repository. 
Feel free to customize the index.html file to suit your needs.

License
This project is licensed under the MIT License - see the LICENSE file for details.






