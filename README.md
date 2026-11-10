**Data and script for Stalking the Social Lives of Sea Turtles: the prevalence, duration, and activity of interactions between three sympatric sea turtle species**

Scripts for data cleaning, processing, and analysis can be found (here) on GitHub at https://github.com/soph-eclaire/InteractionsProject and at https://doi.org/10.5281/zenodo.24015669

Full dataset used can be found at https://doi.org/10.5281/zenodo.24117513

Data cleaning and processing was completed using _InteractionsDataCleaningProcessing_Final.Rmd_

Data analysis was completed using _Interactions_Analysis.Rmd_

Data was collected via animal-borne CATS camera tags to opportunistically observe and analyze behavioral interactions between three sympatric sea turtle species in a critical foraging habitat off the Gulf coast of Florida, USA. The data was broken into two sets: (1) behavioral annotations taken from video footage; and (2) movement data collected via several sensors embedded within the tags [most importantly to this analysis, dynamic body acceleration (DBA) computed from a tri-axial accelerometer].

**Working through the script**

_merged_interactions_annotations.csv_ is the complete raw dataset of video annotations, completed in behavioral analysis software Boris. The beginning of the data cleaning/processing script focuses on cleaning up this data, including applying actual date/times to behaviors (as opposed to time in "seconds into the video"), appropriately labelling modifiers (additional information collected for a behavior within Boris), differentiating interaction behavior events by interaction type, correcting for time discrepencies (frame rate differences, time change for EST vs EDT), and transforming data from long to wide format. 

For videos where a turtle's release was caught on camera, release time (taken from the clock in the bottom right corner of the video) was noted in the Boris annotations as "release time" behavior; however, this was not possible for some deployments where the camera did not record the exact release. As such, a release time was taken from our capture database and added to the dataset via _MissingReleaseTimes.csv_ during data cleaning/processing. 

The final cleaned product for the behavior data is _clean.behavior.data.2023.to.2026.csv_.

The movement data is then introduced (_allsensdata_new.csv, divephases_new.csv, adjusteddives_new.csv_) to be merged in and aligned with the behavior data by date/time. First, these three files are merged together to create final.movement.data.csv. This csv is then merged with _clean.behavior.data.2023.to.2026.csv_. This is the full dataset of behavior and movement data for the turtles included in this study, only including data from the windows of time where there is both video annotation and sensor data to analyze (e.g., overnight sensor data where there was no accompanying video footage due to light constraints is filtered out at this point).

From here, prior to completing any analysis, some behaviors are merged together (searching and foraging; types of swimming) and the first three hours of data collected post-release for each individual is filtered out to account for any residual stress related to capture/handling. 

Mean DBA is then computed for each occurrence of a behavior for each individual to prepare data for DBA analysis. This produces the final, cleaned dataset _full.CATS.data.csv_, ready to be used in the analysis script.

The _Interactions_Analysis.Rmd_ script is broken down by individual analysis, working through time budgets, interaction counts, interaction duration, and DBA one by one, including any further data wrangling, analyses, and plotting/figure creation.


**Files and Variables**

**merged_interactions_annotations.csv**

_Description:_ complete raw dataset of video annotations for data collected from 2023 to 2026, completed in behavioral analysis software Boris

_Variables:_
*Note: only the variables/data used in the analysis for this project are listed below. 
- Observation.id - Observation ID, including deployment number and number of particular video (e.g., CC-11-11_CR12_4 indicated camera CC-11-11, deployment 12, video 4)
- Observation.date - Date and time observation was completed in Boris - not the date/time of the actual footage
- Observation.duration - Length (s) of video annotated
- Observation.type - Media file, indicating a media file was uploaded to Boris for annotation
- Source - Filepath of video annotated
- Media.duration..s. - Full length (s) of video
- FPS - Frame rate video was played at
- Subject - Subject behaviors were annotated for. Generally NA, as video were not originally annotated for multiple subjects, and only for the tagged ("focal") turtle. However, as interactions were annotated for both the focal and observed turtles, observed turtles were added as subjects to differentiate behavior between individuals. CATS turtle as a subject is added in later data cleaning/processing to replace the blanks/NAs.
- Behavior - Behavior annotated as occurring (swimming, foraging, etc)
- Behavioral.category - Some behaviors share a category (e.g., active and passive swim are both "swim"). For some behaviors, the category is the same as the behavior (e.g., rest)
- Behavior.type - Point or start/stop; point events are one point in time (e.g., marking the time to note the actual time of day in hh:mm:ss taken from the clock in the bottom right corner of the video), start/stop events have a duration, and thus a start/stop.
- Time - Time into video (s) behavior was marked; later transformed into a date/time using actual release data and the time noted in Modifier..1 column for "Time" behavior (hh:mm:ss)
- Media.file.name - Filepath of video annotated
- Comment - Any additional comments aded for the behavior annotation
- Modifier..1 through Modifier..10 - Additional data collected for a behavior. Modifiers 1-5 may be different depending on the behavior; for example, for foraging behavior, Modifier 1 may indicate the foraging location (benthic, pelagic, or surface), while for species interactions, it is the species of the other turtle the subject turtle is interacting with. Modifiers are split up by behavior and transformed throughout the beginning of the cleaning/processing script to include actual labels (e.g., interactive behaviors)
  
