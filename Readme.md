
# Your final report should include each of the following:



```python
import pandas as pd
import numpy as np

jason_path = "HeroesOfPymoli/purchase_data.json"

orginal_df = pd.read_json(jason_path)

```


```python
#Total Number of Players
Total_numbers_of_players = {}

Total_numbers_of_players['Total Players'] = orginal_df['SN'].nunique()
pd.DataFrame(data=Total_numbers_of_players,index=[0])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>573</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Total)
Needs Formating in table


```python
#Holds Numbers
purchasing_analysis = {}

#Pulling the Data from orginal_df
purchasing_analysis['Number of Unique Items'] = orginal_df['Item Name'].nunique()
purchasing_analysis['Average Price']=orginal_df["Price"].mean()
purchasing_analysis['Number of Purchases']=orginal_df["Item ID"].count()
purchasing_analysis['Total Revenue']=orginal_df["Price"].sum()

#Combines Data into a Dataframe
purchasing_analysis_df=pd.DataFrame(data=purchasing_analysis,index=[0])

#Formats the Output for Readablity
purchasing_analysis_df=purchasing_analysis_df[['Number of Unique Items','Average Price','Number of Purchases','Total Revenue']]
purchasing_analysis_df.style.format({'Total Revenue':'${:.2f}','Average Price':'${:.2f}'})
```




<style  type="text/css" >
</style>  
<table id="T_0a1b7ab8_3a96_11e8_9f5a_b4ae2bc9de0d" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Number of Unique Items</th> 
        <th class="col_heading level0 col1" >Average Price</th> 
        <th class="col_heading level0 col2" >Number of Purchases</th> 
        <th class="col_heading level0 col3" >Total Revenue</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a1b7ab8_3a96_11e8_9f5a_b4ae2bc9de0dlevel0_row0" class="row_heading level0 row0" >0</th> 
        <td id="T_0a1b7ab8_3a96_11e8_9f5a_b4ae2bc9de0drow0_col0" class="data row0 col0" >179</td> 
        <td id="T_0a1b7ab8_3a96_11e8_9f5a_b4ae2bc9de0drow0_col1" class="data row0 col1" >$2.93</td> 
        <td id="T_0a1b7ab8_3a96_11e8_9f5a_b4ae2bc9de0drow0_col2" class="data row0 col2" >780</td> 
        <td id="T_0a1b7ab8_3a96_11e8_9f5a_b4ae2bc9de0drow0_col3" class="data row0 col3" >$2286.33</td> 
    </tr></tbody> 
</table> 



# Gender Demographics
Needs Formating in table


```python
gender_count = orginal_df.groupby(['Gender'])
gender_count_df = gender_count[["SN"]].nunique()
gender_count_df['Percentage of Players'] = gender_count["SN"].nunique()/gender_count_df['SN'].sum()

#Format Table
gender_count_df = gender_count_df.rename(columns={"SN": "Total Count"})
gender_count_df.style.format({'Percentage of Players':'{:.2%}'})
```




<style  type="text/css" >
</style>  
<table id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0d" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Count</th> 
        <th class="col_heading level0 col1" >Percentage of Players</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0dlevel0_row0" class="row_heading level0 row0" >Female</th> 
        <td id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0drow0_col0" class="data row0 col0" >100</td> 
        <td id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0drow0_col1" class="data row0 col1" >17.45%</td> 
    </tr>    <tr> 
        <th id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0dlevel0_row1" class="row_heading level0 row1" >Male</th> 
        <td id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0drow1_col0" class="data row1 col0" >465</td> 
        <td id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0drow1_col1" class="data row1 col1" >81.15%</td> 
    </tr>    <tr> 
        <th id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0dlevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0drow2_col0" class="data row2 col0" >8</td> 
        <td id="T_0a21c0c8_3a96_11e8_ba1a_b4ae2bc9de0drow2_col1" class="data row2 col1" >1.40%</td> 
    </tr></tbody> 
</table> 




```python
gender_analysis = {}
gender_analysis['Average Purchase Price'] = gender_count["Price"].mean()
gender_analysis['Total Purchase Value'] = gender_count["Price"].sum()
gender_analysis['Purchase Count'] = gender_count["Price"].count()
gender_analysis['Normalized Totals'] = gender_count["Price"].sum()/gender_count["SN"].nunique()
pd.DataFrame(data=gender_analysis).style.format({'Normalized Totals':'${:,.2f}','Total Purchase Value':'${:,.2f}',\
                                                'Average Purchase Price':'${:,.2f}'})

