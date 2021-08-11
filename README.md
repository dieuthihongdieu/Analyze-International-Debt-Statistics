# Analyze-International-Debt-Statistics

<p  align="center"> <img src="https://res.cloudinary.com/dangdieu1699999/image/upload/v1628669481/istockphoto-1129857593-640x640_uxi6rc.jpg"> </p>

# Overview 
<p>
The project is included in Premium project belong to DataCamp. The data used in this project is provided by The World Bank. It contains both national and regional debt statistics for several countries across the globe as recorded from 1970 to 2015.</p>
<p> Though this project, I understand thoroughly when Writing SQL queries to answer interesting questions about international debt using data from The World Bank.

# Project Tasks
1. The World Bank's international debt data (#1. The World Bank's international debt data)
2. Finding the number of distinct countries
3. Finding out the distinct debt indicators
4. Totaling the amount of debt owed by the countries
5. Country with the highest debt
6. Average amount of debt across indicators
7. The highest amount of principal repayments
8. The most common debt indicator
9. Other viable debt issues and conclusion

# Solution
## 1. The World Bank's international debt data
<p>It's not that we humans only take debts to manage our necessities. A country may also take debt to manage its economy. 
<p> The purpose is to analyze international debt data collected by The World Bank. The dataset contains information about the amount of debt (in USD) owed by developing countries across several categories.<br>
Find the answers to questions like: </p>
<ul>
<li>What is the total amount of debt that is owed by the countries listed in the dataset?</li>
<li>Which country owns the maximum amount of debt and what does that amount look like?</li>
<li>What is the average amount of debt owed by countries across different debt indicators?</li>

<p>Let's first <code>SELECT</code> <em>all</em> of the columns from the <code>international_debt</code> table. Also, Limit the output to the first ten rows to keep the output clean.</p>


```python
%%sql
postgresql:///international_debt
    
select *
from international_debt
limit 10;
```


**Result**

<table>
    <tr>
        <th>country_name</th>
        <th>country_code</th>
        <th>indicator_name</th>
        <th>indicator_code</th>
        <th>debt</th>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>Disbursements on external debt, long-term (DIS, current US$)</td>
        <td>DT.DIS.DLXF.CD</td>
        <td>72894453.700000003</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>Interest payments on external debt, long-term (INT, current US$)</td>
        <td>DT.INT.DLXF.CD</td>
        <td>53239440.100000001</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>PPG, bilateral (AMT, current US$)</td>
        <td>DT.AMT.BLAT.CD</td>
        <td>61739336.899999999</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>PPG, bilateral (DIS, current US$)</td>
        <td>DT.DIS.BLAT.CD</td>
        <td>49114729.399999999</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>PPG, bilateral (INT, current US$)</td>
        <td>DT.INT.BLAT.CD</td>
        <td>39903620.100000001</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>PPG, multilateral (AMT, current US$)</td>
        <td>DT.AMT.MLAT.CD</td>
        <td>39107845</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>PPG, multilateral (DIS, current US$)</td>
        <td>DT.DIS.MLAT.CD</td>
        <td>23779724.300000001</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>PPG, multilateral (INT, current US$)</td>
        <td>DT.INT.MLAT.CD</td>
        <td>13335820</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>PPG, official creditors (AMT, current US$)</td>
        <td>DT.AMT.OFFT.CD</td>
        <td>100847181.900000006</td>
    </tr>
    <tr>
        <td>Afghanistan</td>
        <td>AFG</td>
        <td>PPG, official creditors (DIS, current US$)</td>
        <td>DT.DIS.OFFT.CD</td>
        <td>72894453.700000003</td>
    </tr>
</table>


## 2. Finding the number of distinct countries
***Analysis***
<p>- From the first ten rows, see the amount of debt owed by <em>Afghanistan</em> in the different debt indicators. <br>- Do not know the number of different countries we have on the table. There are repetitions in the country names because a country is most likely to have debt in more than one debt indicator. </p>
<p>- Extract the number of unique countries present in the table. </p>


```python
%%sql
postgresql:///international_debt
SELECT 
    count(distinct country_name)AS total_distinct_countries
FROM international_debt;
```
**Result**
<table>
    <tr>
        <th>total_distinct_countries</th>
    </tr>
    <tr>
        <td>124</td>
    </tr>
</table>




