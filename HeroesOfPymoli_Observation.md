# Observable Trends in HeroesOfPymoli Dataset 


```python
Obsevation 1.
Observation 2.
Observation 3.
```


```python
# Dependencies and Setup
%load_ext lab_black
import pandas as pd

# File to Load
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(file_to_load)
purchase_data.head()
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
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count

* Display the total number of players



```python
# Calculating length of unique screen names "SN" for total players
total_players = len(purchase_data["SN"].unique())

# Creating DataFrame for Total Players
df1 = pd.DataFrame({"Total Players": [total_players]})
df1
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
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
# Running basic calculations for number of unique items, average price, number of purchases, and total  revenue
unique_items = len(purchase_data["Item ID"].unique())
average_price = purchase_data["Price"].mean()
number_purchase = purchase_data["Purchase ID"].count()
total_revenue = purchase_data["Price"].sum()

# Creating DataFrame for Purchasing Analysis (Total)
df2 = pd.DataFrame(
    {
        "Number of Unique Items": [unique_items],
        "Average Price": [average_price],
        "Number of Purchases": [number_purchase],
        "Total Revenue": [total_revenue],
    }
)

# Formatting average price and total revenue
df2.style.format({"Average Price": "${:,.2f}", "Total Revenue": "${:,.2f}"})
```




<style  type="text/css" >
</style><table id="T_c7281512_f49e_11ea_89ca_42010a8a0002" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Number of Unique Items</th>        <th class="col_heading level0 col1" >Average Price</th>        <th class="col_heading level0 col2" >Number of Purchases</th>        <th class="col_heading level0 col3" >Total Revenue</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c7281512_f49e_11ea_89ca_42010a8a0002level0_row0" class="row_heading level0 row0" >0</th>
                        <td id="T_c7281512_f49e_11ea_89ca_42010a8a0002row0_col0" class="data row0 col0" >183</td>
                        <td id="T_c7281512_f49e_11ea_89ca_42010a8a0002row0_col1" class="data row0 col1" >$3.05</td>
                        <td id="T_c7281512_f49e_11ea_89ca_42010a8a0002row0_col2" class="data row0 col2" >780</td>
                        <td id="T_c7281512_f49e_11ea_89ca_42010a8a0002row0_col3" class="data row0 col3" >$2,379.77</td>
            </tr>
    </tbody></table>



## Gender Demographics

* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
# Grouping purchase_data by gender
gender_group = purchase_data.groupby(["Gender"])

# Calculating count of unique screen names "SN", i.e. count of players by gender
player_count_gender = gender_group["SN"].nunique()

# Calculating percentage of players by gender
player_percent_gender = (player_count_gender / total_players) * 100

# Creating DataFrame for Gender Demographics
df5 = pd.DataFrame(
    {
        "Total Count": player_count_gender,
        "Percentage of Players": player_percent_gender,
    }
)

# Setting index, sorting by total count in descending order, and formatting percentage of players
df5.index.name = None
df5.sort_values(["Total Count"], ascending=False).style.format(
    {"Percentage of Players": "{:,.2f}%"}
)
```




<style  type="text/css" >
</style><table id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Total Count</th>        <th class="col_heading level0 col1" >Percentage of Players</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002level0_row0" class="row_heading level0 row0" >Male</th>
                        <td id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002row0_col0" class="data row0 col0" >484</td>
                        <td id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002row0_col1" class="data row0 col1" >84.03%</td>
            </tr>
            <tr>
                        <th id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002level0_row1" class="row_heading level0 row1" >Female</th>
                        <td id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002row1_col0" class="data row1 col0" >81</td>
                        <td id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002row1_col1" class="data row1 col1" >14.06%</td>
            </tr>
            <tr>
                        <th id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002level0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th>
                        <td id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002row2_col0" class="data row2 col0" >11</td>
                        <td id="T_c72e1c78_f49e_11ea_89ca_42010a8a0002row2_col1" class="data row2 col1" >1.91%</td>
            </tr>
    </tbody></table>




## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Running basic calculation for purchase count by gender
purchase_count_gender = gender_group["Purchase ID"].count()

# Running basic calculation for average purchase price by gender
average_price_gender = gender_group["Price"].mean()

# Running basic calculation for total purchase value by gender
total_value_gender = gender_group["Price"].sum()

# Running basic calculation for average total purchase per person by gender
avg_per_person_gender = total_value_gender / player_count_gender