```




<style  type="text/css" >
</style>  
<table id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0d" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Average Purchase Price</th> 
        <th class="col_heading level0 col1" >Normalized Totals</th> 
        <th class="col_heading level0 col2" >Purchase Count</th> 
        <th class="col_heading level0 col3" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Gender</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0dlevel0_row0" class="row_heading level0 row0" >Female</th> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow0_col0" class="data row0 col0" >$2.82</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow0_col1" class="data row0 col1" >$3.83</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow0_col2" class="data row0 col2" >136</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow0_col3" class="data row0 col3" >$382.91</td> 
    </tr>    <tr> 
        <th id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0dlevel0_row1" class="row_heading level0 row1" >Male</th> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow1_col0" class="data row1 col0" >$2.95</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow1_col1" class="data row1 col1" >$4.02</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow1_col2" class="data row1 col2" >633</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow1_col3" class="data row1 col3" >$1,867.68</td> 
    </tr>    <tr> 
        <th id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0dlevel0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow2_col0" class="data row2 col0" >$3.25</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow2_col1" class="data row2 col1" >$4.47</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow2_col2" class="data row2 col2" >11</td> 
        <td id="T_0a26093e_3a96_11e8_b2bf_b4ae2bc9de0drow2_col3" class="data row2 col3" >$35.74</td> 
    </tr></tbody> 
</table> 



# **Age Demographics**

* The below each broken into bins of 4 years (i.e. &lt;10, 10-14, 15-19, etc.) 
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value
  * Normalized Totals


```python
#age_demographics = orginal_df.groupby(['Age']).nunique()
#age_demographics['SN'].sum()
```


```python
age_demographics = orginal_df[['Age','SN','Price']]
bins = [0, 10, 14, 19, 24, 29, 34, 39, 999]
group_names = ['<10', '10-14', '15-19', '20-24', '25-29','30-34','35-39','40+']
age_demographics=age_demographics.reset_index(drop=True)
age_demographics['Catagory']=pd.cut(age_demographics['Age'], bins, labels=group_names)
age_catagory_df = age_demographics.groupby(['Catagory']).nunique()
age_total_p_df = age_demographics.groupby(['Catagory']).count()

age_price_df = age_demographics.groupby(['Catagory']).sum()
total_number = age_catagory_df['SN'].sum()
age_catagory_df2 = age_total_p_df[['SN']]
age_catagory_df2=age_catagory_df2.reset_index()
age_price_df = age_price_df.reset_index()

catagory_demographics_df = age_catagory_df
catagory_demographics_df = catagory_demographics_df.drop(columns=['Catagory','Age'])

#purchase count by catagory needs renaming
catagory_demographics_df = catagory_demographics_df.reset_index()
catagory_demographics_df['Percentage of Players'] = catagory_demographics_df['SN']/total_number
catagory_demographics_df = catagory_demographics_df[['Catagory','SN','Percentage of Players']].set_index('Catagory')
catagory_final_df = catagory_demographics_df.rename(columns={'SN':'Total Count'})
catagory_demographics_df = catagory_demographics_df.reset_index()
catagory_final_df.style.format({'Percentage of Players':'{:.2%}'})

```




<style  type="text/css" >
</style>  
<table id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0d" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Total Count</th> 
        <th class="col_heading level0 col1" >Percentage of Players</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Catagory</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0dlevel0_row0" class="row_heading level0 row0" ><10</th> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow0_col0" class="data row0 col0" >22</td> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow0_col1" class="data row0 col1" >3.84%</td> 
    </tr>    <tr> 
        <th id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0dlevel0_row1" class="row_heading level0 row1" >10-14</th> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow1_col0" class="data row1 col0" >20</td> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow1_col1" class="data row1 col1" >3.49%</td> 
    </tr>    <tr> 
        <th id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0dlevel0_row2" class="row_heading level0 row2" >15-19</th> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow2_col0" class="data row2 col0" >100</td> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow2_col1" class="data row2 col1" >17.45%</td> 
    </tr>    <tr> 
        <th id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0dlevel0_row3" class="row_heading level0 row3" >20-24</th> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow3_col0" class="data row3 col0" >259</td> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow3_col1" class="data row3 col1" >45.20%</td> 
    </tr>    <tr> 
        <th id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0dlevel0_row4" class="row_heading level0 row4" >25-29</th> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow4_col0" class="data row4 col0" >87</td> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow4_col1" class="data row4 col1" >15.18%</td> 
    </tr>    <tr> 
        <th id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0dlevel0_row5" class="row_heading level0 row5" >30-34</th> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow5_col0" class="data row5 col0" >47</td> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow5_col1" class="data row5 col1" >8.20%</td> 
    </tr>    <tr> 
        <th id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0dlevel0_row6" class="row_heading level0 row6" >35-39</th> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow6_col0" class="data row6 col0" >27</td> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow6_col1" class="data row6 col1" >4.71%</td> 
    </tr>    <tr> 
        <th id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0dlevel0_row7" class="row_heading level0 row7" >40+</th> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow7_col0" class="data row7 col0" >11</td> 
        <td id="T_0a3901f4_3a96_11e8_ae4c_b4ae2bc9de0drow7_col1" class="data row7 col1" >1.92%</td> 
    </tr></tbody> 
</table> 




```python
age_price_df['Average Spent'] =  age_price_df['Price']/catagory_demographics_df['SN']
age_price_df['Normalized Totals'] = age_price_df['Price']/age_catagory_df2["SN"]
age_price_df['Purchase Count'] = age_catagory_df2["SN"]
age_display = age_price_df[['Catagory','Purchase Count','Average Spent','Price','Normalized Totals']]

