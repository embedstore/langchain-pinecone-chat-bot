# langchain-pinecone-chat-bot

This repo is a fully functional Flask app that can be used to create a chatbot app like BibleGPT, KrishnaGPT or Chat app over any other data source.

It uses the following

* Ready made embeddings from [embedstore.ai](https://embedstore.ai) ([python package](https://github.com/embedstore/pyembeddingtown)). These text is chunked using LangChain's RecursiveCharacterTextSplitter with chunk_size as 1000, chunk_overlap as 100 and length_function as len. OpenAI embeddings (dimension 1536) are then used to calculate embeddings for each chunk.
* It loads the embeddings and then indexes them into a Pinecone index.
* Now whenever a user query is received, it first creates embedding for it using OpenAI embeddings. Then it search for the nearest 3 neighbour using cosine similarity in Pinecone index.
* Now these documents are passed as context to ChatGPT API with the below prompt and temperature as 0 and max_tokens as 800

```
You are given a paragraph and a query. You need to answer the query on the basis of paragraph. If the answer is not contained within the text below, say "Sorry, I don't know. Please try again."

P: {documents}
Q: {query}
A:
```
* Answer retrieved from ChatGPT API is shown to the user.

# Setup Instructions

* First make sure that you python3, python-virtualenv and setup tool installed on the system.
* Next clone the repo

```
git clone https://github.com/embedstore/langchain-pinecone-chat-bot.git
```

* Now create a virtual environment and install all the dependencies

```
cd langchain-pinecone-chat-bot
virtualenv -p $(which python3) pyenv
source pyenv/bin/activate

pip install -r requirements.txt
```

* Now copy the env file and fill in your variables

```
cp .env.sample .env
```

* The `EMBEDDING_ID` variable is the id of the embedding which you can get from [embedstore.ai](https://embedstore.ai)

* Now run the app

```
python main.py
```

* You can also create a repl and import the repo and run it easily over there.

# License

* MIT License