# Creating DataFrame for Purchasing Analysis (Gender)
df4 = pd.DataFrame(
    {
        "Purchase Count": purchase_count_gender,
        "Average Purchase Price": average_price_gender,
        "Total Purchase Value": total_value_gender,
        "Avg Total Purchase per Person": avg_per_person_gender,
    }
)

# Setting index and formatting average purchase price,total purchase value, and average total purchase per person
df4.index.name = "Gender"
df4.style.format(
    {
        "Average Purchase Price": "${:,.2f}",
        "Total Purchase Value": "${:,.2f}",
        "Avg Total Purchase per Person": "${:,.2f}",
    }
)
```




<style  type="text/css" >
</style><table id="T_c7340034_f49e_11ea_89ca_42010a8a0002" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th>    </tr>    <tr>        <th class="index_name level0" >Gender</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c7340034_f49e_11ea_89ca_42010a8a0002level0_row0" class="row_heading level0 row0" >Female</th>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row0_col0" class="data row0 col0" >113</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row0_col1" class="data row0 col1" >$3.20</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row0_col2" class="data row0 col2" >$361.94</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row0_col3" class="data row0 col3" >$4.47</td>
            </tr>
            <tr>
                        <th id="T_c7340034_f49e_11ea_89ca_42010a8a0002level0_row1" class="row_heading level0 row1" >Male</th>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row1_col0" class="data row1 col0" >652</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row1_col1" class="data row1 col1" >$3.02</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row1_col2" class="data row1 col2" >$1,967.64</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row1_col3" class="data row1 col3" >$4.07</td>
            </tr>
            <tr>
                        <th id="T_c7340034_f49e_11ea_89ca_42010a8a0002level0_row2" class="row_heading level0 row2" >Other / Non-Disclosed</th>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row2_col0" class="data row2 col0" >15</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row2_col1" class="data row2 col1" >$3.35</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row2_col2" class="data row2 col2" >$50.19</td>
                        <td id="T_c7340034_f49e_11ea_89ca_42010a8a0002row2_col3" class="data row2 col3" >$4.56</td>
            </tr>
    </tbody></table>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
# Creating bins for ages
age_bins = [0, 9.90, 14.90, 19.90, 24.90, 29.90, 34.90, 39.90, 9999]
age_labels = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

# Assigning and sorting age data into age_bins and age_labels
purchase_data["Age Ranges"] = pd.cut(purchase_data["Age"], age_bins, labels=age_labels)

# Grouping updated purchase_data by age
age_group = purchase_data.groupby(["Age Ranges"])

# Calculating total number of players by age
player_count_age = age_group["SN"].nunique()

# Calculating percentage of players by age
player_percent_age = (player_count_age / total_players) * 100

# Creating DataFrame for Age Demographics
df5 = pd.DataFrame(
    {"Total Count": player_count_age, "Percentage of Players": player_percent_age,}
)

# Setting index and formatting percentage of players
df5.index.name = None
df5.style.format({"Percentage of Players": "{:,.2f}%"})
```




<style  type="text/css" >
</style><table id="T_c73991f2_f49e_11ea_89ca_42010a8a0002" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Total Count</th>        <th class="col_heading level0 col1" >Percentage of Players</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c73991f2_f49e_11ea_89ca_42010a8a0002level0_row0" class="row_heading level0 row0" ><10</th>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row0_col0" class="data row0 col0" >17</td>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row0_col1" class="data row0 col1" >2.95%</td>
            </tr>
            <tr>
                        <th id="T_c73991f2_f49e_11ea_89ca_42010a8a0002level0_row1" class="row_heading level0 row1" >10-14</th>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row1_col0" class="data row1 col0" >22</td>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row1_col1" class="data row1 col1" >3.82%</td>
            </tr>
            <tr>
                        <th id="T_c73991f2_f49e_11ea_89ca_42010a8a0002level0_row2" class="row_heading level0 row2" >15-19</th>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row2_col0" class="data row2 col0" >107</td>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row2_col1" class="data row2 col1" >18.58%</td>
            </tr>
            <tr>
                        <th id="T_c73991f2_f49e_11ea_89ca_42010a8a0002level0_row3" class="row_heading level0 row3" >20-24</th>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row3_col0" class="data row3 col0" >258</td>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row3_col1" class="data row3 col1" >44.79%</td>
            </tr>
            <tr>
                        <th id="T_c73991f2_f49e_11ea_89ca_42010a8a0002level0_row4" class="row_heading level0 row4" >25-29</th>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row4_col0" class="data row4 col0" >77</td>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row4_col1" class="data row4 col1" >13.37%</td>
            </tr>
            <tr>
                        <th id="T_c73991f2_f49e_11ea_89ca_42010a8a0002level0_row5" class="row_heading level0 row5" >30-34</th>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row5_col0" class="data row5 col0" >52</td>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row5_col1" class="data row5 col1" >9.03%</td>
            </tr>
            <tr>
                        <th id="T_c73991f2_f49e_11ea_89ca_42010a8a0002level0_row6" class="row_heading level0 row6" >35-39</th>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row6_col0" class="data row6 col0" >31</td>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row6_col1" class="data row6 col1" >5.38%</td>
            </tr>
            <tr>
                        <th id="T_c73991f2_f49e_11ea_89ca_42010a8a0002level0_row7" class="row_heading level0 row7" >40+</th>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row7_col0" class="data row7 col0" >12</td>
                        <td id="T_c73991f2_f49e_11ea_89ca_42010a8a0002row7_col1" class="data row7 col1" >2.08%</td>
            </tr>
    </tbody></table>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Running basic calculation for purchase count by age