age_display = age_display.rename(columns={'Price':'Total Purchase Value'})
age_display = age_display.set_index(['Catagory']).style.format({'Normalized Totals':'${:,.2f}','Total Purchase Value':'${:,.2f}',\
                            'Average Purchase Price':'${:,.2f}','Average Spent':'${:,.2f}'})
age_display
```




<style  type="text/css" >
</style>  
<table id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0d" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Average Spent</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
        <th class="col_heading level0 col3" >Normalized Totals</th> 
    </tr>    <tr> 
        <th class="index_name level0" >Catagory</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0dlevel0_row0" class="row_heading level0 row0" ><10</th> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow0_col0" class="data row0 col0" >32</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow0_col1" class="data row0 col1" >$4.39</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow0_col2" class="data row0 col2" >$96.62</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow0_col3" class="data row0 col3" >$3.02</td> 
    </tr>    <tr> 
        <th id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0dlevel0_row1" class="row_heading level0 row1" >10-14</th> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow1_col0" class="data row1 col0" >31</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow1_col1" class="data row1 col1" >$4.19</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow1_col2" class="data row1 col2" >$83.79</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow1_col3" class="data row1 col3" >$2.70</td> 
    </tr>    <tr> 
        <th id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0dlevel0_row2" class="row_heading level0 row2" >15-19</th> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow2_col0" class="data row2 col0" >133</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow2_col1" class="data row2 col1" >$3.86</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow2_col2" class="data row2 col2" >$386.42</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow2_col3" class="data row2 col3" >$2.91</td> 
    </tr>    <tr> 
        <th id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0dlevel0_row3" class="row_heading level0 row3" >20-24</th> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow3_col0" class="data row3 col0" >336</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow3_col1" class="data row3 col1" >$3.78</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow3_col2" class="data row3 col2" >$978.77</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow3_col3" class="data row3 col3" >$2.91</td> 
    </tr>    <tr> 
        <th id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0dlevel0_row4" class="row_heading level0 row4" >25-29</th> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow4_col0" class="data row4 col0" >125</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow4_col1" class="data row4 col1" >$4.26</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow4_col2" class="data row4 col2" >$370.33</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow4_col3" class="data row4 col3" >$2.96</td> 
    </tr>    <tr> 
        <th id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0dlevel0_row5" class="row_heading level0 row5" >30-34</th> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow5_col0" class="data row5 col0" >64</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow5_col1" class="data row5 col1" >$4.20</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow5_col2" class="data row5 col2" >$197.25</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow5_col3" class="data row5 col3" >$3.08</td> 
    </tr>    <tr> 
        <th id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0dlevel0_row6" class="row_heading level0 row6" >35-39</th> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow6_col0" class="data row6 col0" >42</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow6_col1" class="data row6 col1" >$4.42</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow6_col2" class="data row6 col2" >$119.40</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow6_col3" class="data row6 col3" >$2.84</td> 
    </tr>    <tr> 
        <th id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0dlevel0_row7" class="row_heading level0 row7" >40+</th> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow7_col0" class="data row7 col0" >17</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow7_col1" class="data row7 col1" >$4.89</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow7_col2" class="data row7 col2" >$53.75</td> 
        <td id="T_0a3cfc4a_3a96_11e8_aafe_b4ae2bc9de0drow7_col3" class="data row7 col3" >$3.16</td> 
    </tr></tbody> 
</table> 



# **Top Spenders**

* Identify the the top 5 spenders in the game by total purchase value, then list (in a table):
  * SN
  * Purchase Count
  * Average Purchase Price
  * Total Purchase Value


```python

