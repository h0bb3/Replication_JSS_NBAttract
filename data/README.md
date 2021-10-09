# Data File Format
The data files are raw csv data where each row contains the results of one mapping experiment. Each system has its own file.

## Columns
_globalId_ : a global counter id should be unique per data row.  
_date_ : the date the experiment was run  
_time_: the time of day the experiment was run  
_mappingId_: unique identifer of the mapping  
_initialClustered_: how many entities are clustered in the intial set  
_totalMapped_: how many entities that are mapped in the ground truth architecture (typically this is the same number in all experiments for the same system)  
_iterations_: how many iterations HuGMe was run  
_totalManuallyClustered_: how many entities were manually clustered (should be 0 for this dataset)  
_totalAutoClustered_: how many entities were automatically clustered  
_totalAutoWrong_: how many entities of the automatically clustered were not correct  
_totalFailedClusterings_: the number of bad suggestions for manual clustering (should be 0 for this dataset)  
_mappingPercent_: the percent of entities in the initial set, the initialClustered can deviate from this slightly due to rules of having at leas one entity per module and also rounding  
_metric_: the metric used to create the initial set (should be rand for this dataset)  
_system_: the system used in the mapping  
_algorithm_: the mapping function name typically: HuGMe:CAttract, NaiveBayes:NBAttract, LSI_IR:IRAttract, LSI_IR:LSIAttract  
_omega_: the value of the omega parameter used in CountAttract, -1 for others  
_phi_: the value of the phi parameter used in Countattract, -1 for others  
_dw__*: the weights of different dependencies for CountAttract, X for others  
_stemming_: if stemming is used or not (Y/N/X)  
_cda_: if CDA is used or not (Y/N/X) 
_nodeText_: if the text (identifier names etc) in the source code  entity is used or not (Y/N/X)  
_nodeName_: if the file name of the source code entity is used or not (Y/N/X)  
_archName_: if the module name is used or not (Y/N/X)  
_minWordSize_: threshold for minimum term length should be 3 for this dataset  
_threshold_: the mapping threshold for NBAttract, should be 0.9 for this dataset)	wordcount  
_wordCount_: if the words should be counted or be binary for each source code entity in NBAttract (should be N for this dataset)  

## Metric Calculations
From this data some basic performance metrics can be computed:

truepositives = totalAutoClustered - totalAutoWrong  
falsenegatives = totalMapped - initialClustered - totalManuallyClustered - totalAutoClustered  

precision = truepositives / totalAutoClustered  
recall = truepositives / (truepositives + falsenegatives)  
f1 = (2 * precision * recall) / (precision + recall)