## 3. Finding out the distinct debt indicators
***Analysis***
<p>Analysis: <br> - A total of 124 countries present on the table.<br>-  In the first section, there is a column called <code>indicator_name</code> that briefly specifies the purpose of taking the debt. Just beside that column, there is another column called <code>indicator_code</code> which symbolizes the category of these debts.<br> - Knowing about these various debt indicators will help us to understand the areas in which a country can possibly be indebted to. </p>


```python
%%sql
postgresql:///international_debt
select distinct indicator_code as distinct_debt_indicators
from international_debt
order by distinct_debt_indicators;
```
<table>
    <tr>
        <th>distinct_debt_indicators</th>
    </tr>
    <tr>
        <td>DT.AMT.BLAT.CD</td>
    </tr>
    <tr>
        <td>DT.AMT.DLXF.CD</td>
    </tr>
    <tr>
        <td>DT.AMT.DPNG.CD</td>
    </tr>
    <tr>
        <td>DT.AMT.MLAT.CD</td>
    </tr>
    <tr>
        <td>DT.AMT.OFFT.CD</td>
    </tr>
    <tr>
        <td>DT.AMT.PBND.CD</td>
    </tr>
    <tr>
        <td>DT.AMT.PCBK.CD</td>
    </tr>
    <tr>
        <td>DT.AMT.PROP.CD</td>
    </tr>
    <tr>
        <td>DT.AMT.PRVT.CD</td>
    </tr>
    <tr>
        <td>DT.DIS.BLAT.CD</td>
    </tr>
    <tr>
        <td>DT.DIS.DLXF.CD</td>
    </tr>
    <tr>
        <td>DT.DIS.MLAT.CD</td>
    </tr>
    <tr>
        <td>DT.DIS.OFFT.CD</td>
    </tr>
    <tr>
        <td>DT.DIS.PCBK.CD</td>
    </tr>
    <tr>
        <td>DT.DIS.PROP.CD</td>
    </tr>
    <tr>
        <td>DT.DIS.PRVT.CD</td>
    </tr>
    <tr>
        <td>DT.INT.BLAT.CD</td>
    </tr>
    <tr>
        <td>DT.INT.DLXF.CD</td>
    </tr>
    <tr>
        <td>DT.INT.DPNG.CD</td>
    </tr>
    <tr>
        <td>DT.INT.MLAT.CD</td>
    </tr>
    <tr>
        <td>DT.INT.OFFT.CD</td>
    </tr>
    <tr>
        <td>DT.INT.PBND.CD</td>
    </tr>
    <tr>
        <td>DT.INT.PCBK.CD</td>
    </tr>
    <tr>
        <td>DT.INT.PROP.CD</td>
    </tr>
    <tr>
        <td>DT.INT.PRVT.CD</td>
    </tr>
</table>


## 4. Totaling the amount of debt owed by the countries
***Analysis***
<p>- As mentioned earlier, the financial debt of a particular country represents its economic state. But if we were to project this on an overall global scale, how will we approach it?</p>
<p>- Finding out the total amount of debt (in USD) that is owed by the different countries makes a sense of how the overall economy of the entire world is holding up.</p>


```python
%%sql
postgresql:///international_debt
SELECT 
    round(sum(debt)/1000000, 2) as total_debt
FROM international_debt; 
```
<table>
    <tr>
        <th>total_debt</th>
    </tr>
    <tr>
        <td>3079734.49</td>
    </tr>
</table>

## 5. Country with the highest debt
***Analysis***
<p>"Human beings cannot comprehend very large or very small numbers. It would be useful for us to acknowledge that fact." - <a href="https://en.wikipedia.org/wiki/Daniel_Kahneman">Daniel Kahneman</a>. That is more than <em>3 million <strong>million</strong></em> USD, an amount which is really hard to fathom. </p>
<p>- After having the exact total of the amounts of debt owed by several countries, let's now find out the country that owns the highest amount of debt along with the amount. <br><strong>Note</strong> that this debt is the sum of different debts owed by a country across several categories. <br> => Help understand more about the country in terms of its socio-economic scenarios. </p>

```python
%%sql
postgresql:///international_debt
SELECT 
    country_name, 
    sum(debt) as total_debt
FROM international_debt
GROUP BY country_name
ORDER BY total_debt DESC
Limit 1;
```

**Result**

<table>
    <tr>
        <th>country_name</th>
        <th>total_debt</th>
    </tr>
    <tr>
        <td>China</td>
        <td>285793494734.200001568</td>
    </tr>
</table>


