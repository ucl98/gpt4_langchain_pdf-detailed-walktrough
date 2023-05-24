## Table of Contents

- [Prerequisites](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#prerequisites)
- [Foreword](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#foreword)
- [Project setup](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#project-setup)
- [Debugging](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#debugging)
  - [Alternative ingest with python](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#alternative-ingest-with-python)
  - [Openai paid account](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#openai-paid-account)
  - [Openai free trial expired](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough/blob/main/README.md#openai-free-trial-expired)
  - [Issues with GPT4 api key](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#issues-with-gpt4-api-key)
  - [Check if pinecone is working](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#check-if-pinecone-is-working)
- [Contribution](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#contribution)

## Forwords to China
Some have reported issues with this project when they start it in china. There might be regional blocking from openai/pinecone (21.05.2023).

#### Solution from jchermy
1. : Create Cloudflare Worker, refer to https://github.com/noobnooc/noobnooc/discussions/9;
2. ：Proxy all the needs of openai. The example is as follows:
  ```js
  const embeddings = new OpenAIEmbeddings(undefined, {
    basePath: 'https://openai.1rmb.tk/v1/',
    apiKey: 'xxx',
  }); 
  ```

## Prerequisites

- Openai account with payment option.
  - Check in this section, if your openai account is appropiate: [issues-with-openai](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#issues-with-openai), [Openai free trial expired](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#Openai free trial expired).
    - Having a openai membership for ChatGPT is **NOT** sufficient. 
  - As rough estimate: 1000pdf pages cost about 1€.
  - Use GPT3.5 key first before trying GPT4 key ([Issues with GPT4 api key](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough#Issues-with-GPT4-api-key)).
    - GPT4 key may cause issues or will be less performaned.
- Pinecone account.

## Discord Server
[Join the discord if you have questions](https://discord.com/invite/E4Mc77qwjm).

## Project setup

###### Download the project

Download the project: https://github.com/mayooear/gpt4-pdf-chatbot-langchain

###### Install nodejs and npm

Install Node.js and npm. 
Official website: https://nodejs.org/en/download

Verfiy that everything is installed with the following terminal commands.
- Your version may differ, it is only important that node has version 18 or higher.

![image](https://user-images.githubusercontent.com/132441647/235887685-8c1ae873-48b6-4b34-a01c-ce01bbee14ed.png)

###### Install all required packages

Open a terminal at the top level of the project and run "npm install" to install all necessary dependencies.

![image](https://user-images.githubusercontent.com/132441647/236019383-a1e5b602-ac6f-4494-9ded-411cade89caf.png)

###### Create a ".env"

Create a file named ".env" inside your project with the following content.
```.env
OPENAI_API_KEY = 

PINECONE_API_KEY = 
PINECONE_ENVIRONMENT = 

PINECONE_INDEX_NAME = 
```
![image](https://user-images.githubusercontent.com/132441647/240514496-a24b3ce3-ce67-401a-9994-69bd8d18bd4d.png)

###### Openai api key

Go to https://platform.openai.com/overview and got "View API keys".

![image](https://user-images.githubusercontent.com/132441647/235887753-125b598d-664f-4844-91a5-fd8d5dd4c18a.png)

Click "+ Create new secrete key" and copy the key in your ".env" file
![image](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough/assets/132441647/5089d79e-0676-4413-90fb-c0d4753ce8ec)

###### Pinecone api key

Go to https://app.pinecone.io/organizations/ and create an api key there as well. Add them to the ".env" file.

![image](https://user-images.githubusercontent.com/132441647/235887859-f78c9e7b-4529-40bd-bdc7-4e72ec03837d.png)

###### Pinecone index

Create a new pinecone index with the Dimension `1536`.

![image](https://user-images.githubusercontent.com/132441647/235887835-80163968-6cbc-47ed-8392-fe604389d793.png)

It should look similar to this:

![image](https://user-images.githubusercontent.com/132441647/235887815-9d2da5e8-8a7e-4974-a10d-78d38cdf59fb.png)

###### Add pinecone index to the ".env" file

Add the information from your index correct to the .env file. At this point it should look like this:

![image](https://user-images.githubusercontent.com/132441647/235888151-4e1411ac-140c-452c-9cbd-a74905988571.png)

###### (Optional) Set namespace in config/pinecone.ts

Give the namespace for your vectors a name in "config/pinecone.ts".

![image](https://user-images.githubusercontent.com/132441647/235887923-bf356cd0-481f-4ec0-ad1a-cf61e9aa5fe2.png)

All vectors that are ingested will be available by this namespace in your pinecone index.
The name you defined in "config/pinecone.ts" will be used to store your ingested data in this namespace, but also lookup your data on a question to the chatbot.
- It is not possible to search data in multiple namespaces simultaneously.

![image](https://user-images.githubusercontent.com/132441647/236438694-147bfae9-e84f-40b1-be68-99ae4822dfbe.png)

###### Docs folder

Create a folder "docs" where you have your pdf files.

![image](https://user-images.githubusercontent.com/132441647/235887949-f5d8df0d-ecb1-46e6-917f-18bf65adf9ea.png)

###### Ingest your pdf

Run "npm run ingest" in a terminal. This will ingest your pdf into the pinecone database. Remove the pdf document from the "docs" folder, otherwise it will be ingested a second time if you run "npm run ingest" again.

The terminal must be in the project folder at the top level. I have installed "gpt4-pdf-chatbot-langchain" in "Documents".
![image](https://user-images.githubusercontent.com/132441647/236017033-400a4c81-53fb-4bf5-b41a-a3ddbcf4de3d.png)

###### Start appliation

Start the application with "npm run dev" in the terminal. Open a browser and go to the address http://localhost:3000/. You should see the project.
![image](https://user-images.githubusercontent.com/132441647/236017283-60c6eb6c-bd7f-4c73-8ced-cf8fa2628d03.png)

## Debugging

#### Alternative ingest with python

To trouble shoot it might be useful to take a look at my python reimplementation at ingest. It gives more control over each step of ingest.

https://github.com/ucl98/pinecone_ingest_python_implementation

#### Openai paid account
Check if you have a paid account. If you see the following message, you need to set up a paid account.
- https://platform.openai.com/account/usage
![image](https://user-images.githubusercontent.com/132441647/235887985-f0d83447-a7e0-4dcd-87ac-11458d0742d1.png)

#### Openai free trial expired
You may used a free trial for the openai api. This trial expires and in this case you cannot use the openai api.
For this case add a payed option.
![image](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough/assets/132441647/8fab065d-4f60-462c-b8ce-c94ceede8b5b)
![image](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough/assets/132441647/37cc0650-2685-4d04-81b1-fbfebcc96218)


#### Issues with GPT4 api key
Go to [openai playgroud](https://platform.openai.com/playground?mode=chat) and check if you have access to GPT4. If the model is not available, you will have no access to it and need to use GPT3.5.
- Access to the GPT4 api key does not depend on a ChatGPT subscription. You needd to [apply for it](https://openai.com/waitlist/gpt-4-api).
<img width="1440" alt="image" src="https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough/assets/132441647/e4933871-c217-4363-9108-45a81396a063">

#### Check if pinecone is working
You can make a pinecone api request on the webpage of pinecone. Go to the "Query" tab, enter the namespace, approve the namespace and then hit "query". If it returns a result, the connection to pinecone is working.
<img width="1440" alt="image" src="https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough/assets/132441647/1271fb37-f7b2-40ea-a085-8b7256a30c34">
<img width="1440" alt="image" src="https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough/assets/132441647/533cc730-1b5c-4e4b-8bd5-e2141bac4f25">

##### Api keys
Another issue can be that your api key is not working. Create a new one and test it again.
![image](https://github.com/ucl98/gpt4_langchain_pdf-detailed-walktrough/assets/132441647/5089d79e-0676-4413-90fb-c0d4753ce8ec)

## Contribution
- ucl
- angelina-magidova-synder
- chaudhary_181
- jchermy