purchase_count_age = age_group["Purchase ID"].count()

# Running basic calculation for average purchase price by age
average_price_age = age_group["Price"].mean()

# Running basic calculation for total purchase value by age
total_value_age = age_group["Price"].sum()

# Running basic calculation for average total purchase per person by age
average_per_person_age = total_value_age / player_count_age

# Creating DataFrame for Purchasing Analysis (Age)
df6 = pd.DataFrame(
    {
        "Purchase Count": purchase_count_age,
        "Average Purchase Price": average_price_age,
        "Total Purchase Value": total_value_age,
        "Avg Total Purchase per Person": average_per_person_age,
    }
)

# Setting index and formatting average purchase price,total purchase value, and average total purchase per person
df6.index.name = "Age Ranges"
df6.style.format(
    {
        "Average Purchase Price": "${:,.2f}",
        "Total Purchase Value": "${:,.2f}",
        "Avg Total Purchase per Person": "${:,.2f}",
    }
)
```




<style  type="text/css" >
</style><table id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>        <th class="col_heading level0 col3" >Avg Total Purchase per Person</th>    </tr>    <tr>        <th class="index_name level0" >Age Ranges</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002level0_row0" class="row_heading level0 row0" ><10</th>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row0_col0" class="data row0 col0" >23</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row0_col1" class="data row0 col1" >$3.35</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row0_col2" class="data row0 col2" >$77.13</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row0_col3" class="data row0 col3" >$4.54</td>
            </tr>
            <tr>
                        <th id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002level0_row1" class="row_heading level0 row1" >10-14</th>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row1_col0" class="data row1 col0" >28</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row1_col1" class="data row1 col1" >$2.96</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row1_col2" class="data row1 col2" >$82.78</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row1_col3" class="data row1 col3" >$3.76</td>
            </tr>
            <tr>
                        <th id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002level0_row2" class="row_heading level0 row2" >15-19</th>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row2_col0" class="data row2 col0" >136</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row2_col1" class="data row2 col1" >$3.04</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row2_col2" class="data row2 col2" >$412.89</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row2_col3" class="data row2 col3" >$3.86</td>
            </tr>
            <tr>
                        <th id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002level0_row3" class="row_heading level0 row3" >20-24</th>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row3_col0" class="data row3 col0" >365</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row3_col1" class="data row3 col1" >$3.05</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row3_col2" class="data row3 col2" >$1,114.06</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row3_col3" class="data row3 col3" >$4.32</td>
            </tr>
            <tr>
                        <th id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002level0_row4" class="row_heading level0 row4" >25-29</th>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row4_col0" class="data row4 col0" >101</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row4_col1" class="data row4 col1" >$2.90</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row4_col2" class="data row4 col2" >$293.00</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row4_col3" class="data row4 col3" >$3.81</td>
            </tr>
            <tr>
                        <th id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002level0_row5" class="row_heading level0 row5" >30-34</th>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row5_col0" class="data row5 col0" >73</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row5_col1" class="data row5 col1" >$2.93</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row5_col2" class="data row5 col2" >$214.00</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row5_col3" class="data row5 col3" >$4.12</td>
            </tr>
            <tr>
                        <th id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002level0_row6" class="row_heading level0 row6" >35-39</th>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row6_col0" class="data row6 col0" >41</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row6_col1" class="data row6 col1" >$3.60</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row6_col2" class="data row6 col2" >$147.67</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row6_col3" class="data row6 col3" >$4.76</td>
            </tr>
            <tr>
                        <th id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002level0_row7" class="row_heading level0 row7" >40+</th>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row7_col0" class="data row7 col0" >13</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row7_col1" class="data row7 col1" >$2.94</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row7_col2" class="data row7 col2" >$38.24</td>
                        <td id="T_c73f08e4_f49e_11ea_89ca_42010a8a0002row7_col3" class="data row7 col3" >$3.19</td>
            </tr>
    </tbody></table>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Grouping purchase_data by screen names ("SN")
sn_group = purchase_data.groupby("SN")

# Calculating purchase count by "SN"
purchase_count_sn = sn_group["Purchase ID"].count()

# Calculating average purchase price by "SN"
average_price_sn = sn_group["Price"].mean()

# Calculating total purchase value by "SN"
total_value_sn = sn_group["Price"].sum()

# Creating DataFrame for Top Spenders
df7 = pd.DataFrame(
    {
        "Purchase Count": purchase_count_sn,
        "Average Purchase Price": average_price_sn,
        "Total Purchase Value": total_value_sn,
    }
)

# sorting top 5 spenders by total purchase value in descending order and formatting for currency $
df7.sort_values(["Total Purchase Value"], ascending=False).head(5).style.format(
    {
        "Average Purchase Total": "${:,.2f}",
        "Average Purchase Price": "${:,.2f}",
        "Total Purchase Value": "${:,.2f}",
    }
)
```




