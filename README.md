

## Prerequisites

- Openai account.
- Pinecone account.

## Project setup

###### Download the project

Download the project: https://github.com/mayooear/gpt4-pdf-chatbot-langchain

###### Install nodejs and npm

Official website: https://nodejs.org/en/download

Verfiy that everything is installed with the following terminal commands.

![image-20230503113530864](/Users/alessandrosanto/Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503113530864.png)

###### Create a ".env"

Create a file named ".env" inside yout project.

![image-20230503114129062](../../Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503114129062.png)

###### Openai api key

Go to https://platform.openai.com/overview and got "View API keys"

![image-20230503114340513](../../Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503114340513.png)

Click "+Create new secrete key" and copy the key in your ".env" file

###### Pinecone api key

Go to https://app.pinecone.io/organizations/ and create an api key there as well. Add them to the ".env" file.

![image-20230503114716258](../../Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503114716258.png)

###### Pinecone index

Create a new pinecone index with the Dimension `1536`.

![image-20230503114935909](../../Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503114935909.png)

It should look similar to this

![image-20230503115116431](../../Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503115116431.png)

###### Add pinecone index to the ".env" file

Add the information from your index correct to the .env file. At this point it should look like this

![image-20230503115256150](../../Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503115256150.png)

###### (Optional) config/pinecone.ts

Add a namespace for your vectors in "config/pinecone.ts".

![image-20230503115534960](../../Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503115534960.png)

###### Docs folder

Create a folder "docs" where you have your pdf files.

![image-20230503115836069](../../Library/Mobile Documents/com~apple~CloudDocs/Typora/Images/image-20230503115836069.png)

###### Ingest your pdf

Run "npm run ingest" in a terminal. This will ingest your pdf into the pinecone database. Remove the pdf document from the "docs" folder, otherwise it will be ingested a second time if you run "npm run ingest" again.

###### Start appliation

Start the application with "npm run dev" in the terminal. Open a browser and go to the address http://localhost:3000/. You should see the project.

#### Alternative ingest with python

To trouble shoot it might be useful to take a look at my python reimplementation at ingest. It gives more control over each step of ingest.

https://github.com/ucl98/pinecone_ingest_python_implementation

#### Issues with openai

Check if you have a paid account. If you see the following message, you need to set up a paid account.

![img](https://cdn.discordapp.com/attachments/1102300260602232973/1102900848083861554/image.png)