spenders_count_df = orginal_df.groupby(['SN']).count().reset_index()
spenders_count_df=spenders_count_df.drop(columns=['Age','Gender','Item ID','Price'])
spenders_value_df = orginal_df.groupby(['SN']).sum().reset_index()
spenders_value_df=spenders_value_df.drop(columns=['Age','Item ID'])
spenders_mean_df = orginal_df.groupby(['SN']).mean().reset_index()
spenders_mean_df=spenders_mean_df.drop(columns=['Age','Item ID'])

spenders_final_df = spenders_count_df
spenders_final_df['Total Purchase Value'] = spenders_value_df['Price']
spenders_final_df['Average Purchase Price'] = spenders_mean_df['Price']

spenders_format_df = spenders_final_df.sort_values(by=['Total Purchase Value'], ascending=False).head()
spenders_format_df=spenders_format_df.rename(columns={'Item Name':'Purchase Count'})
some_df = spenders_format_df[['SN','Purchase Count','Average Purchase Price','Total Purchase Value']]
some_df = some_df.set_index(['SN']).style.format({'Average Purchase Price':'${:,.2f}','Total Purchase Value':'${:,.2f}'})
some_df
```




<style  type="text/css" >
</style>  
<table id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0d" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Purchase Count</th> 
        <th class="col_heading level0 col1" >Average Purchase Price</th> 
        <th class="col_heading level0 col2" >Total Purchase Value</th> 
    </tr>    <tr> 
        <th class="index_name level0" >SN</th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
        <th class="blank" ></th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0dlevel0_row0" class="row_heading level0 row0" >Undirrala66</th> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow0_col0" class="data row0 col0" >5</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow0_col1" class="data row0 col1" >$3.41</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow0_col2" class="data row0 col2" >$17.06</td> 
    </tr>    <tr> 
        <th id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0dlevel0_row1" class="row_heading level0 row1" >Saedue76</th> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow1_col0" class="data row1 col0" >4</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow1_col1" class="data row1 col1" >$3.39</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow1_col2" class="data row1 col2" >$13.56</td> 
    </tr>    <tr> 
        <th id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0dlevel0_row2" class="row_heading level0 row2" >Mindimnya67</th> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow2_col0" class="data row2 col0" >4</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow2_col1" class="data row2 col1" >$3.18</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow2_col2" class="data row2 col2" >$12.74</td> 
    </tr>    <tr> 
        <th id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0dlevel0_row3" class="row_heading level0 row3" >Haellysu29</th> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow3_col0" class="data row3 col0" >3</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow3_col1" class="data row3 col1" >$4.24</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow3_col2" class="data row3 col2" >$12.73</td> 
    </tr>    <tr> 
        <th id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0dlevel0_row4" class="row_heading level0 row4" >Eoda93</th> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow4_col0" class="data row4 col0" >3</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow4_col1" class="data row4 col1" >$3.86</td> 
        <td id="T_0a49d642_3a96_11e8_9982_b4ae2bc9de0drow4_col2" class="data row4 col2" >$11.58</td> 
    </tr></tbody> 
</table> 




```python
item_count_df = orginal_df.groupby(['Item Name']).count().reset_index()
#Purchase Count
item_count_df=item_count_df.drop(columns=['Age','Gender','Item ID','SN'])
#item_count_df.head()
```


```python
item_price_df = orginal_df.groupby(['Item Name']).mean().reset_index()

