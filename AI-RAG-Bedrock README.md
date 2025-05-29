<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a RAG Chatbot in Bedrock

**Project Link:** [View Project](http://learn.nextwork.org/projects/ai-rag-bedrock)

**Author:** Albert  
**Email:** tapcyberx@gmail.com

---

## Set Up a RAG Chatbot in Bedrock

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/ai-rag-bedrock_d5e8f1g2)

---

## Introducing Today's Project!

RAG (Retrieval-Augmented Generation) is an AI technique that enhances a model's responses by allowing it to retrieve and reference external data sources, such as your own documents, during generation.

In today’s project, I’ll demonstrate RAG by setting up a RAG-powered chatbot using Amazon Bedrock. The chatbot will be connected to a custom knowledge base, enabling it to provide more accurate, context-aware answers based on my uploaded content.


### Tools and concepts

Services I used were Amazon Bedrock, S3 and OpenSearch Serverless Key concepts I learnt include knowledge bases, requesting access to AI models, how chatbots generate responses (AI models + knowledge base), vector stores.



### Project reflection

This project took me approximately 3 hours to complete.

The most challenging part was getting the chatbot up and running, especially when configuring the Knowledge Base and resolving setup errors. However, the most rewarding part was troubleshooting and seeing everything work correctly, watching the chatbot respond accurately using my custom documents made the effort worthwhile.





I did this project to learn how Amazon Bedrock and Retrieval-Augmented Generation (RAG) work together to build intelligent, document-aware chatbots.

The project definitely met my goals,it gave me hands-on experience with setting up a Knowledge Base, configuring vector search, and integrating generative AI. It also helped me identify key areas to continue exploring, like prompt optimization and model selection for different use cases.

---

## Understanding Amazon Bedrock

Amazon Bedrock is an AWS service that makes it easy to build and scale generative AI applications without managing infrastructure. It acts like a marketplace for foundation models, allowing you to explore and use models from multiple top providers through a unified interface.

In this project, I’m using Bedrock to create a Knowledge Base and connect it to a RAG chatbot, enabling it to retrieve and respond with information from my own documents.

My Knowledge Base is connected to Amazon S3 because S3 serves as the storage location for the raw documents that the Knowledge Base will use.

Since Amazon S3 is AWS’s scalable object storage service, it allows me to store various types of files like PDFs, text documents, and other data in a single bucket.
This connection enables the RAG chatbot to retrieve relevant information from those documents when generating responses.

In this step, I uploaded documents to my S3 bucket, these files will serve as the foundation of my chatbot’s Knowledge Base.

It's important that my S3 bucket is in the same region as the Bedrock Knowledge Base because Amazon Bedrock is a regional service, and all data used must reside in the same AWS region as the Bedrock resource (KBase) to ensure proper integration and performance.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/ai-rag-bedrock_b5c8d1e2)

---

## My Knowledge Base Setup

My Knowledge Base uses a vector store to store and search text based on semantic meaning, not just keywords. I chose OpenSearch Serverless because it’s fully managed, scalable, and optimized for vector search operations.

When I query the Knowledge Base, OpenSearch compares the query’s embedding with stored document embeddings and returns the most relevant results, which are then passed to Amazon Bedrock to generate accurate, context-aware responses.

Embeddings are vector representations of text that capture the semantic meaning of each chunk. They allow the system to compare and retrieve relevant information based on contextual similarity, rather than exact keyword matches.

In this project, I’m using Titan Text Embeddings v2 because it’s fast, accurate, and cost-effective, making it a great choice for powering efficient and scalable search within my RAG Knowledge Base.

Chunking is the process of breaking down large text documents into smaller, manageable pieces called chunks. This makes it easier for the system to index and retrieve information accurately.

In my Knowledge Base, I configured chunking to create chunks of about 300 tokens each. This helps improve search efficiency and relevance when querying the vector store, allowing the RAG model to find and respond with the most relevant information from my documents.




![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/ai-rag-bedrock_p9r2s5t8)

---

## AI Models

AI models are essential for my chatbot because they act as the translator between the raw search results from the Knowledge Base and a natural, human-like response.

Without an AI model, the chatbot would simply return raw text chunks from documents. With the model, it can understand the context, synthesize the information, and deliver coherent, helpful answers making the interaction feel conversational and intelligent.

To access AI models in Amazon Bedrock, I first visited the “Model access” page in the AWS Console and submitted a request for access to the specific models I wanted to use.

This step is necessary because some foundation model providers have their own usage policies, terms, or approval processes. AWS handles this by requiring explicit access requests to ensure availability and compliance before allowing use of those models within Bedrock.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/ai-rag-bedrock_model-access-proof)

---

## Syncing the Knowledge Base

Even though I already connected my S3 bucket when creating the Knowledge Base, I still need to sync the data because syncing is what actually moves the data from S3 and into the Knowledge Base plus OpenSearch Serverless.

The sync process involves three steps: Bedrock takes data from S3 (Ingesting), Bedrock chunks and embeds the data (Processing) and Bedrock stores the processed data in the vector store (OpenSearch Serverless).



![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/ai-rag-bedrock_sync-screenshot)

---

## Testing My Chatbot

'I initially tried to test my chatbot using Llama 3.1 8B as the AI model, but it triggered an error - it was not available on demand. I had to switch to Llama 3.3 70B because it was offered on-demand by AWS (since it's a newer, eficient model).

When I asked about topics unrelated to my data, my chatbot could not help us with the request.  This proves the chatbot only knows information that I give it won't know anything outside of th Knowledge Base.

When you turn off the "Generate Responses" setting, the chatbot returns the raw chunks of text directly from the Knowledge Base, without running them through the AI model.

I tested this and saw that the chatbot provided a list 5 paragraphs pulled from the documents. When the setting is on, the AI model processes those chunks and generates a clear, conversational response, making the output easier to understand and more user-friendly.



![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/ai-rag-bedrock_d5e8f1g2)

---

## Upgrading My Chatbot

In a project extension, I looked into increasing the number of source chunks, which are number of chunck of text that the Knowledge Base will return for a query. This will improve my chatbot's responses by giving the AI model more data to use.

I also added a custom prompt that tells my chatbot to always respond by mentioning skills that the student's learnt, even if the student didn't ask for it directly. I also gave context that the database contains documentation for projects.



After adjusting the source chunks and the generation prompt, my chatbot's response became much more detailed. The chatbot would talk about skills I've learnt, and used 10 or more examples within the response.

![Image](http://learn.nextwork.org/delighted_indigo_timid_orc/uploads/ai-rag-bedrock_improved-response)

---

---