**clean.behavior.data.2023.to.2026.csv**

_Description:_ cleaned behavior data, ready to merge with movement/sensor data.

_Variables:_
- DeployID - Deployment number 
- ObservID - Observation number (deployment number_video number from that deployment)
- BehStartTime - Start time of the behavior (mm/dd/yy hh:mm:ss)
- BehStopTime - Stop time of the behavior (mm/dd/yy hh:mm:ss)
- BehDuration _ Durtaion (s) of the behavior
- ObsStartTime - Start time (mm/dd/yy hh:mm:ss) of the individual video
- ObsEndTime - End time (mm/dd/yy hh:mm:ss) of the individual video
- Subject - Subject behavior was annotated for; mostly CATS turtle, except for interactions, where behavior was also annotated for observed turtle(s)
- SpeciesSubject - Sea turtle species of the given subject (Loggerhead, Green, or Kemp's ridley)
- LifeStageSubject - Estimated lifestage of the given subject (juvenile, subadult, or adult; taken from morphometric capture data, or for observed turtles, estimated)
- SexSubject - Sex of the given subject (male, female, or unknown; taken from morphometric capture data, or for observed turtles, estimated)
- BodyConditionSubject - Estimated body condition of the given subject (poor, good, or robust; taken from morphometric capture data, or for observed turtles, estimated)
- SignsDiseaseInjurySubject - Any notable signs of disease/injury for the given subject (e.g., fibropapillomatosis, flipper or carapace injury; marked as either yes, no, or unclear)
- ReleaseTime - Time (mm/dd/yy hh:mm:ss) tagged turtle was released
- Behavior - Behavior (swimming, fraging, resting, etc)
- BehavCat - Some behaviors share a category (e.g., active and passive swim are both "swim"). For some behaviors, the category is the same as the behavior (e.g., rest)
- InteractiveBehaviorsSubject - For species interaction behavior, the interactive behaviors exhibited (e.g., approach, inspect, biting, chasing)
- PreviousBehavior - Behavior turtle was engaging in prior to an interaction
- NextBehavior - Next behavior the turtle engages in after an interaction
- SpeciesInteractingWith - Species the subject is interacting with (loggerhead, green, or Kemp's ridley; if the tagged turtle was a loggerhead and observed turtle a green, when subject is CATS turtle, this will be green; when subject is Observed turtle (n) this will be loggerhead)
- InteractionWinner - If an aggressive interaction has a clear winner (e.g., one turtle "wins" a contest resource, chasing th eother out), the appropriate subject is indicated here (though this was not used in final analyses)
- AggressionInitiator - For an aggressive interaction, which subject initiated the aggression
- InteractionBottomTypeStart - Habitat bottom type (seagrass, hard bottom, sandy bottom, or mixed) at the start of an interaction
- InteractionBottomTypeEnd - Habitat bottom type (seagrass, hard bottom, sandy bottom, or mixed) at the end of an interaction
- InteractionHabitatStart - Habitat (structured or unstructured) at the start of an interaction
- InteractionHabitatEnd - Habitat (structured or unstructured) at the end of an interaction
- InteractionDepthStart - Depth (bottom, midwater, or surface) at the start of an interaction
- InteractionDepthEnd - Depth (bottom, midwater, or surface) at the end of an interaction
- Behavior.type - Point or start/stop; point events are one point in time (e.g., marking the time to note the actual time of day in hh:mm:ss taken from the clock in the bottom right corner of the video), start/stop events have a duration, and thus a start/stop.
- Source - Filepath of video annotated
- InteractionType - For species interactions, the type of interaction (passive, active, or aggressive), determined based on interactive behaviors exhibited by the focal (CATS) turtle
- DeployNum - Unique deployment number, one for each deployment
- BehavID - Numbers assigned to each behavior (e.g., swimming is 1, breathing is 2)
- Segment - Number of the occurrence of a behavior for an individual (e.g., first swimming event for deployment number 1 is "1", second swimming event for deployment 1 is "2")
- pair_id - Used to transform data from long to wide format

**allsensdata_new.csv**

_Description:_ Sensor data was loaded into the script as allsensdata_new.csv, which was already processed using the processing script from https://doi.org/10.1186/s40317-025-00406-4, found at https://zenodo.org/records/20147018 . From here, it was merged in/aligned with the behavior data using the below variables.

_Variables:_
*Note: only the variables/data used in the analysis for this project are listed below
- DeployID - Deployment number
- DT - The date/time (mm/dd/yy hh:mm:ss), used to align this data with the behavior dataset
- DBA - Dynamic body acceleration value, recorded via tri-axial accelerometer (and computed in the processing script); one row for every 2 s


