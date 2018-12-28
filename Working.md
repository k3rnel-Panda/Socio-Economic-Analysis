**PROCEDURE**

1. *Health*: 

This socio-economic parameter is one of the most influential parameters which can make or break a particular district in terms of their effects on a state as a whole. Due to its sheer importance, it was paramount to take up a dataset which could correctly portray the scenario. 
Therefore, I decided to go with the data present at the datagov.in website which you could find [here][2].

After extracting the data from the above mentioned website, I cleaned the redundant and unnecessary parameters which would have not clearly depicted the socio-economic influence of this indicator.  

	`health = pd.read_csv('./Health.csv')   
	 health.sort_values(by=['District'])
	 health.District = health.District.str.lower()
	 health_ind = health
	 health_ind.reset_index(drop=True, inplace=True)
	 health_ind.sort_values(by=['District'])
	 health_ind.head(5)
	
	
![Health ](https://lh3.googleusercontent.com/ocIajF__PqCfEGZXKjtl_Zpje22mFlQUzDQ8m0xy1rxQ2nTrfyIdeGjuwsttQ1W240nPH_UNvhF-=s0 "Health")
*Agriculture*

Agriculture, the world’s oldest profession is the main source of life sustenance for human population. However, though there has been substantial growth in other sectors, the Agriculture Sector still continues to be the mainstay of livelihood for human civilization. Growth of the agricultural sector is important not only for ensuing food security and reduction of poverty in rural areas, but also sustaining growth of rest of the states and its districts. 

The data pertinent to the agricultural field has been downloaded from a survey which can be found [here][3]. 

`agricult = pd.read_csv('./Agriculture.csv')
print agricult.columns`

![enter image description here](https://lh3.googleusercontent.com/XVUqxqTnq_sps98x9WcdHr0J5rcgZK4og4aXF7LBr567JqhNghR58FcInjAZFFcxuCQEPkk17XMn=s0 "agri1.PNG")


`agri_ind = agricult
print 'Agriculture Indicators'
agri_ind.sort_values(by=['District']).head(5)`

![enter image description here](https://lh3.googleusercontent.com/8AnEnv2OC76edrsQRHhbpvb7fk5GbU0ftlRthRhX_Mxq2VgK6ivKNOzq45zJ2mnpSIxFHSHlavzw=s0 "agri2.PNG")

After comparing the data between the health and the agriculture indicators, it became clear that there was a discrepancy in the column, District. Some districts were named differently when compared with the same districts in the other file. This problem could be rectified with the help of Python itself but by cleaning the erroneous values in Excel, it displayed a quick and much more efficient response as compared to Python.


*Literacy Rate:*

This parameter is essential to showcase the education status of a district which can lead to variable effects in the Human Development Index.
The relevant data for this field has been taken from [here][4].

`literacy = pd.read_csv('./Literacy.csv')
literacy_ind = literacy
literacy_ind`

![enter image description here](https://lh3.googleusercontent.com/tCjEirTcoY3FcqkG5pfgYtwhP2cRXUfwHJ00Ss1s7K06cSAoDYUJi2bbtBDMxYrF39xiqekNlrY0=s0 "literacy.PNG")

*Employment Rate*:

This parameter is used to highlight the working status of the people in a particular district and how literacy rates affect employment chances.
The data for this field has also been taken from the [above source][5].

`emp = pd.read_csv('./Work.csv')
emp_ind = emp
emp_ind.head()`

![enter image description here](https://lh3.googleusercontent.com/s2rrLcBSJLwKb7jIxhKS4InBsm_Q0DipyvsZwAW_IziZY96RXdkTFY1ASyUWxXveHteoYHcjnU4l=s0 "emp.PNG")

**Merging Data**

The collection of all the indicators contributing to socio-economic changes need to be compiled together at one source in order to decipher the order in which these indicators effect a region and how these regions are effected by it. 

`indicator = pd.merge(health_ind, agri_ind, left_on=['District'], right_on=['District'], how='left')
indicator = pd.merge(literacy_ind, emp_ind, left_on=['District'], right_on=['District'],
how='left')
print 'Indicator Dataset'
print indicator.shape
indicator`

![enter image description here](https://lh3.googleusercontent.com/_yFAKQlBe6WJKyEukvEQvE9d6Ad2nGb_25errd4uCDTx7ha-q6iWO_b9YHDLuMLRO4pnjbAi8FBo=s0 "merge.PNG")

**Ranking the Indicators**:

`corcor  ==  indicator.corr()
cor.loc[:,:] = np.tril(cor, k=-1)
cor = cor.stack()
cor[(cor > 0.60) | (cor < -0.50)]`

![enter image description here](https://lh3.googleusercontent.com/JYMeA9Ka01FvOIxWZ7JPcfcm7mZsjFzdeivvADd91BrS4L8jtRjvaV0MAlZC4kBdSQv3Nm2X42W7=s0 "Indicator.PNG")

**Ranking the Districts based on the ranked indicators**:

`X_indicators = indicator.ix[:,1:].copy()
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X_indicators)
scaled_average = np.mean(X_scaled, axis=1) 
dictionary = dict(zip(indicator.ix[:,0], scaled_average))
sorted_x = sorted(dictionary.items(), key=operator.itemgetter(1), reverse=True)
for index, rank in enumerate(sorted_x):
    print index+1, '', rank[0], rank[1]`

![enter image description here](https://lh3.googleusercontent.com/sTL2VUBR2QAZvOJ-k-VxwzxcK7tqyZxzHK39rYx8MgfnGR25fd2dq3DA241P0S0ih3cBPZ_gSiLi=s0 "rank.PNG")


*Future Implementation:*
----------------------------------------

A more in depth analysis of the various indicators leading to the socio-economic impact would pave the way for much more efficient and ground breaking results for the upliftment of that region. 

One of the most vital aspect to remember for such an analysis is the selection of a correct dataset which should have citations from a reputed survey.



**TOOLS USED**:
1. Python
2. Excel
3. Flourish

				**THANK YOU FOR THE READ!!**
