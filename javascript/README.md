# BagelDB NPM Client Documentation

This package is a client for interacting with BagelDB, a database service. It allows you to check the connection (ping), insert vectors into a specified index, perform a search in a given index, and get OpenAI embeddings.

## Table of Contents
- [1. Installation](#1-installation)
- [2. Initializing the Client](#2-initializing-the-client)
- [3. Ping](#3-ping)
- [4. Inserting Vectors](#4-inserting-vectors)
- [5. Searching Vectors](#5-searching-vectors)
- [6. Getting OpenAI Embeddings](#6-getting-openai-embeddings)
- [7. Storing and Searching Embeddings](#7-storing-and-searching-embeddings)
- [Examples](./examples)

## 1. Installation

1. Install the package using the command: 
   ```
   npm install bageldb-beta
   ```
   **Note**: If you encounter an error message, you may need to install Node.js and npm. Visit the [official Node.js website](https://nodejs.org/en/download/) and follow their instructions.

## 2. Initializing the Client

1. Import the client into your JavaScript file. 

   ```javascript
   const BagelDB = require('bageldb-beta');
   ```

2. Create a new instance.

   ```javascript
   const db = new BagelDB();
   ```

   **Note**: If you encounter an error, ensure that the `bageldb-beta` package is installed and spelled correctly.

## 3. Ping

1. Use `ping` to check if the connection with BagelDB's server is healthy.

   ```javascript
   db.ping()
     .then(response => console.log(response))
     .catch(error => console.error('An error occurred while pinging:', error));
   ```

   `ping` returns a promise. If successful, the response is logged. If not, an error message is logged.

   **Possible errors**: Network issues, BagelDB's server might be down. Check your internet connection and ensure BagelDB's server is running.

## 4. Inserting Vectors

1. Use `insert` to add vectors to a specified index.

   ```javascript
   const index = 'myIndex';
   const vectors = [
     {
       id: 'vec1',
       values: [0.1, 0.2, 0.3, 0.4],
       metadata: { genre: 'drama' },
     },
     {
       id: 'vec2',
       values: [0.2, 0.3, 0.4, 0.5],
       metadata: { genre: 'action' },
     },
   ];

   db.insert(index, vectors)
     .then(response => console.log(response))
     .catch(error => console.error('An error occurred while inserting:', error));
   ```

   This method returns a promise. If successful, the server's response is logged. If not, an error message is logged.

   **Possible errors**: Invalid vector format or data. Make sure your vectors follow the correct structure and the data types are correct.

## 5. Searching Vectors

1. Use `search` to find vectors in a specified index.

   ```javascript
   const index = 'myIndex';
   const vector = [1.0, 2.0, 3.0, 4.0];

   db.search(index, vector)
     .then(response => console.log(response))


     .catch(error => console.error('An error occurred while searching:', error));
   ```

   `search` returns a promise. If successful, the server's response is logged. If not, an error message is logged.

   **Possible errors**: Invalid vector or index. Ensure your vector is an array of numbers and the index exists in the database.

## 6. Getting OpenAI Embeddings

1. Use `getOpenAIEmbedding` to generate embeddings for a given input text.

   ```javascript
   const inputText = 'Sample text for embedding';

   db.getOpenAIEmbedding(inputText)
     .then(response => console.log(response))
     .catch(error => console.error('An error occurred while getting embedding:', error));
   ```

   `getOpenAIEmbedding` returns a promise. If successful, the server's response is logged. If not, an error message is logged.

   **Possible errors**: Invalid input text or missing OpenAI API key. Make sure your input text is a string and you have your OpenAI API key in your environment variables.

## 7. Storing and Searching Embeddings

1. Once you have the embeddings from OpenAI, you can store them in BagelDB using the `insert` method.

   ```javascript
   const index = 'myEmbeddingsIndex';
   const vectors = [
     {
       id: 'embed1',
       values: embedding, // Use the retrieved embedding array
       metadata: { text: inputText },
     },
   ];

   db.insert(index, vectors)
     .then(response => console.log(response))
     .catch(error => console.error('An error occurred while inserting:', error));
   ```

2. Then, you can perform a search in this index.

   ```javascript
   const vector = embedding; // Use the retrieved embedding array

   db.search(index, vector)
     .then(response => console.log(response))
     .catch(error => console.error('An error occurred while searching:', error));
   ```

   Both `insert` and `search` return a promise. If successful, the server's response is logged. If not, an error message is logged.

   **Possible errors**: Invalid vector, index, or embedding. Make sure your embeddings are an array of numbers, your input text is a string, and the index exists in the database.

## Examples

You can find an end-to-end example in the [examples/](./examples) directory. The example demonstrates the complete workflow of using the BagelDB NPM client.