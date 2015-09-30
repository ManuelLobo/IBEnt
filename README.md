# IBEnt
Framework for identifying biomedical entities

## Dependencies:
* Pre-processing:
    * [Genia Sentence Splitter](http://www.nactem.ac.uk/y-matsu/geniass/)
    * [Python wrapper for Stanford CoreNLP](https://bitbucket.org/torotoki/corenlp-python)
* Term recognition
    * [Stanford NER 3.5.X](http://nlp.stanford.edu/software/CRF-NER.shtml)
* Relation extraction
    * [SVM-light-TK](http://disi.unitn.it/moschitti/Tree-Kernel.htm)
    * [Shallow Language Kernel](https://hlt-nlp.fbk.eu/technologies/jsre)
* Local [ChEBI](https://www.ebi.ac.uk/chebi/) MySQL database
    * Required ChEBI tables: term, term_synonym, word2term3, word3, descriptor3, SSM_TermDesc, graph_path
* requirements.txt

## Configuration
After setting up the dependencies, you have to edit src/config.py with the MySQL information for ChEBI and GO databases.

## Usage
You can either run the system in batch or server mode.
Batch mode expects specific data formats and can be used to train classifiers and evaluate on a test set.
For example, to train a classifier models/class1.ser.gz from the data on corpus1:

    python src/main.py train --goldstd corpus1 --models models/class1
    
To test with this classifier on corpus2 and save the results to data/results1.pickle:

    python src/main.py test --goldstd corpus2 -o pickle data/results1 --models models/class1
    
To evaluate the results on the corpus2 gold standard:

    python src/evaluate.py evaluate corpus2 --results data/results1 --models models/class1

If you just want to send text to previously trained classifiers and get results, use the server mode.
Start the server with `python src/server.py` and input text with `python src/client`.
You can also use your own client, sending a POST request to the address in config.host_ip.