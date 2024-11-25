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

2. Authenticate to Azure portal using Azure CLI (install it

2. Install the Visual Studio Code Terraform extension.

![image](https://github.com/user-attachments/assets/6b238a74-27cd-48c8-b047-6d4a625cd9c1)

3. Define the version of Terraform and the cloud provider that we will connect to.

![image](https://github.com/user-attachments/assets/cf810f60-5652-4f46-96dc-82cd0eeb4888)

4. Check the validity of the file:

terraform fmt
  
5. Initialize Terraform:

terraform init

![image](https://github.com/user-attachments/assets/ec1e0286-9cff-4f54-8a57-9f79b081b79e)

**Important notes:** 

- Terraform init is interested only in provider related stuff.
- If we change something in the provider block and run terraform init (as in the below example), it will have no problem to run successfully.

![image](https://github.com/user-attachments/assets/9b45a69e-bf69-4035-932b-bf18e4b8ff00)

- If we run the wrong name of the provider, **terraform init** will fail. So terraform init is not enough to test the code. 

- terraform.lock.hcl is a file that communicates with the Azure API and maintain the version of terraform that we declared.

![image](https://github.com/user-attachments/assets/5e6889ff-d1b5-4efd-8fd4-93261e124bd2)


6. Create a resource group:

![image](https://github.com/user-attachments/assets/db6259fe-83e1-40f0-a392-0f8cdc94fbe7)

*Run **Terraform plan** (commans that creates an execution plan, which lets you preview the changes that Terraform plans to make to your infrastructure.) and then **Terraform apply** (command executes the actions proposed in a Terraform plan.)

**Note:** If you do want to apply the changes planned in the Terraform plan, directly in environment, without any other proper verification, we can use Terraform apply -auto-approve.

Created successfully in the Azure portal:

![image](https://github.com/user-attachments/assets/ff5c0325-6910-4a48-af34-5846803034e7)

**Important notes:** Double check the creation of the resource in the Azure portal.

7. Create a virtual network:

![image](https://github.com/user-attachments/assets/3583c980-b5b7-465a-af63-d763f6b3d603)

**Note:** 
- In this case I introduced the reference attributes of other resources.
- Why this concept of reference is not used? Because it creates a logical order of things: In our case you can't deploy to a virtual network if you haven't created and deployed to a resource group. 



<h2> Project improvement </h2>

<h2> Conclusion </h2>


**Key benefits of the serverless application in real-world scenarios:**




Overall, this serverless file sharing platform provides a robust and flexible solution for various file sharing and storage needs, making it ideal for businesses and individuals seeking a scalable and cost-effective solution.
