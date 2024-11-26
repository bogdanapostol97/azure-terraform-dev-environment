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

![image](https://github.com/user-attachments/assets/5bd55b28-d345-4c21-8970-051ba40e8ac1)

8. At this point we can check the structure of a terraform.tfstate file.

![image](https://github.com/user-attachments/assets/1051b826-d9b0-47b9-b8a2-6de33e281b2d)

**Note:**

- There are very, very, very few circumstances where we should modify terraform.tfstate manually - - actually  we should not be able to have access to it because it should be stored remotely.
- Everytime we modify the state, it creates a backup as we can see in the above screenshot.
- If the state was corrupted or you made a big mistake, you can delete the tfstate and rename the backup as terraform.tfstate.
- If we want everything back to the initial state with all the resources, we will run terraform apply again. 

9. Create a subnet:

![image](https://github.com/user-attachments/assets/ee3ce5cb-e6ee-4879-88d4-0f1ea97961fd)

After saving the code, we will run terraform plan && terraform apply:

![image](https://github.com/user-attachments/assets/f2b0e75d-49cc-4021-b9fe-5442a2d3a139)

![image](https://github.com/user-attachments/assets/ef97c5bb-7a65-4cff-890c-a1954f9b0600)

Checking if it was created in the Azure portal:

![image](https://github.com/user-attachments/assets/644bd93e-1422-4622-a2b3-5e078820b5d1)

10. Create a network security group:

![image](https://github.com/user-attachments/assets/d01a263f-eb12-4aa3-9055-5a7bb10daf66)

Terraform plan & terraform apply -auto-approve:

![image](https://github.com/user-attachments/assets/ec3f9079-3a00-4fd7-ac0c-0333d6c28c16)

Creation of the resource in Azure portal:

![image](https://github.com/user-attachments/assets/627fc606-1c3a-4b4f-8300-02678cd6cb9c)

11. Associate the network security group with the subnet

![image](https://github.com/user-attachments/assets/2740fedf-5df1-43c7-b77e-b81346943c44)

The proof it was created in Azure portal:

![image](https://github.com/user-attachments/assets/dc8fe404-af5f-46e6-85a4-844e05d0791c)

12. A public IP:

![image](https://github.com/user-attachments/assets/4d592955-fae8-4283-83c6-40ae1fcda888)

13. A network interface:

![image](https://github.com/user-attachments/assets/a0be2678-1d01-4d46-b8f7-4aa546df0ef0)

![image](https://github.com/user-attachments/assets/2fd71827-fa13-4d80-be23-1e4e31324e55)

**Note:** The value of the public IP will not show up when we run **terraform state show** command until it is attached to a resources and it is used somewhere.

14. A linux Virtual Machine: 

![image](https://github.com/user-attachments/assets/2f1c0538-388e-4101-9160-c589d0a3bfb9)

The creation in Azure portal:

![image](https://github.com/user-attachments/assets/42b48d33-3248-421a-a6c1-e4ea77e482da)

Terraform show:

![image](https://github.com/user-attachments/assets/9f2266c1-7ad6-4b47-82b6-ebcb02bef8ce)

**Notes:** To create the SSH Key and attach it to the Virtual Machine, we can use the following

- Run **ssh-keygen -t rsa.**
- Once you are asked to save the key somewhere on your computer, rename it as your preference (in my case mtcazurekey
- Verify the creation of the key navigating
- You can add the following block inside the definition of the Virtual Machine in the terraform file:

![image](https://github.com/user-attachments/assets/4f9d9522-9325-440a-b8dc-920c97073a3e)

15. SSH connect to VM:

- After running the **terraform state show azurerm_linux_virtual_machine.mtc-vm**, you take the public IP from the Virtual Machine details that are listed:
  
![image](https://github.com/user-attachments/assets/be411f4c-b74b-4475-a6f1-a4febbfea6ff)

- Run the following command to connect to VM: 

![image](https://github.com/user-attachments/assets/b814a359-616e-472e-bb9a-7da19ee78a3f)

- Verify if you successfully logged in the right linux distribution by running the following command:

![image](https://github.com/user-attachments/assets/50b36efd-ec87-41ba-9a3b-4b435c0564a0)


16. Docker installation using custom data:

- Create a custom data file with the following bash script:

![image](https://github.com/user-attachments/assets/e2274aa7-0862-4de9-b7bf-1f15880c1bae)

- We add the reference of the custom data file in the definition of VM in the terraform file like this:

![image](https://github.com/user-attachments/assets/b47dc6c4-8b06-4b27-8c6c-6ee8eb495303)

**Note:** 

- After implementing the above steps, we need to run **terraform plan** && **terraform apply** once again to replace the VM already created with a new one, SSH connect to the new VM and verify the docker installation with **docker --version** command.
- **filebase64** - reads the contents of a file at the given path and returns them as a base64-encoded string.

17 Final enhacements:

17.1) **Leverage variable for tag:** Instead of repeating "dev" for the environment tag in multiple resources, define a variable environment = "dev" at the beginning and use it for all tags:

![image](https://github.com/user-attachments/assets/36057a5d-067d-4d35-a70f-d2f9d305f507)

- We are the using for all the resources with that prefix.

![image](https://github.com/user-attachments/assets/ac6d862f-b6ad-4c13-97bb-2fae86aef516)

17.2) **Standardize Naming Conventions:** Use a consistent naming pattern for your resources. For example, instead of a static name "mtc-vm", you could use "${var.prefix}-vm" where var.prefix is another variable defined at the beginning. This makes your code more readable and easier to manage.

![image](https://github.com/user-attachments/assets/ffc43822-e148-4c66-a824-05c04b3411da)

- And I used it again for all the resources that are in this situation:

![image](https://github.com/user-attachments/assets/4901d8a7-3009-405c-ba1b-f5e31c98af08)

<h2> Project improvement </h2>

**1. Implement Automated Testing:**

- Unit Tests: Write unit tests for individual Terraform modules to verify their correctness and prevent regressions.
- Integration Tests: Test the entire Terraform configuration to ensure it deploys the desired infrastructure. Tools like terraform-compliance can help with this.

**2. Utilize Terraform Modules for Complex Configurations:**

- Break down complex infrastructure into smaller, reusable modules.
- Organize modules into a hierarchical structure for better management.
- Use variables and outputs to make modules flexible and configurable.

**3. Implement Continuous Integration and Continuous Delivery (CI/CD):**

- Set up a CI/CD pipeline to automate the testing, building, and deployment of your infrastructure.
- Use tools like Jenkins, GitLab CI/CD, or Azure DevOps to define and execute your pipeline.
- Integrate with version control systems like Git to track changes and manage deployments.

<h2> Conclusion </h2>
By following the best practices outlined in this document, you can streamline your Terraform infrastructure provisioning process, enhance code quality, and reduce the risk of errors. Leveraging modules, variables, and automated testing, you can create a more efficient and reliable infrastructure.

