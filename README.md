# Topic Classification for ESRF experiment proposals
## Background
This work develops a data pipeline to assign topics to the European Synchrotron Radiation Facility (ESRF) experiment proposals, with broader applications to other Photon and Neutron (PaN) facilities.

To use the facilities provided by PaN institutes, potential users have to submit a proposal which will be reviewed. Once approved, the users can then carry out their experiments and possibly publish the results of the experiments. Note that a single proposal could lead to multiple experiment sessions.

Currently, there exist only high-level topic classifications for these proposals. This work aims to provide topics with a greater level of granularity, and to evaluate the feasibility of a real-time topic classification system at the proposal submission stage for PaN facilities.

The OpenAlex team [1] developed a model and topics vocabulary to classify publications and add them to their growing data repository. The model can be repurposed to classify the experiment proposals instead.

## Methodology
The model developed by the OpenAlex team uses the **Title**, **Abstract**, **Referenced works** (the works that the publication cites), and **Journal name** of the publications to make the topic predictions. 

Similarly, experiment proposals also have **Title** and **Abstract**, which are currently not openly available. However, they are reused in the experiment session metadata, although certain experiment sessions may have a manually created **Title** and **Abstract**. Hence, we gather all the **Title** and **Abstract** metadata from the experiment sessions, remove any duplicates, and concatenate the rest into one big **Title** and one big **Abstract**. 

For **Referenced works**, the references cited wthin a proposal are extracted in a structured manner using the GROBID tool [2].

The **Journal name** is not relevant for experiment proposals. However, we use the **Subject** metadata of the experiment sessions as a substitute. The rationale is that journal names often contain subject-related keywords (e.g. Journal of Synchrotron Radiation is about synchrotron-related research), so the **Subject** metadata would provide similar contextual information when tokenised and encoded into embeddings by the machine learning model.

<img width="613" height="461" alt="image" src="https://github.com/user-attachments/assets/3ab9a832-05f5-4ac4-b8d7-74a351688744" />

The code for the model has been copied from the [OpenAlex GitHub repository](https://github.com/ourresearch/openalex-topic-classification).

## How to use
Download the model artifacts from the Zenodo page [3]. All the other necessary data files are in the Datasets folder. 

There are three Jupyter Notebooks, **Data Processing.ipynb** for importing and processing data, **Grobid.ipynb** for extracting structured information from ESRF experiment report PDFs, and **Topic classification.ipynb** (together with **predictor.py**) for the actual implementation of the model. In order to run these three Notebooks, it is recommended to create a virtual enviroment and install packages using the requirements.txt (which is the one provided on the OpenAlex GitHub repository with some additional packages added to it).

The full dataset of proposals with the corresponding topic predictions can be found in the Datasets/Predictions folder. All intermediate datasets are saved in the Datasets/Checkpoint_data folder. The outputs of **Grobid.ipynb** can be found in the Datasets/GROBID_web_Services_results folder in the form of a zip file.

## Evaluation exercise
An evaluation was carried out for "PDF metadata only" proposals, as they are representative of what information can be expected to be present at the proposal submission stage. In other words, this exercise is mainly focused on evaluating the feasibility of a theoretical live topic classification service.

18 domain experts reviewed 209 proposals and the associated topic predictions. The domain experts cover the entire specturm of the 12 ESRF Scientific Disciplines. The 209 proposals were selected based on having non-null data fields (Title, Abstract, References) and were found to be mostly representative of the population proposals. Each proposal was reviewed by three separate reviewers to mitigate individual subjectivity and ensure scientific rigour.

The reviewers were provided with the Title and Abstract (along with other supplementary information such as references and beamline) and tasked to evaluate each topic prediction by selecting 'Relevant', 'Unclear', and 'Not relevant' from a dropdown menu. This information allowed us to measure the inter-rater agreement and overall model performance in the context of a live service.

We found that the reviewers were largely in agreement, albeit with noticeable levels of dissent, demonstrating the subjective and challenging nature inherent to such a task even for domain experts. The model was found to be suitable for a live service setting where the proposal authors are present to provide real-time verification. However, it's performance is not good enough for back-classification of historical proposal documents with no human expert oversight.

The set of 209 proposals can be found in the 'proposals_for_validation.json' file. 
The full set of evaluations can be found in the 'results_spreadsheets.xlsx' file. 
The 'Data analysis.ipynb' notebook was used to analyse the reviewer evaluations.

The first two files can be found in the Datasets/Evaluation_exercise folder.
The Jupyter notebook can be found in the Code folder.


## References
[1] Priem, J., Piwowar, H., & Orr, R. (2022). OpenAlex: A fully-open index of scholarly works, authors, venues, institutions, and concepts. ArXiv. <https://arxiv.org/abs/2205.01833>

[2] GROBID (2008-2025) <https://github.com/kermitt2/grobid>

[3] Barrett, J. (2024). OpenAlex Topic Classification v1 Model Artifacts and Training Data [Data set]. Zenodo. <https://doi.org/10.5281/zenodo.11235511>
