

## Prerequisites

- Openai account.
- Pinecone account.

## Foreword
Every change I did in the gpt4-pdf-chatbot-langchain project, I have included in the "gpt4-pdf-chatbot-langchain" folder.
It should give you a quick overview on what changes need to be done. It needs your api-keys, namespace, .. though. It is not meant to be copied to your gpt4-pdf-chatbot-langchain project.

[Join the discord if you have questions](https://discord.com/invite/E4Mc77qwjm)

## Project setup

###### Download the project

Download the project: https://github.com/mayooear/gpt4-pdf-chatbot-langchain

###### Install nodejs and npm

Official website: https://nodejs.org/en/download

Verfiy that everything is installed with the following terminal commands.
- Your version may differ, it is only important that node has version 18 or higher.

![image](https://user-images.githubusercontent.com/132441647/235887685-8c1ae873-48b6-4b34-a01c-ce01bbee14ed.png)

###### Create a ".env"

Create a file named ".env" inside yout project.

![image](https://user-images.githubusercontent.com/132441647/235887711-839ca986-e6c7-4bd9-ad05-39ada6477683.png)

###### Openai api key

Go to https://platform.openai.com/overview and got "View API keys".

![image](https://user-images.githubusercontent.com/132441647/235887753-125b598d-664f-4844-91a5-fd8d5dd4c18a.png)

Click "+Create new secrete key" and copy the key in your ".env" file

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

###### (Optional) config/pinecone.ts

Add a namespace for your vectors in "config/pinecone.ts".

![image](https://user-images.githubusercontent.com/132441647/235887923-bf356cd0-481f-4ec0-ad1a-cf61e9aa5fe2.png)

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

#### Alternative ingest with python

To trouble shoot it might be useful to take a look at my python reimplementation at ingest. It gives more control over each step of ingest.

https://github.com/ucl98/pinecone_ingest_python_implementation

#### Issues with openai

Check if you have a paid account. If you see the following message, you need to set up a paid account.
<img width="1273" alt="image" src="https://user-images.githubusercontent.com/132441647/235887985-f0d83447-a7e0-4dcd-87ac-11458d0742d1.png">

## Contribution
- ucl
- angelina-magidova-synder
