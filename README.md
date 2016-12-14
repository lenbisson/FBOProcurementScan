# FBO Procurement Scan
### A program for predicting which solicitations are likely to not be in conformance with Section 508 requirements

##### About Section 508 Procurement Review
Section 508 of the Rehabilitation Act of 1973 mandates that all government technology be made accessible to persons with disabilities. For example, government websites are supposed to be built to be compatible with screen-reading software so that the page's information and functionalities are accessible to the visually-impaired.

The government contracts with private companies for services and projects quite often. When the government enters into a contract, it is important that the requirements relating to Section 508 be clearly spelled out. Ultimately, the government is responsible for ensuring that new products are accessible, so companies can only be held accountable for not producing accessible products if the accessibility requirements were explicitly defined in the legal documents relating to the contract. These legal documents are listed publicly on [FedBizOpps]('https://fbo.gov'), a GSA website that serves as one of the central points where contracting opportunities are listed (it is not the only source, but it is the largest). 

A part of GSA's Section 508 Program is to assist agencies in performing solicitation review, a process by which experts in Section 508 law review new procurement documents as they are posted to FedBizOpps for conformance with Section 508 requirements. This is a daunting task, as FedBizOpps often sees in excess of 500 new opportunities posted every day, including even weekends and holidays. 

This program was written as an aide to those performing this soliciation review process. GSA has been centrally reviewing a sample of solicitations (an average of 20-40 per month) since 2009. This left us with a large set of data: past procurements and their level of conformance (graded as 'red' for entirely non conformant, 'green' for fully conformant, and 'yellow' for partially conformant). We began by collecting documents from the graded procurements, parsing them into raw text, then applying several Natural Language Processing (NLP) techniques to tokenize, lemmatize (revert a word to its basic form), and vectorize the text. With the vectorized text, we trained several well-known machine learning algorithms to look for patterns associated with green vs. yellow vs. red procurements, then scored the models using [k-folds cross validation]('https://en.wikipedia.org/wiki/Cross-validation_(statistics)#k-fold_cross-validation'). 

The final piece was a module for pulling new solicitations from FedBizOpps, parsing/vectorizing their documents, and predicting their level of conformance based on the outputs of the trained machine learning algorithms. 

The outputs here should **NOT** be taken as an official evaluation of the conformance level of a document. This project is still in its alpha stage, and even when the program is in a production phase, machine learning can only take one so far in evaluating procurements. It is still vital that procurements be reviewed by Section 508 SMEs in order to make a definitive determination. The purpose of this tool is to act as a filter, aiding 508 SMEs in finding the solicitations most likely to not be in conformance with Section 508, so that they can be further evaluated and so that amendments can be made before the solicitation closes. 

##### System Requirements
The bulk of this program is written in Python 3.4.3. It has not been tested in a Python 2.x environment, though it would likely work with some minor adjustments. The path variables in the program are written with a Unix/Linux operating system in mind, so some edits will be needed to run this program on a Windows machine (notably changning the ```/``` characters in paths to ```\```).

For document parsing, the program uses Textract, a Python library for parsing most types of documents into plain text. As of this writing, Textract is not optimized for use with Python 3.4.3, so you will need to make some edits to the base libraries to run this tool. Instructions to follow shortly.

You will also need to have Node.js and npm installed on the machine that is running the software. Further instructions on this can be found in ```scripts/pull```.