<style  type="text/css" >
</style><table id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Average Purchase Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >SN</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002level0_row0" class="row_heading level0 row0" >Lisosia93</th>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row0_col0" class="data row0 col0" >5</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row0_col1" class="data row0 col1" >$3.79</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row0_col2" class="data row0 col2" >$18.96</td>
            </tr>
            <tr>
                        <th id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002level0_row1" class="row_heading level0 row1" >Idastidru52</th>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row1_col0" class="data row1 col0" >4</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row1_col1" class="data row1 col1" >$3.86</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row1_col2" class="data row1 col2" >$15.45</td>
            </tr>
            <tr>
                        <th id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002level0_row2" class="row_heading level0 row2" >Chamjask73</th>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row2_col0" class="data row2 col0" >3</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row2_col1" class="data row2 col1" >$4.61</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row2_col2" class="data row2 col2" >$13.83</td>
            </tr>
            <tr>
                        <th id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002level0_row3" class="row_heading level0 row3" >Iral74</th>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row3_col0" class="data row3 col0" >4</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row3_col1" class="data row3 col1" >$3.40</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row3_col2" class="data row3 col2" >$13.62</td>
            </tr>
            <tr>
                        <th id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002level0_row4" class="row_heading level0 row4" >Iskadarya95</th>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row4_col0" class="data row4 col0" >3</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row4_col1" class="data row4 col1" >$4.37</td>
                        <td id="T_c744c3ba_f49e_11ea_89ca_42010a8a0002row4_col2" class="data row4 col2" >$13.10</td>
            </tr>
    </tbody></table>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
# Grouping purchase_data by item ID and item name
item_group = purchase_data.groupby(["Item ID", "Item Name"])

# Calculating item purchase count
item_purchase_count = item_group["SN"].count()

# Calculating item total purchase value
item_total_value = item_group["Price"].sum()

# Calculating item price
item_price = item_total_value / item_purchase_count

# Creating DataFrame for Most Popular Items
df8 = pd.DataFrame(
    {
        "Purchase Count": item_purchase_count,
        "Item Price": item_price,
        "Total Purchase Value": item_total_value,
    }
)

