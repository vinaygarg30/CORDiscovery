# CORDiscovery Engine
An informational retrieval and text summarization engine for COVID19 Open Dataset

### Problem Statement​ ###
With Covid-19 becoming a pandemic the research on same has also accelerated - more than 44000 research articles already published and growing. The objective is to analyze the existing literature for analysis including question, answering and summarization which helps in getting better and faster insights

### Solution Overview ###
#### Level 1: Using ensemble to create vector embeddings and rank documents
* An ensemble framework to rank the documents using various Natural Language Processing techniques – ​
    * **TF-IDF**: Determines the importance of an individual word relative to a document
    * **Topic Modeling (Latent Semantic Analysis)**: Assigns particular words to clusters (or word clouds) that contain similar terms​
    * **BERT**: Bidirectional Encoder Representations from Transformers (BERT) is a pre-trained model developed by Google. Unlike traditional RNNs or LSTMs, which only learn in one direction, BERT is trained in both directions and thus is better at understanding context. ​
    * **SciBERT**: pre-trained model on medical journal articles and would be more applicable for the existing case​
* Storing generated document embeddings in Elastic search for near real time search using Dense Vector API 
* Retrieving top N documents from the ranked ensemble

#### Level 2: Extractive summarization around the retrieved documents ####
* Generating extractive summaries using pre-trained BERT text summarizer
* It works by embedding the sentences of retrieved documents, running a clustering algorithm and finding the sentences that are closest to the cluster's centroids.

### Process Workflow ###
* Data Preparation and Wrangling
* Generation of embeddings for the document corpus for different techniques in ensemble approach
* Data/Embedding Ingestion into Elasticsearch as dense vectors
* Saving the model objects and configuration for later use
* Generation of embeddings for user search input
* Matching (input embeddings and document vectors) based on cosine similarity
* Summarizing the retrieved documents using BERT summarizer
* Displaying search results

### Setup Elasticsearch ### 
* Download and install Elasticsearch 7.6 from https://www.elastic.co/downloads/elasticsearch<br> 
NOTE: To use the Dense Vector and Script Score APIs, make sure you download the latest version _(stated above)_ for this implementation.

### Code Instructions ###
* Download the dataset (metadata.csv) from https://www.kaggle.com/allen-institute-for-ai/CORD-19-research-challenge and place in 'data' folder
* You must download the Bert and Scibert model and place them in a local folder called 'bin'
* To install the required packages _(we encourage to create a virtual environment to avoid package conflicts)_, run the following command - 
    `pip install -r requirements.txt`
* Run the jupyter notebook and navigate to code in the 'src' folder
* Once you run the notebook, a flask app will be running on http://localhost:5000 and try the following sample queries:
    * Clinical and bench trials to investigate less common viral inhibitors against COVID-19 such as naproxen, clarithromycin, and minocycline that that may exert effects on viral replication.
    * Methods evaluating potential complication of Antibody-Dependent Enhancement (ADE) in vaccine recipients.
    * Exploration of use of best animal models and their predictive value for a human vaccine.
    * Capabilities to discover a therapeutic (not vaccine) for the disease, and clinical effectiveness studies to discover therapeutics, to include antiviral agents.
    * Assays to evaluate vaccine immune response and process development for vaccines, alongside suitable animal models
 





