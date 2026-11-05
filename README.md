Data and script for Stalking the Social Lives of Sea Turtles: the prevalence, duration, and activity of interactions between three sympatric sea turtle species 

Scripts for data cleaning, processing, and analysis can be found on GitHub at https://github.com/soph-eclaire/InteractionsProject
Data cleaning and processing was completed using InteractionsDataCleaningProcessing_Final.Rmd
Data analysis was completed using Interactions_Analysis.Rmd

Data was collected via animal-borne CATS camera tags to opportunistically observe and analyze behavioral interactions between three sympatric sea turtle species in a critical foraging habitat off the Gulf coast of Florida, USA. The data was broken into two sets: (1) behavioral annotations taken from video footage; and (2) movement data collected via several sensors embedded within the tags [most importantly to this analysis, dynamic body acceleration (DBA) computed from a tri-axial accelerometer].

merged_interactions_annotations.csv is the complete raw dataset of video annotations, completed in behavioral analysis software Boris. The beginning of the data cleaning/processing script focuses on cleaning up this data, including applying actual date/times to behaviors (as opposed to time in "seconds into the video"), and appropriately labelling modifiers (additional information collected for a behavior within Boris, e.g., the interactive behaviors observed for a turtle during "Species interaction" behavior). The final cleaned producted is clean.behavior.data.2023.to.2026.csv.

The movement data is then introduced (allsensdata_new.csv, divephases_new.csv, adjusteddives_new.csv) to be merged in and aligned with the behavior data but date/time. 
