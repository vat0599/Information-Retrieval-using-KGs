# Information-Retrieval-using-KGs
The problem statements is to formulate raw sentences into a knowledge graph using natural language processing and retrieve information for the same. In this process, if a person searches for any keyword which is present in the database, then the model should retrieve all the necessary nodes and create a knowledge graph out of it, so that it can be visualized by the user.

## Dataset used:
In this project, a custom dataset of 4300 lines is stored in a csv file. This file consists of a compilation of over 500 Wikipedia articles of varied topics. One thing to pay attention is this dataset is specifically prepared with exactly two entities – one subject and one object. The purpose of this formatting is for sentence segmentation which is seen in next section. This is just a sample dataset and there is no harm in using dataset from DBpedia or Wikidata or Freebase.

## Steps to implement the code:
- Clone the repo.
- Make sure the dependencies are downloaded and keep the wiki_sentences file in the same directory as the ipynb file.
- Execute ipython notebook.

## Algorithm Flow:
Given text is segmented into sentences, which then sent to entity extraction in which the subject and object present in a sentence is taken out and stored. Next, we concentrate on the relation/predicate extraction in which the joining word or the root word or the semantic of the sentence is taken as the edge. Once this done, we then finally visualize them in a graph format so that the user can have a better understanding of the passage.

Now lets look at each step in little detail:
### Sentence Segmentation:
Sentence segmentation is the process of splitting the text document or article into sentences. Then, these sentences are shortlisted only where there is exactly one subject and one object.

This can be seen in below example.

<img src='https://user-images.githubusercontent.com/41820878/104224630-41f8f280-546b-11eb-82ac-8147890a241a.png'>

### Entities Extraction:
The extraction of a single word entity from a sentence is not a tough task. This can easily do this with the help of parts of speech (POS) tags. The nouns and the proper nouns are taken as the entities. However, when an entity spans across multiple words, then POS tags alone are not sufficient. We need to parse the dependency tree of the sentence.

This is where the importance of spacy comes in. Spacy works on rule-based matching, in which the structure of the sentence is understood. For example, X such as Y is one such pattern, where the type of Y is found out from X and stored in the data frame.

Some examples are countries like Vietnam or fruits such as apple, flowers such as rose. There are a lot more rules prebuilt in the library and this effectively understands all possible meanings and nuances present in a sentence. Once this data frame is created, we proceed to the next stage of extraction relation.

### Extraction Relation:
To build a knowledge graph, the most important things are the nodes and the edges between them. These nodes are going to be the entities that are present in the sentences.
Edges are the relationships connecting these entities to one another. We will extract these elements in an unsupervised manner, i.e., we will use the grammar of the sentences. The main idea is to go through a sentence and extract the subject and the object as and when they are encountered.

After we construct knowledge graph for few sentences, our remaining work is to create a knowledge graph for chunk of lines, or a paragraph or an article. One catch here is, these are not individual sentence, but a group of sentences, carrying a theme or a concept. So, it is important to understand the relation and context behind the lines, so that similar sentences can be mapped to the existing graph.

This leads us to the next and final stage, the relation /predicate extraction.

### Relation/Predicate Extraction
Using the hypothesis that the predicate is actually the main verb in a sentence the relation extraction is performed. This is because throughout the English language it is seen that the verb carries the heart of the sentence. The gist of any sentence can be understood by the verb in the sentence. Apart from the common verbs like is, was, are, which carries no informative significance, other verbs in the sentence has key role in formatting the knowledge graph. It commonly seen that a Google search of who is the winner of the 2011 cricket world cup redirects with a single answer of “India”. This is because the search engine understood the verb “won” in the sentence and searched for the answer from its knowledge base and returned the with the answer.

Table below shows the most frequent relations or predicates that has been extracted from the custom dataset. This differs from dataset to dataset.

<img src='https://user-images.githubusercontent.com/41820878/104227315-314a7b80-546f-11eb-9d71-2b41afc96d26.png'>

This is where the need of spacy comes. Spacy automatically adds the probable relations and interconnects graphs based on its vector distance of similarity, thus forming a huge blob of interconnected nodes.

Figure below shows the interconnected graphs after the model learnt the entire 4300 words from the csv file. This is however little tedious to read and understand also derive useful information from. Thus, there is this package called networkx which is imported in the code to manipulate with the knowledge base formed. Networkx has these special functions like from_pandas_edgelist() which is responsible for creating the nodes and connecting them through lines as we seen below. This is again recursively called by MultiDiGraph() function which takes care of having interconnections between different nodes lines in the paragraph.

<img src='https://user-images.githubusercontent.com/41820878/104227383-4fb07700-546f-11eb-9af0-6bcf175b8e9d.png'>

After this is sorted, we can have a neater version where we can interpret some useful information has the title of the project suggests. This can be done specifying the verb or the relation which we are interested to look upon. For example, if we choose a relation of `composed by` then we get to see all the music directors, genre of songs released by the same and other relevant details. This is what shown in the figure below.

<img src='https://user-images.githubusercontent.com/41820878/104227592-ab7b0000-546f-11eb-9d08-950b12e4527e.png'>

## Contributions
Do not hesitate to contribute by [filling an issue](https://github.com/vat0599/Information-Retrieval-using-KGs/issues) or [a PR](https://github.com/vat0599/Information-Retrieval-using-KGs/pulls) !
