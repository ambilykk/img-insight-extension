<img width="250" alt="img-insight-icon1" src="./img-insight-extn/img-insight-icon.png" />

# Copilot Extension - Image Insight

The Copilot Extension processes image files to generate code snippets from visual data, analyze and interpret architecture diagrams, and convert diagram-based logic into code. It can extract key information to create class files, model data from images, and identify target resource requirements. Additionally, it generates test cases from visual flows and parses network topology diagrams to produce configuration scripts.

> **Note:** This solution was developed to demonstrate potential use cases and is not intended for production use. If you plan to deploy it in a production environment, please customize it to meet your non-functional requirements (NFRs). This repository is not regularly maintained or updated.

## Components:

1.  Copilot Chat: User interfacce
2.  img-insight Extension: Copilot Extension to process image
3.  GitHub Model: GPT 4o-mini model from GitHub Models for processing the user request
4.  GitHub Keys api: Request verification
5.  GitHub content api: Retrieve the content of attachments, if any

![Image Insight Components](https://github.com/user-attachments/assets/23edd14e-72d5-4bd2-8483-f6f8e30d3794)

## Pre-requisites:
1.  Copilot license
2. [GitHub Models](https://github.com/marketplace/models) access or [Azure OpenAI service](https://azure.microsoft.com/en-in/products/ai-services/openai-service)

## Features of this Extension:

  ### 1. Analyze and Interpret the Architecture Diagram
   This feature allows you to analyze and interpret architecture diagrams.

  **Sample Prompts:**
  ```
  - Explain the architecture at *image link*.
  - Explain the attached image 
  ```
  
  ### 2. Generate Class Files
  This feature helps you generate class files based on diagrams.
  
  **Sample Prompts:**
  ```
  - Create C# class files using the diagram at *image link*.
  - Create Java class files based on attached diagram
  ```
  
  ### 3. Converting Diagram-Based Logic into Code
  This feature converts logic from diagrams into code.
  
  **Sample Prompts:**
  ```
  - Convert this logic into a JavaScript function *image link*.
  - Create Python code based on the attached flow-chart
  ```
  
  ### 4. Image-Based Data Modeling
  This feature generates SQL create statements using entities defined in images.
  
  **Sample Prompts:**
  ```
  - Generate SQL create statements using the entities defined at *image link* .
  ```
  
  ### 5. Identify Target Resource Requirements
  This feature identifies the Azure resources utilized in architecture diagrams.
  
  **Sample Prompts:**
  ```
  - What are the Azure resources utilized in *image link* 
  ```
  
  ### 6. Generating Test Cases from Visual Flows
  This feature generates unit test cases using JUnit to address functionality defined in visual flows.
  
  **Sample Prompts:**
  ```
  - Generate unit test cases using JUnit to address the functionality defined at *image link*.
  ```
  
  ### 7. Parse Network Topology Diagrams to Generate Configuration Scripts
  This feature generates configuration scripts based on network topology diagrams.
  
  **Sample Prompts:**
  ```
  - Generate configuration scripts for the diagram at *image link*.
  ```

 ### 8. Screen Design to code
  This feature convert a web or mobile design into code by extracting style and page components
  
  **Sample Prompts:**
  ```
  - Create html and css files for the design share *image link or attachment*.
  ```

## Demo Video

[![Watch the Img-Insight in Action](https://img.youtube.com/vi/JEJgF48sYxM/0.jpg)](https://youtu.be/JEJgF48sYxM)

## Local Setup Instructions


1. **Clone the Repository**
   ```bash
   git clone https://github.com/ambilykk/img-insight-extension.git
   
   ```

2.  Create a new `.env` file in the root directory of your project.
    Add the following line to the `.env` file, if you are using **GitHub Model**

        ```
        GITHUB_KEYS_URI=https://api.github.com/meta/public_keys/copilot_api
        GITHUB_TOKEN=<your-github-token>
        ```
    Add the following line to the `.env` file, if you are using **Azure OpenAI Service**

      ```
      GITHUB_KEYS_URI=https://api.github.com/meta/public_keys/copilot_api
      AZURE_OPENAI_ENDPOINT=
      AZURE_OPENAI_API_KEY=
      OPENAI_API_VERSION=
      ```
3.  **Modify Code to Select GitHub Model or Azure OpenAI**
    
    For using **GitHub Models**, no code changes are required.
    
    If you're using **Azure OpenAI Service**, modify the following code snippets:

    In [home.js](./img-insight-extn/home.js), update the statement:

    ```javascript
    const { chatProcessing } = require('./gh-model-client');
    ```
    
    to
    
    ```javascript
    const { chatProcessing } = require('./gh-model-client-Azure-OpenAI');
    ```
    
    In [attachment-processing.js](./img-insight-extn/attachment-processing.js), update the statement:
    
    ```javascript
    const { chatProcessing } = require('./gh-model-client');
    ```
    
    to
    
    ```javascript
    const { chatProcessing } = require('./gh-model-client-Azure-OpenAI');
    ```
  
5.  **Install the Required Dependencies**
    Navigate to the `img-insight-extn` directory and install the dependencies:

    ```bash
    cd img-insight-extn
    npm install
    ```

6.  **Run the App**
    Start the Extension application:

    ```bash
    npm start
    ```

7.  **Access the Application**
    Open your browser and navigate to:
    ```
    http://localhost:3000
    ```

## Deployment to Azure

1. Establish OIDC Connectivity with Microsoft Entra ID by refering the [documentation](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/about-security-hardening-with-openid-connect#getting-started-with-oidc)
   - Add the following secrets to GitHub Secrets:
     ```properties
     AZURE_CLIENT_ID - Your Azure client ID
     AZURE_AD_TENANT - Your Azure AD tenant
     AZURE_SUBSCRIPTION_ID  -  Your Azure subscription ID
     ```
2. Create a Web applicaton to host the extension
3. Update the `Environment Variables` in the Azure Web application with the following.
   
   For **GitHub Models**
   
   ```properties
   GITHUB_KEYS_URI=https://api.github.com/meta/public_keys/copilot_api
   GITHUB_TOKEN=<your-github-token>
   ```

   For **Azure OpenAI Service**

   ```properties
    GITHUB_KEYS_URI=https://api.github.com/meta/public_keys/copilot_api
    AZURE_OPENAI_ENDPOINT=<YOUR_AZURE_OPENAI_ENDPOINT>
    AZURE_OPENAI_API_KEY=<YOUR_AZURE_OPENAI_API_KEY>
    OPENAI_API_VERSION=<API_VERSION> Ex: 2023-03-15-preview
   ```
   
4. Update the `app-name` input for the workflow [Node Deploy](.github/workflows/node-deploy.yml) with the Azure Web application name
5. Trigger the workflow by selecting the `pack-name=img-insight-extn` and clicking on `Run workflow`

## GitHub Copilot Extension: Configuration Video

[![How to Configure Copilot Extension](https://img.youtube.com/vi/ky5TMI9skLE/0.jpg)](https://youtu.be/ky5TMI9skLE)

## References

1. [Copilot Extension](https://github.com/features/copilot/extensions)
2. [Copilot Extension Public Beta](https://github.blog/news-insights/product-news/enhancing-the-github-copilot-ecosystem-with-copilot-extensions-now-in-public-beta/)
3. [Copilot Extension Learning Resources](https://resources.github.com/learn/pathways/copilot/extensions/essentials-of-github-copilot-extensions/)
4. [Copilot Extension Toolkit & SDKs](https://github.com/copilot-extensions)
