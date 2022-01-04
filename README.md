# TripClick Baselines with Improved Training Data

Welcome 🙌 to the hub-repo of our paper:

*Establishing Strong Baselines for TripClick Health Retrieval* Sebastian Hofstätter, Sophia Althammer, Mete Sertkan and Allan Hanbury

https://arxiv.org/abs/2201.00365

**tl;dr** We create strong re-ranking and dense retrieval baselines (BERT<sub>CAT</sub>, BERT<sub>DOT</sub>, ColBERT, and TK) for TripClick (health ad-hoc retrieval). We improve the – originally too noisy – training data with a simple negative sampling policy. We achieve large gains over BM25 in the re-ranking and retrieval setting on TripClick, which were not achieved with the original baselines. We publish the improved training files for everyone to use.

If you have any questions, suggestions, or want to collaborate please don't hesitate to get in contact with us via [Twitter](https://twitter.com/s_hofstaetter) or mail to s.hofstaetter@tuwien.ac.at

**Please cite our work as:**
````
@misc{hofstaetter2022tripclick,
      title={Establishing Strong Baselines for TripClick Health Retrieval}, 
      author={Sebastian Hofst{\"a}tter and Sophia Althammer and Mete Sertkan and Allan Hanbury},
      year={2022},
      eprint={2201.00365},
      archivePrefix={arXiv},
      primaryClass={cs.IR}
}
````

## Training Files

We publish the improved training files without the text content instead using the ids from TripClick (with permission from the TripClick owners); for the text content please get the full TripClick dataset from [the TripClick Github page](https://github.com/tripdatabase/tripclick). 

Our training files have the format ``query_id pos_passage_id neg_passage_id`` (with tab separation) and are available as a HuggingFace dataset: https://huggingface.co/datasets/sebastian-hofstaetter/tripclick-training

## Source Code

The full source-code for our paper is here, as part of our matchmaker library: https://github.com/sebastian-hofstaetter/matchmaker

We provide getting started guides for training re-ranking and retrieval models, as well as a range of evaluation setups.

## Pre-Trained Models

Unfortunately, the license of TripClick does not allow us to publish the trained models. 

## TripClick Baselines Results

For more information and commentary on the results, please see our ECIR paper.

### BM25 Top200 Re-Ranking

| Model |      BERT Instance | HEAD   ||  TORSO || TAIL ||
|--------|-------------------|-------|-|-------|--|---------------|-|
| |  | nDCG  | MRR   | nDCG  | MRR   | nDCG | MRR |
| **Original Baselines**|
| BM25                               | --                                   | .140          | .276          | .206          | .283          | .267         | .258        |
| ConvKNRM                           | --                                   | .198          | .420          | .243          | .347          | .271         | .265        |
| TK                                 | --                                   | .208          | .434          | .272          | .381          | .295         | .280        |
| **Our Improved Baselines**|
| TK                                 | --                                   | .232          | .472          | .300          | .390          | .345         | .319        |
| ColBERT                            | SciBERT                              | .270          | .556          | .326          | .426          | .374         | .347        |
|                                    | PubMedBERT-Abstract                  | .278          | .557          | .340          | .431          | .387         | .361        |
| BERT_CAT                           | DistilBERT                           | .272          | .556          | .333          | .427          | .381         | .355        |
|                                    | BERT-Base                            | .287          | .579          | .349          | .453          | .396         | .366        |
|                                    | SciBERT                              | .294          | .595          | .360          | .459          | .408         | .377        |
|                                    | PubMedBERT-Full                      | .298          | .582          | .365          | .462          | .412         | .381        |
|                                    | PubMedBERT-Abstract                  | .296          | .587          | .359          | .456          | .409         | .380        |
| Ensemble (Last 3 BERT_CAT)                                        |       | **.303**      | **.601**     | **.370**       | **.472**       | **.420** |      **.392** |



### Dense Retrieval Results


| Model    | BERT Instance                            | Head(DCTR)             |                 |                |               |               |               |
| ------------------------------------|-----------------------------|--------------|-----------------|----------------|---------------|---------------|---------------|
|                                     |            | J@10 | nDCG@10 | MRR@10 | R@100 | R@200 | R@1K  |
| **Original Baselines**|
|  BM25                               | --         | 31%         | .140            | .276           | .499          | .621          | **.834** |
| **Our Improved Baselines**|
|  BERT_DOT                           | DistilBERT | 39%         | .236            | .512           | .550          | .648          | .813          |
|                                     | SciBERT    | 41%         | **.243**   | **.530**  | .562          | .640          | .793          |
|                                     | PubMedBERT | 40%         | .235            | .509           | **.582** | **.673** | .828          |
