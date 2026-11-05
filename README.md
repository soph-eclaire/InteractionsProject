Data and script for Stalking the Social Lives of Sea Turtles: the prevalence, duration, and activity of interactions between three sympatric sea turtle species 

Scripts for data cleaning, processing, and analysis can be found on GitHub at https://github.com/soph-eclaire/InteractionsProject
Data cleaning and processing was completed using InteractionsDataCleaningProcessing_Final.Rmd
Data analysis was completed using Interactions_Analysis.Rmd

Data was collected via animal-borne CATS camera tags to opportunistically observe and analyze behavioral interactions between three sympatric sea turtle species in a critical foraging habitat off the Gulf coast of Florida, USA. The data was broken into two sets: (1) behavioral annotations taken from video footage; and (2) movement data collected via several sensors embedded within the tags [most importantly to this analysis, dynamic body acceleration (DBA) computed from a tri-axial accelerometer].

merged_interactions_annotations.csv is the complete raw dataset of video annotations, completed in behavioral analysis software Boris. The beginning of the data cleaning/processing script focuses on cleaning up this data, including applying actual date/times to behaviors (as opposed to time in "seconds into the video"), appropriately labelling modifiers (additional information collected for a behavior within Boris), differentiating interaction behavior events by interaction type, correcting for time discrepencies (frame rate differences, time change for EST vs EDT), and transforming data from long to wide format. The final cleaned product is clean.behavior.data.2023.to.2026.csv.

The movement data is then introduced (allsensdata_new.csv, divephases_new.csv, adjusteddives_new.csv) to be merged in and aligned with the behavior data by date/time. First, these three files are merged together to create final.movement.data.csv. This csv is then merged with clean.behavior.data.2023.to.2026.csv to create the final product combined.behavior.and.movement.data.csv. This is the full dataset of behavior and movement data for the turtles included in this study, only including data from the windows of time where there is both video annotation and sensor data to analyze (e.g., overnight sensor data where there was no accompanying video footage due to light constraints is filtered out at this point).

From here, prior to completing any analysis, some behaviors are merged together (searching and foraging; types of swimming) and the first three hours of data collected post-release for each individual is filtered out to account for any residual stress related to capture/handling. This becomes the final product data.trimmed.csv.

Mean DBA is then computed for each occurrence of a behavior for each individual to prepare data for DBA analysis. This produces the final, cleaned dataset full.CATS.data.csv, ready to be used in the analysis script.


