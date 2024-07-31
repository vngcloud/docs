# Application Load Balancer

## What is an Application Load Balancer?

An Application Load Balancer (ALB) is a networking and server infrastructure tool used to distribute network traffic across multiple servers or virtual machines. This improves the performance and availability of applications. ALBs operate at the application layer, allowing for traffic distribution based on various factors such as request type, server health, and load-balancing algorithms.

ALBs offer advanced routing capabilities, enabling traffic steering based on host or path headers. They also support session persistence, which helps maintain a user's session on the same server, ensuring a consistent experience for applications that require it.

Another key feature of ALBs is their ability to handle SSL/TLS traffic encryption and decryption. This offloads computational work from backend servers, enhancing overall performance and ensuring secure communication.

Thanks to these unique features, Application Load Balancers play a crucial role in improving the performance, scalability, and availability of online applications.

## Key Features

* **Advanced Routing:** ALBs allow for routing based on host and path headers. This lets you direct requests to specific targets based on the content of the request, providing flexibility in tailoring traffic distribution.
* **X-Forwarded Headers:** Supports adding common HTTP headers to requests before distributing them to backend servers. These headers provide backend servers with additional information about the client making the request.
* **Session Persistence:** ALBs support session persistence, ensuring that requests from the same user are always directed to the same backend server. This enhances the consistency of the user experience.
* **Health Checks:** ALBs automatically check the health of backend servers by sending periodic test requests. If a server is not functioning correctly, the ALB stops directing traffic to it, ensuring higher performance and better availability.
* **SSL/TLS Encryption:** ALBs can handle the encryption and decryption of SSL/TLS traffic, offloading this computational work from backend servers and boosting overall performance.
* **Authentication and Authorization:** Integrates with VNG Cloud IAM, fully supporting authentication and authorization features.
* **Load Balancer Monitoring:** Easily monitor the health and access history of clients, as well as the editing history of the Load Balancer.
* **Terraform:** Supports the quick and efficient creation and management of Load Balancers using Terraform.

## Learn More

Find out more about Application Load Balancers here:

* **How it works (ALB)**
* **Getting Started**
* **Manage Load Balancer**
* **Listener**
* **Certificate**
* **Pool**
* **Feature Comparison**
