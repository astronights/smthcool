# smthcool
This code branch provides more weightage to the Mutect variant calling method. The dataset must be extracted and available in the path ./dataset/

Algorithm:
=========
If Mutect does not call a variant, set the result to be False.
If Mutect calls a variant, see if atleast two of the other three variant callers (Vardict, Varscan, Freebayes) also call it. If atleast 2 of them also call the variant, set the result to be True, else set the result to be False.

Rationale:
=========
Almost all the variant calling methods appear to tag the true positives and true negatives quite well. The key difference lies in the count of false positives identified. Of all the variant callers, Mutect is the one with least number of false positives in general. This is also seen in the high Chi square value it has when comparing the results of Mutect and the truth file for each dataset.

Key Considerations:
==================
Here, we only consider the field FILTER_PASS from all 4 VCF files. An outer join is done over all the VCF files to get the necessary combined dataframe. The rows that have a NaN associated with them in the dataframe are replaced with 0, indicating they are not called by the algorithms.

Results:
========

|Dataset|F1|Precision|Recall|
|real1|0.78|0.72|0.83|
|real2_part1|0.71|0.64|0.80|
|syn1|0.92|0.87|0.97|
|syn2|0.93|0.88|0.97|
|syn3|0.70|0.56|0.93|
|syn4|0.66|0.61|0.73|
|syn5|0.85|0.78|0.93|