## 6. Average amount of debt across indicators
***Analysis***
<p>- So, it was <em>China</em>. A more in-depth breakdown of China's debts can be found <a href="https://datatopics.worldbank.org/debt/ids/country/CHN">here</a>. </p>
<p> - Having a brief overview of the dataset and a few of its summary statistics.<br> - Have an idea of the different debt indicators in which the countries owe their debts. <br> => Dig even further to find out on an average how much debt a country owes? <br> => Help to have a better sense of the distribution of the amount of debt across different indicators.</p>


```python
%%sql
postgresql:///international_debt
SELECT 
    indicator_code AS debt_indicator,
    indicator_name,
    avg(debt) as average_debt
FROM international_debt
GROUP BY debt_indicator, indicator_name
ORDER BY average_debt desc
limit 10;
```

  **Result**




<table>
    <tr>
        <th>debt_indicator</th>
        <th>indicator_name</th>
        <th>average_debt</th>
    </tr>
    <tr>
        <td>DT.AMT.DLXF.CD</td>
        <td>Principal repayments on external debt, long-term (AMT, current US$)</td>
        <td>5904868401.499193612</td>
    </tr>
    <tr>
        <td>DT.AMT.DPNG.CD</td>
        <td>Principal repayments on external debt, private nonguaranteed (PNG) (AMT, current US$)</td>
        <td>5161194333.812658349</td>
    </tr>
    <tr>
        <td>DT.DIS.DLXF.CD</td>
        <td>Disbursements on external debt, long-term (DIS, current US$)</td>
        <td>2152041216.890243888</td>
    </tr>
    <tr>
        <td>DT.DIS.OFFT.CD</td>
        <td>PPG, official creditors (DIS, current US$)</td>
        <td>1958983452.859836046</td>
    </tr>
    <tr>
        <td>DT.AMT.PRVT.CD</td>
        <td>PPG, private creditors (AMT, current US$)</td>
        <td>1803694101.963265321</td>
    </tr>
    <tr>
        <td>DT.INT.DLXF.CD</td>
        <td>Interest payments on external debt, long-term (INT, current US$)</td>
        <td>1644024067.650806481</td>
    </tr>
    <tr>
        <td>DT.DIS.BLAT.CD</td>
        <td>PPG, bilateral (DIS, current US$)</td>
        <td>1223139290.398230108</td>
    </tr>
    <tr>
        <td>DT.INT.DPNG.CD</td>
        <td>Interest payments on external debt, private nonguaranteed (PNG) (INT, current US$)</td>
        <td>1220410844.421518983</td>
    </tr>
    <tr>
        <td>DT.AMT.OFFT.CD</td>
        <td>PPG, official creditors (AMT, current US$)</td>
        <td>1191187963.083064523</td>
    </tr>
    <tr>
        <td>DT.AMT.PBND.CD</td>
        <td>PPG, bonds (AMT, current US$)</td>
        <td>1082623947.653623188</td>
    </tr>
</table>

## 7. The highest amount of principal repayments
***Analysis***
<p> - The indicator <code>DT.AMT.DLXF.CD</code> tops the chart of average debt. This category includes repayment of long term debts. Countries take on long-term debt to acquire immediate capital. More information about this category can be found <a href="https://datacatalog.worldbank.org/principal-repayments-external-debt-long-term-amt-current-us-0">here</a>. </p>
<p> - An interesting observation in the above finding is that there is a huge difference in the amounts of the indicators after the second one.<br> => The first two indicators might be the most severe categories in which the countries owe their debts.</p>
<p>-  Since not all the countries suffer from the same kind of economic disturbances, Which country owes the highest amount of debt in the category of long term debts (<code>DT.AMT.DLXF.CD</code>) ? . <br> => Understand that particular country's economic condition a bit more specifically. </p>

**Result**
<table>
    <tr>
        <th>country_name</th>
        <th>indicator_name</th>
    </tr>
    <tr>
        <td>China</td>
        <td>Principal repayments on external debt, long-term (AMT, current US$)</td>
    </tr>
</table>

## 8. The most common debt indicator
***Analysis***
<p>- China has the highest amount of debt in the long-term debt (<code>DT.AMT.DLXF.CD</code>) category. This is verified by <a href="https://data.worldbank.org/indicator/DT.AMT.DLXF.CD?end=2018&most_recent_value_desc=true">The World Bank</a>. It is often a good idea to verify our analyses like this since it validates that our investigations are correct. </p>
<p> - Long-term debt is the topmost category when it comes to the average amount of debt. <br>- But is it the most common indicator in which the countries owe their debt? </p>


