**PROCEDURE**:

The first challenge was tackled using Excel as it provided a much more faster and efficient result. The necessary steps which were taken are as follows:

1.  Firstly, the data under the tab_id was sorted for both the sheets in order to have a common vector value which would be compared in order to extract the correct AC name, Mandal name and Village name. 
2. Second, the correct formula was formulated in order to extract the correct Village Name. 
3. The data on the first sheet was entirely moved to the second sheet and aligned in accordance to the survey start and end dates. 
4. I made use of the **MATCH** function in order to compare whether the date lies in between the survey start and end dates. One could argue about the use of VLOOKUP here but all it does is that it provides a reference rather than returning a value. 
5. Moreover, the index function was used in order to replicate the exact number of column values which were needed to find out the Village Name.
6. Ultimately, an IFERROR function was used to return an unavailable message for missing AC names, Mandal names and Village Names. 
6. As expected, all the values were not satisfied as some were devoid of tablet entries while some were out of range from the survey dates. 
