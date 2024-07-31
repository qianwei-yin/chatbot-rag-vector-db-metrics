# info7375-chatbot-rag-vector-db

### Report and Video

[Report](./REPORT.pdf)
[Video](https://www.youtube.com/watch?v=idEpmh0qCdA)

### Prompts used in the video demonstration

###### Should return answers and resources

What is MongoDB?<br><br>

###### Should return answers and resources

How do I create an index in mongodb?<br><br>

###### Should return an answer that is relate to the previous one

Then according to what you said, what are the benefits of using indexes in mongodb?<br><br>

###### Should say don't know and no answer

What is pinecone?<br><br>

###### Should return some examples and resources

What can mongodb do for my app?<br><br>

###### Should return one example because I narrow the range of my question

What can mongodb do for my app? Can you give me an example of e-commerce website?<br><br>

###### Should return one sensitive example because I make the question more specific

What can mongodb do for my app? Can you give me an example of e-commerce website? Notice that my website needs to be very scalable. Then what is the best practice of using mongodb in this scenario?<br><br>

### Domain Selection:

Domain: A chatbot to help users understand MongoDB official website
Scope: Provide information about MongoDB and its affiliated products.

### Installation

1. Clone the repository
2. `cd your-repository`
3. `pipenv shell` to create a virtual environment
4. `pipenv install` to install all the required packages
5. Set up environment variables:
   Create a `.env` file in the root directory of your project and add your Pinecone API key, OpenAI API key
   ```
   PINECONE_API_KEY=
   OPENAI_API_KEY=
   ```
6. To fetch data from MongoDB website
   ```
   mkdir mongodb-docs
   wget -r -P mongodb-docs -E https://www.mongodb.com/docs/manual
   ```
7. Pre-process data, run the `process_data.py` script.
   It will show the below if successful.
   ```
   Going to add xxx to Pinecone
   ****Loading to vectorstore done ***
   ```
8. Start the app by `streamlit run main.py`

### Notes

Ensure you have the necessary API keys and access for Pinecone and OpenAI.
Modify the INDEX_NAME if you want to use a different index name in Pinecone.

### Explanation of pre-processing data

#### Pass data to vector database (Pinecone) using `process_data.py`

`wget -r -P mongodb-docs -E https://www.mongodb.com/docs/manual`
This command gets documents data from MongoDB's documentation website, processes them, and stores them in a Pinecone Vector Store for efficient retrieval and embedding using OpenAI's embedding model.

#### Features

- Loads documents from MongoDB documentation.
- Splits documents into smaller chunks for efficient processing.
- Updates document metadata with the correct source URLs.
- Adds processed documents to a Pinecone Vector Store.

#### Requirements

- Python 3.x
- python-dotenv
- langchain
- langchain-community
- langchain-openai
- langchain-pinecone
- Pinecone account and API key

#### Functionality

##### `ingest_docs()`

This function:

1. Loads documents from MongoDB documentation using `ReadTheDocsLoader`.
2. Splits documents into smaller chunks using `RecursiveCharacterTextSplitter`.
3. Updates the source URL metadata of each document.
4. Adds the processed documents to a Pinecone Vector Store using `PineconeVectorStore.from_documents`.

##### Main Execution

The script runs the `ingest_docs()` function when executed as the main module.

### Explanation of RAG (Retrieval-Augmented Generation) Script (rag.py)

This Python script implements a Retrieval-Augmented Generation (RAG) model using LangChain, OpenAI, and Pinecone. The script retrieves relevant documents based on a query, incorporates chat history, and generates responses using OpenAI's language models.

#### Features

- Embeds documents using OpenAI's embedding model.
- Retrieves documents from Pinecone Vector Store.
- Rephrases queries and performs retrieval-based question answering.
- Combines retrieved documents to generate a response.

#### Requirements

- Python 3.x
- python-dotenv
- langchain
- langchain-openai
- langchain-pinecone
- Pinecone account and API key
- OpenAI API key

#### Functionality

##### `run_llm()`

This function:

1. Initializes OpenAI embeddings and Pinecone Vector Store.
2. Sets up a chat model with OpenAI's language model.
3. Pulls prompts for rephrasing queries and retrieval-based question answering.
4. Creates a history-aware retriever and a retrieval chain.
5. Invokes the retrieval chain with the input query and chat history.
6. Returns the generated result.
