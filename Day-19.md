## Day-19 (20-07-2024) : Azure Gen AI Part 2

### Table of Content:-
- [Steps to Make Azure ML](#steps-to-make-azure-ml)
- [URI vs. URL](#uri-vs-url)
- [API (Application Programming Interface)](#api-application-programming-interface)
- [Serverless API with Azure AI Content Safety](#serverless-api-with-azure-ai-content-safety)
- [Azure CLI](#azure-cli)
- [Virtual Environment](#virtual-environment)
- [Example Code Setup](#example-code-setup)

---

### Steps to Make Azure ML

**1. Create a Resource Group (RG)**
- Navigate to the Azure portal.
- Click on "Resource groups" and then click "Add".
- Fill in the necessary details such as Subscription, Resource group name, and Region.
- Click "Review + create" and then "Create".

**2. Create an Azure Machine Learning Workspace**
- Go to Azure Machine Learning in the Azure portal and click on "Create".
- Fill in the details:
  - Subscription
  - Resource group (use the one created in step 1)
  - Workspace name
  - Region
- Under **Networking**, choose **Public** for testing purposes.
- Leave other settings as default.
- Click "Review + create" and then "Create".

**3. Launch Studio and Select Model**
- Once the workspace is created, launch the Azure Machine Learning Studio.
- Navigate to the **Model catalog**.
- Choose a model, for example, **Meta-Llama-3-70B-Instruct**.
- Provide the deployment name.

**4. Install Azure CLI**
- Follow the [official instructions](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) to install Azure CLI on your machine.

**5. Log in to Azure CLI**
- Open the terminal and type:
  ```sh
  az login
  ```
- This will open a web browser window for you to log in with your Azure account.

**6. Write the Code for the Chatbot**
- Create your chatbot code. Here’s a simplified example using Python:
  ```python
  import openai

  openai.api_key = "your_openai_api_key"

  def chatbot_response(prompt):
      response = openai.Completion.create(
          engine="davinci",
          prompt=prompt,
          max_tokens=150
      )
      return response.choices[0].text.strip()

  user_input = input("You: ")
  print("Bot:", chatbot_response(user_input))
  ```

**7. Deploy the Chatbot**

#### Create a VM
- In the Azure portal, create a new VM.
- Configure it to allow access to all ports.
- Select an appropriate size and OS for your needs (e.g., Windows Server or Ubuntu).

#### Connect using RDP (Remote Desktop Protocol)
- Use an RDP client to connect to your VM using its public IP address and credentials.

**8. Configure the VM as a Web Server**
- Install necessary web server software (e.g., IIS for Windows or Apache/Nginx for Linux).

**9. Install Python and Necessary Packages**
- Ensure Python is installed on your VM.

**10. Upload and Run Your Code**
- Upload your code to the VM, typically in the `inetpub/wwwroot` folder.
- Open the command prompt or terminal and navigate to your project directory.
- Run the following to install packages:
  ```sh
  pip install -r requirements.txt
  ```
  Ensure your `requirements.txt` contains all the necessary dependencies.
- Navigate to the chat folder and run:
  ```sh
  streamlit run chat_fe.py --server.port 8080
  ```

**11. Configure Inbound Rule for Port 8080**
- In the Azure portal, navigate to your VM's network security group (NSG).
- Add an inbound security rule to allow traffic on port 8080.

---

### URI vs. URL
- **URI (Uniform Resource Identifier)**: A generic term for all types of names and addresses that refer to objects on the web. 
- **URL (Uniform Resource Locator)**: A specific type of URI that provides the means to locate a resource by describing its primary access mechanism (e.g., its network "location").

### API (Application Programming Interface)
- A set of functions and procedures allowing the creation of applications that access the features or data of an operating system, application, or other service.

### Serverless API with Azure AI Content Safety
- Azure AI Content Safety APIs are serverless, meaning you are charged only when they are used. This makes them cost-effective for applications requiring dynamic scaling.

### Azure CLI
- The Azure Command-Line Interface (CLI) is a set of commands used to manage Azure resources. It helps access tenant ID, subscription ID, and more, ensuring safe and efficient management.

### Virtual Environment
- **Virtual environments** help create isolated Python environments for your projects, ensuring dependencies are managed and the system remains clean.

### Example Code Setup

1. **Create a Virtual Environment**:
   ```sh
   conda create -n azureai python=3.11
   conda activate azureai
   conda info
   ```

2. **Navigate to Project Directory**:
   ```sh
   cd project1
   ```

3. **Install Required Packages**:
   ```sh
   pip install -r requirements.txt
   ```

4. **.env File Configuration**:
   - Ensure your `.env` file contains the necessary environment variables.
   - Example:
     ```env
     OPENAI_API_KEY=your_openai_api_key
     ```

5. **Checking Available Files**:
   - Use `wsl ls` to list available files in the terminal.

6. **ConversationBufferMemory**:
   - This feature helps to store memory in chat applications, ensuring context is maintained across interactions.

---

This guide provides a comprehensive approach to setting up Azure ML and deploying a chatbot, complete with detailed steps, visual aids, and example code.
