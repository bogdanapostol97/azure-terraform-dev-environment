<h1> Azure DEV Environment using Terraform </h1>

In this lab I developed a Terraform DEV environment using Visual Studio Code to deploy an Azure Ubuntu virtual machine that I can SSH into to have my own redeployable environment

<h2> Disclaimer </h2>

Many thanks to the guidance offered in the laboratory: [https://www.youtube.com/watch?v=TkEubrv8gA0](https://www.youtube.com/watch?v=V53AHWun17s&t=872s)

The documentation is customized with my implementation and how I solved the issues that have appeared along the way.

<h2> Introduction </h2>

This project leverages AWS services to provide a scalable and secure solution for file sharing. It utilizes serverless functions for cost-effectiveness and eliminates the need to manage physical servers. Users can interact with the platform using any HTTP client, making it versatile for various file sharing and storage needs.

<h2> Prerequisites </h2>

- Azure Account: A valid Azure account with appropriate permissions.
- Terraform: Installed on your local machine.
- Azure CLI: Installed and configured with your Azure credentials.

<h2> Implementation guide </h2>

1. Create a New Directory:

Create a new directory to store your Terraform configuration files:

mkdir terraform-azure
cd terraform-azure

2. Install the Visual Studio Code Terraform extension.

![image](https://github.com/user-attachments/assets/6b238a74-27cd-48c8-b047-6d4a625cd9c1)

3. Initialize Terraform:

4. Login to the Azure CLI:

Follow the instructions from this official Microsoft documentation to check there are https://learn.microsoft.com/bs-latn-ba/cli/azure/authenticate-azure-cli

To verify the successful login you can run the following command:

![image](https://github.com/user-attachments/assets/fd7e43e9-b36f-407c-bb2a-584dfb9defb3)



<h2> Conclusion </h2>
This serverless file sharing platform offers a cost-effective and scalable solution for secure file uploads and downloads. By leveraging AWS services such as Lambda, API Gateway, and S3, it eliminates the need for managing physical servers, reducing operational overhead and costs.

**Key benefits of the serverless application in real-world scenarios:**


- Scalability: The platform can automatically scale to handle varying workloads, ensuring high availability and performance even during peak traffic.
- Cost-efficiency: Serverless architecture eliminates the need to pay for idle resources, making it cost-effective for applications with fluctuating workloads.
- Reduced maintenance: The platform handles server management and infrastructure updates, freeing developers to focus on application development.
- Rapid deployment: Serverless functions can be deployed quickly and easily, accelerating time-to-market.
- Integration with other AWS services: The platform can be easily integrated with other AWS services like Cognito for user authentication, DynamoDB for data storage, and SQS for asynchronous processing.

Overall, this serverless file sharing platform provides a robust and flexible solution for various file sharing and storage needs, making it ideal for businesses and individuals seeking a scalable and cost-effective solution.