# Sorting 5 most popular items by purchase count in descending order and formatting for currency $
df8.sort_values(["Purchase Count"], ascending=False).head(5).style.format(
    {"Item Price": "${:,.2f}", "Total Purchase Value": "${:,.2f}"}
)
```




<style  type="text/css" >
</style><table id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Item Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >Item ID</th>        <th class="index_name level1" >Item Name</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level0_row0" class="row_heading level0 row0" >178</th>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row0_col0" class="data row0 col0" >12</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row0_col1" class="data row0 col1" >$4.23</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row0_col2" class="data row0 col2" >$50.76</td>
            </tr>
            <tr>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level0_row1" class="row_heading level0 row1" >145</th>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level1_row1" class="row_heading level1 row1" >Fiery Glass Crusader</th>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row1_col0" class="data row1 col0" >9</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row1_col1" class="data row1 col1" >$4.58</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row1_col2" class="data row1 col2" >$41.22</td>
            </tr>
            <tr>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level0_row2" class="row_heading level0 row2" >108</th>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level1_row2" class="row_heading level1 row2" >Extraction, Quickblade Of Trembling Hands</th>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row2_col0" class="data row2 col0" >9</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row2_col1" class="data row2 col1" >$3.53</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row2_col2" class="data row2 col2" >$31.77</td>
            </tr>
            <tr>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level0_row3" class="row_heading level0 row3" >82</th>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level1_row3" class="row_heading level1 row3" >Nirvana</th>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row3_col0" class="data row3 col0" >9</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row3_col1" class="data row3 col1" >$4.90</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row3_col2" class="data row3 col2" >$44.10</td>
            </tr>
            <tr>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level0_row4" class="row_heading level0 row4" >19</th>
                        <th id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002level1_row4" class="row_heading level1 row4" >Pursuit, Cudgel of Necromancy</th>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row4_col0" class="data row4 col0" >8</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row4_col1" class="data row4 col1" >$1.02</td>
                        <td id="T_c74a29e0_f49e_11ea_89ca_42010a8a0002row4_col2" class="data row4 col2" >$8.16</td>
            </tr>
    </tbody></table>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
# Creating DataFrame for Most Profitable Items
df9 = pd.DataFrame(
    {
        "Purchase Count": item_purchase_count,
        "Item Price": item_price,
        "Total Purchase Value": item_total_value,
    }
)

# Sorting 5 most profitable items by total purchase value in descending order and formatting for currency $
df9.sort_values(["Total Purchase Value"], ascending=False).head(5).style.format(
    {"Item Price": "${:,.2f}", "Total Purchase Value": "${:,.2f}"}
)
```




<style  type="text/css" >
</style><table id="T_c74ea254_f49e_11ea_89ca_42010a8a0002" ><thead>    <tr>        <th class="blank" ></th>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >Purchase Count</th>        <th class="col_heading level0 col1" >Item Price</th>        <th class="col_heading level0 col2" >Total Purchase Value</th>    </tr>    <tr>        <th class="index_name level0" >Item ID</th>        <th class="index_name level1" >Item Name</th>        <th class="blank" ></th>        <th class="blank" ></th>        <th class="blank" ></th>    </tr></thead><tbody>
                <tr>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level0_row0" class="row_heading level0 row0" >178</th>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level1_row0" class="row_heading level1 row0" >Oathbreaker, Last Hope of the Breaking Storm</th>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row0_col0" class="data row0 col0" >12</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row0_col1" class="data row0 col1" >$4.23</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row0_col2" class="data row0 col2" >$50.76</td>
            </tr>
            <tr>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level0_row1" class="row_heading level0 row1" >82</th>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level1_row1" class="row_heading level1 row1" >Nirvana</th>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row1_col0" class="data row1 col0" >9</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row1_col1" class="data row1 col1" >$4.90</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row1_col2" class="data row1 col2" >$44.10</td>
            </tr>
            <tr>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level0_row2" class="row_heading level0 row2" >145</th>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level1_row2" class="row_heading level1 row2" >Fiery Glass Crusader</th>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row2_col0" class="data row2 col0" >9</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row2_col1" class="data row2 col1" >$4.58</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row2_col2" class="data row2 col2" >$41.22</td>
            </tr>
            <tr>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level0_row3" class="row_heading level0 row3" >92</th>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level1_row3" class="row_heading level1 row3" >Final Critic</th>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row3_col0" class="data row3 col0" >8</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row3_col1" class="data row3 col1" >$4.88</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row3_col2" class="data row3 col2" >$39.04</td>
            </tr>
            <tr>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level0_row4" class="row_heading level0 row4" >103</th>
                        <th id="T_c74ea254_f49e_11ea_89ca_42010a8a0002level1_row4" class="row_heading level1 row4" >Singed Scalpel</th>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row4_col0" class="data row4 col0" >8</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row4_col1" class="data row4 col1" >$4.35</td>
                        <td id="T_c74ea254_f49e_11ea_89ca_42010a8a0002row4_col2" class="data row4 col2" >$34.80</td>
            </tr>
    </tbody></table>