item_price_df = item_price_df.drop(columns=['Age','Item ID'])
#item_price_df.head()
#Average Price
```


```python
item_value_df = orginal_df.groupby(['Item Name']).sum().reset_index()
item_value_df=item_value_df.drop(columns=['Age','Item ID'])
#item_value_df.head()
```


```python
final_df = item_count_df
final_df['Item Price'] = item_price_df['Price']
final_df['Total Purchase Value'] = item_value_df['Price']
final_df.sort_values(by=['Price'], ascending=False).head().style.format({'Item Price':'${:,.2f}','Total Purchase Value':'${:,.2f}'})
```




<style  type="text/css" >
</style>  
<table id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0d" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Item Name</th> 
        <th class="col_heading level0 col1" >Price</th> 
        <th class="col_heading level0 col2" >Item Price</th> 
        <th class="col_heading level0 col3" >Total Purchase Value</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0dlevel0_row0" class="row_heading level0 row0" >56</th> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow0_col0" class="data row0 col0" >Final Critic</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow0_col1" class="data row0 col1" >14</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow0_col2" class="data row0 col2" >$2.76</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow0_col3" class="data row0 col3" >$38.60</td> 
    </tr>    <tr> 
        <th id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0dlevel0_row1" class="row_heading level0 row1" >8</th> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow1_col0" class="data row1 col0" >Arcane Gem</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow1_col1" class="data row1 col1" >11</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow1_col2" class="data row1 col2" >$2.23</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow1_col3" class="data row1 col3" >$24.53</td> 
    </tr>    <tr> 
        <th id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0dlevel0_row2" class="row_heading level0 row2" >11</th> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow2_col0" class="data row2 col0" >Betrayal, Whisper of Grieving Widows</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow2_col1" class="data row2 col1" >11</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow2_col2" class="data row2 col2" >$2.35</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow2_col3" class="data row2 col3" >$25.85</td> 
    </tr>    <tr> 
        <th id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0dlevel0_row3" class="row_heading level0 row3" >137</th> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow3_col0" class="data row3 col0" >Stormcaller</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow3_col1" class="data row3 col1" >10</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow3_col2" class="data row3 col2" >$3.46</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow3_col3" class="data row3 col3" >$34.65</td> 
    </tr>    <tr> 
        <th id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0dlevel0_row4" class="row_heading level0 row4" >173</th> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow4_col0" class="data row4 col0" >Woeful Adamantite Claymore</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow4_col1" class="data row4 col1" >9</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow4_col2" class="data row4 col2" >$1.24</td> 
        <td id="T_0a5d4454_3a96_11e8_a4be_b4ae2bc9de0drow4_col3" class="data row4 col3" >$11.16</td> 
    </tr></tbody> 
</table> 




```python
final_df.sort_values(by=['Total Purchase Value'], ascending=False).head().head().style.format({'Item Price':'${:,.2f}','Total Purchase Value':'${:,.2f}'})
```




<style  type="text/css" >
</style>  
<table id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0d" > 
<thead>    <tr> 
        <th class="blank level0" ></th> 
        <th class="col_heading level0 col0" >Item Name</th> 
        <th class="col_heading level0 col1" >Price</th> 
        <th class="col_heading level0 col2" >Item Price</th> 
        <th class="col_heading level0 col3" >Total Purchase Value</th> 
    </tr></thead> 
<tbody>    <tr> 
        <th id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0dlevel0_row0" class="row_heading level0 row0" >56</th> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow0_col0" class="data row0 col0" >Final Critic</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow0_col1" class="data row0 col1" >14</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow0_col2" class="data row0 col2" >$2.76</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow0_col3" class="data row0 col3" >$38.60</td> 
    </tr>    <tr> 
        <th id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0dlevel0_row1" class="row_heading level0 row1" >112</th> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow1_col0" class="data row1 col0" >Retribution Axe</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow1_col1" class="data row1 col1" >9</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow1_col2" class="data row1 col2" >$4.14</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow1_col3" class="data row1 col3" >$37.26</td> 
    </tr>    <tr> 
        <th id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0dlevel0_row2" class="row_heading level0 row2" >137</th> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow2_col0" class="data row2 col0" >Stormcaller</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow2_col1" class="data row2 col1" >10</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow2_col2" class="data row2 col2" >$3.46</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow2_col3" class="data row2 col3" >$34.65</td> 
    </tr>    <tr> 
        <th id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0dlevel0_row3" class="row_heading level0 row3" >132</th> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow3_col0" class="data row3 col0" >Spectral Diamond Doomblade</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow3_col1" class="data row3 col1" >7</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow3_col2" class="data row3 col2" >$4.25</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow3_col3" class="data row3 col3" >$29.75</td> 
    </tr>    <tr> 
        <th id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0dlevel0_row4" class="row_heading level0 row4" >96</th> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow4_col0" class="data row4 col0" >Orenmir</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow4_col1" class="data row4 col1" >6</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow4_col2" class="data row4 col2" >$4.95</td> 
        <td id="T_0a62781c_3a96_11e8_81b3_b4ae2bc9de0drow4_col3" class="data row4 col3" >$29.70</td> 
    </tr></tbody> 
</table> 


