# Topic Classification for ESRF experimental proposals
## Data files

Checkpoint data:

* Publications_ESRF.csv: all publications collected by the ESRF. Includes publications that resulted from experiments done at the ESRF.

* session_esrf_valid_with_subj.json: list of ESRF experiment sessions with the following metadata:
    + DOI
    + Title
    + Summary (Abstract)
    + Associated proposals (proposal number and PDF document name)
    + Subject (ESRF Scientific Discipline)
    + Instrument (ESRF beamlines)

* Proposals_ESRF_base: list of ESRF proposals with the following metadata:
    + Proposal number
    + Summary (Aggregated summaries/abstracts from associated experiment sessions; there is a many-to-one relation between 'session_esrf_valid_with_sub' and 'Proposals_ESRF_base'.)
    + Title (aggregated in a similar manner to Summary)
    + Subject (ESRF Scientific Discipline)
    + Instrument (ESRF beamlines)
    + Experiment session DOI(s)
    + PDF name(s)

* PDF_metadata.json: References (with DOIs) and additional abstract information extracted from the experiment report PDFs using GROBID.

* Proposals_ESRF_PDF_metadata_only.json: list of proposals with the following metadata:
    + Proposal number
    + Summary (the additional abstract information from 'PDF_metadata' appended to Summary of 'Proposals_ESRF_base')
    + Title (aggregared in a similar manner to Summary)
    + Subject (ESRF Scientific Discipline)
    + Instrument (ESRF beamlines)
    + Experiment session DOI(s)
    + PDF name(s)
    + Reference DOIs from 'PDF_metadata' 
    + OpenAlex IDs for the references

* Proposals_ESRF_publications_only_doi.json: list of proposals with the following metadata:
    + Proposal number
    + Summary (same as Summary of 'Proposals_ESRF_base')
    + Title (same as Title of 'Proposals_ESRF_base')
    + Subject (ESRF Scientific Discipline)
    + Instrument (ESRF beamlines)
    + Experiment session DOI(s)
    + PDF name(s)
    + Publications DOI; each proposal/experiment session can lead to publications, we aggregate all the associated publications for each proposal

* Proposals_ESRF_publications_only.json: same as 'Proposals_ESRF_publications_only_doi' but with an additional 'OpenAlex IDs' column:
    + Proposal number
    + Summary (same as Summary of 'Proposals_ESRF_base')
    + Title (same as Title of 'Proposals_ESRF_base')
    + Subject (ESRF Scientific Discipline)
    + Instrument (ESRF beamlines)
    + Experiment session DOI(s)
    + PDF name(s)
    + Publications DOIs; each proposal/experiment session can lead to publications, we aggregate all the associated publications for each proposal
    + OpenAlex IDs for the publications

* Proposals_ESRF_combined.json: 'Proposals_ESRF_PDF_metadata_only' and 'Proposals_ESRF_publications_only' combined together:
    + Proposal number
    + Summary (the additional abstract information from 'PDF_metadata' appended to Summary of 'Proposals_ESRF_base')
    + Title (aggregared in a similar manner to Summary)
    + Subject (ESRF Scientific Discipline)
    + Instrument (ESRF beamlines)
    + Experiment session DOI(s)
    + PDF name(s)
    + Reference DOIs from 'PDF_metadata' 
    + OpenAlex IDs for the references
    + Publications DOIs; each proposal/experiment session can lead to publications, we aggregate all the associated publications for each proposal
    + OpenAlex IDs for the publications
    + Combined list of OpenAlex IDs (IDs for the references and the publications)


Predictions:

* Proposals_ESRF_Predictions_PDF_metadata_only.json: list of proposals with Topic predictions:
    + Title
    + abstract_inverted_index (basically Summary; renamed to follow the OpenAlex model's naming convention)
    + OpenAlex IDs for the references
    + journal_display_name' (basically Subject/ESRF Scientific Discipline)
    + inverted: boolean to indicate if the abstract_inverted_index is an inverted index (True) or just normal text
    + Proposal number
    + Instrument (ESRF beamlines)
    + Experiment session DOI(s)
    + PDF name(s)
    + Reference DOIs from 'PDF_metadata' 
    + Topic predictions
         - Topic ID
         - Topic label
         - Topic score (model's confidence in the prediction)

* Proposals_ESRF_Predictions_publications_only.json
    + Title
    + abstract_inverted_index (basically Summary; renamed to follow the OpenAlex model's naming convention)
    + OpenAlex IDs for the publications
    + journal_display_name' (basically Subject/ESRF Scientific Discipline)
    + inverted: boolean to indicate if the abstract_inverted_index is an inverted index (True) or just normal text
    + Proposal number
    + Instrument (ESRF beamlines)
    + Experiment session DOI(s)
    + PDF name(s)
    + Publications DOIs
    + Topic predictions
         - Topic ID
         - Topic label
         - Topic score (model's confidence in the prediction)

* Proposals_ESRF_Predictions_combined_all.json: 'Proposals_ESRF_Predictions_PDF_metadata_only' combined with 'Proposals_ESRF_Predictions_publications_only':
    + Title
    + abstract_inverted_index (basically Summary; renamed to follow the OpenAlex model's naming convention)
    + journal_display_name' (basically Subject/ESRF Scientific Discipline)
    + inverted: boolean to indicate if the abstract_inverted_index is an inverted index (True) or just normal text
    + Proposal number
    + Instrument (ESRF beamlines)
    + Experiment session DOI(s)
    + PDF name(s)
    + Reference DOIs from 'PDF_metadata' 
    + OpenAlex IDs for the references
    + Publications DOIs
    + OpenAlex IDs for the publications
    + Combined list of OpenAlex IDs (IDs for the references and the publications)
    + Topic predictions
         - Topic ID
         - Topic label
         - Topic score (model's confidence in the prediction)




## Summary of the main files
* Publications_ESRF.csv: All publications collected by the ESRF. Includes publications that resulted from experiments done at the ESRF.

* Proposals_ESRF_base.json: ESRF proposals with summary, title, subject, instrument,experiment session doi, and PDF document name.

* Proposals_ESRF_publications_only_doi.json: ESRF proposals with publication DOIs only, no corresponding OpenAlex IDs.

* Proposals_ESRF_publications_only.json: The above but with OpenAlex IDs.

* Proposals_ESRF_Predictions_PDF_metadata_only.json: Proposals with PDF metadata and corresponding topic predictions.

* Proposals_ESRF_Predictions_publications_only.json: Proposals with publications and corresponding topic predictions.

* Proposals_ESRF_Predictions_combined_all.json: Proposals with PDF metadata and publications, includes topic predictions with PDF metadata only, publications only, and combined PDF metadata and publications.