```python
%%sql
postgresql:///international_debt
    
SELECT 
    indicator_code,
    COUNT(indicator_code) AS indicator_count
FROM international_debt
GROUP BY indicator_code
ORDER BY indicator_count DESC, indicator_code DESC
LIMIT 20;
```

**Result**

<table>
    <tr>
        <th>indicator_code</th>
        <th>indicator_count</th>
    </tr>
    <tr>
        <td>DT.INT.OFFT.CD</td>
        <td>124</td>
    </tr>
    <tr>
        <td>DT.INT.MLAT.CD</td>
        <td>124</td>
    </tr>
    <tr>
        <td>DT.INT.DLXF.CD</td>
        <td>124</td>
    </tr>
    <tr>
        <td>DT.AMT.OFFT.CD</td>
        <td>124</td>
    </tr>
    <tr>
        <td>DT.AMT.MLAT.CD</td>
        <td>124</td>
    </tr>
    <tr>
        <td>DT.AMT.DLXF.CD</td>
        <td>124</td>
    </tr>
    <tr>
        <td>DT.DIS.DLXF.CD</td>
        <td>123</td>
    </tr>
    <tr>
        <td>DT.INT.BLAT.CD</td>
        <td>122</td>
    </tr>
    <tr>
        <td>DT.DIS.OFFT.CD</td>
        <td>122</td>
    </tr>
    <tr>
        <td>DT.AMT.BLAT.CD</td>
        <td>122</td>
    </tr>
    <tr>
        <td>DT.DIS.MLAT.CD</td>
        <td>120</td>
    </tr>
    <tr>
        <td>DT.DIS.BLAT.CD</td>
        <td>113</td>
    </tr>
    <tr>
        <td>DT.INT.PRVT.CD</td>
        <td>98</td>
    </tr>
    <tr>
        <td>DT.AMT.PRVT.CD</td>
        <td>98</td>
    </tr>
    <tr>
        <td>DT.INT.PCBK.CD</td>
        <td>84</td>
    </tr>
    <tr>
        <td>DT.AMT.PCBK.CD</td>
        <td>84</td>
    </tr>
    <tr>
        <td>DT.INT.DPNG.CD</td>
        <td>79</td>
    </tr>
    <tr>
        <td>DT.AMT.DPNG.CD</td>
        <td>79</td>
    </tr>
    <tr>
        <td>DT.INT.PBND.CD</td>
        <td>69</td>
    </tr>
    <tr>
        <td>DT.AMT.PBND.CD</td>
        <td>69</td>
    </tr>
</table>


## 9. Other viable debt issues and conclusion
***Analysis***
<p> - There are a total of six debt indicators in which all the countries listed in our dataset have taken debt. The indicator <code>DT.AMT.DLXF.CD</code> is also there in the list. <br>=> <strong>Note: </strong> A clue that all these countries are suffering from a common economic issue.<br> But that is not the end of the story, but just a part of the story.</p>
<p>Let's change tracks from <code>debt_indicator</code>s now and focus on the amount of debt again. Let's find out the maximum amount of debt that each country has.<br> => Change identify the other plausible economic issues a country might be going through.</p>
<p>


```python
%%sql
postgresql:///international_debt
select country_name,
       max(debt) as maximum_debt
from international_debt
group by country_name
order by maximum_debt desc
limit 10;

```

<table>
    <tr>
        <th>country_name</th>
        <th>maximum_debt</th>
    </tr>
    <tr>
        <td>China</td>
        <td>96218620835.699996948</td>
    </tr>
    <tr>
        <td>Brazil</td>
        <td>90041840304.100006104</td>
    </tr>
    <tr>
        <td>Russian Federation</td>
        <td>66589761833.5</td>
    </tr>
    <tr>
        <td>Turkey</td>
        <td>51555031005.800003052</td>
    </tr>
    <tr>
        <td>South Asia</td>
        <td>48756295898.199996948</td>
    </tr>
    <tr>
        <td>Least developed countries: UN classification</td>
        <td>40160766261.599998474</td>
    </tr>
    <tr>
        <td>IDA only</td>
        <td>34531188113.199996948</td>
    </tr>
    <tr>
        <td>India</td>
        <td>31923507000.799999237</td>
    </tr>
    <tr>
        <td>Indonesia</td>
        <td>30916112653.799999237</td>
    </tr>
    <tr>
        <td>Kazakhstan</td>
        <td>27482093686.400001526</td>
    </tr>
</table>

