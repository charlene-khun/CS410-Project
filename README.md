# Project Overview
This project focused on improving the online shopping experience by helping users identify relevant electronics products more efficiently on Amazon. The business problem was that customers can face information overload when searching through large numbers of products and reviews, making it difficult to determine which items best match their needs. To address this, our team built a Chrome extension that allows users to enter a natural-language product query and receive a relevant recommendation directly while browsing Amazon. The system used an electronics dataset based on Amazon product metadata and reviews, along with a local Retrieval-Augmented Generation (RAG) pipeline powered by Ollama models.

The primary stakeholders were online shoppers who need a faster and more convenient way to evaluate product options, as well as e-commerce platforms interested in improving product discovery and customer engagement. The project supports the purchasing decision by taking a user's query, retrieving relevant product information from the indexed electronics dataset, and presenting a similar or suitable product through the Chrome extension. Behind the application, the team also developed scripts to reduce, clean, combine, and transform the raw Amazon review and product data into a corpus that could be indexed and searched by the RAG system.

The significance of the project is that it demonstrates how unstructured customer review and product data can be transformed into useful information for consumer decision-making. Rather than requiring shoppers to manually read many product listings and reviews, the system uses information retrieval and generative AI to surface products that better align with the user's stated needs. From a data perspective, the project also highlights the importance of data preparation, indexing, retrieval, and user-facing presentation in building an AI application, showing how cleaned and organized data can ultimately support faster, more informed purchasing decisions.

# Documentation
Please see our documentation of the code in the documentation folder of our github. Here: https://github.com/uiuc-msynowiec/CS410-Project/tree/main/Documentation. Below are the instructions on how to run our code.

# Running the local RAG program

## Requirements
Make sure you have Ollama installed. If not, go to this link and install it: https://ollama.com/download. Furthermore, once installed go to Terminal or CommandPrompt and enter this command to double check the version: "ollama --version". If the version is something like 0.13.x, then you should be good to go. Follow this by pulling the following models from ollama: "ollama pull nomic-embed-text" and "ollama pull llama3.1"

## Step 1
Clone the Github Repo, and open it up in VSCode

## Step 2
Pull up the repo in a File Explorer/Finder window and navigate to the /CS410-Project/rag_proj/reviewsset/ folder. THIS HAS TO BE THE UNZIPPED FOLDER.

## Step 3
Once here, double click on the Electronics_combined_10000.zip file. This will uncompress the file which is ok.

## Step 4
Once the file has been unzipped, copy the file and put it under this path instead: /CS410-Project/rag_proj/reviews_extracted/reviewsset/Electronics_combined_10000.zip_extracted

## Step 5
Once the unzipped file has been moved to the correct folder, remove the file from this path as it is no longer necessary: /CS410-Project/rag_proj/reviewsset/, and go back to the terminal in VSCode and navigate to the rag_proj folder within the overall repo.

## Step 6
Here now run the command "python ragpipeline.py"

## Step 7
If you'd like the program to reindex everything type "y" when prompted, else if you've run the program before, there should be an index saved and you can just press "n".

## Step 8
Type "exit" to quit the program whenever and enjoy using the program!

# 🚀 Loading the Chrome Extension

## 1. Open the Extensions Page
Go to: chrome://extensions

## 2. Enable Developer Mode
Toggle **Developer mode** in the top-right corner.

## 3. Load the Extension
Click **“Load unpacked”** and select your amazonextension3.0 folder.

## 4. Start Ollama and the RAG server
To start ollama type:
ollama serve

To start the RAG server, run it from the rag_proj directory:
python ragpipeline_server.py

## 5. Test It
Go to [https://www.amazon.com](https://www.amazon.com) and verify that your extension works (e.g., banner appears or logo changes).



#  Running Chrome Extension
## Step 1: 
Once the extension is loaded and you are in the page "amazon.com" type in a query that is related to electronics (i.e... what is good electronics for a 20 year old.)
## Step 2: 
Click on the button, "Run extension logic". In our latest Chrome Extension, click on the button that says "Ask AI".
## Step 3: 
A similar item based on the query should appear in the status section of the chrome extension.
## Step 4: 
The user can click on Settings and has the option to change to either light or dark mode based on their preference.

# Running the Cleaning Scripts
The cleaning scripts have been batched into two sets. There are two versions of the scripts, one for a small dataset of 1000 items (process.bat and process_2.bat) and one for a larger set of 10000 items (process_10000.bat and process_2_10000.bat). The original dataset will need to be downloaded from the website below.

Intermediate versions of the files have been zipped and placed in the dataset_tools directory.

## Step 1
Download the electronics dataset and place it in the dataset_tools directory. The data can be found on the following site:
https://amazon-reviews-2023.github.io/

Direct links to the metadata and reviews datasets are here:
https://mcauleylab.ucsd.edu/public_datasets/data/amazon_2023/raw/review_categories/Electronics.jsonl.gz
https://mcauleylab.ucsd.edu/public_datasets/data/amazon_2023/raw/meta_categories/meta_Electronics.jsonl.gz

## Step 2
The first batch step consists of generating a smaller set from the 
dataset_tools\process.bat - run this script to generate a set of 1000 items
dataset_tools\process_10000.bat - run this script to generate a set of 10000 items

## Step 3
The second batch step consists of cleaning the data, combining it into a single dataset and generating a corpus compatible with pyserini.
dataset_tools\process_2.bat - run this script to generate the corpus for 1000 items
dataset_tools\process_2_10000.bat - run this script to generate the corpus for 10000 items
