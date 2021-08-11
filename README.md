# Analyze-International-Debt-Statistics
## 1. The World Bank's international debt data
<p>It's not that we humans only take debts to manage our necessities. A country may also take debt to manage its economy. For example, infrastructure spending is one costly ingredient required for a country's citizens to lead comfortable lives. <a href="https://www.worldbank.org">The World Bank</a> is the organization that provides debt to countries.</p>
<pI am  going to analyze international debt data collected by The World Bank. The dataset contains information about the amount of debt (in USD) owed by developing countries across several categories. **find the answers to questions like: </p>
<ul>
<li>What is the total amount of debt that is owed by the countries listed in the dataset?</li>
<li>Which country owns the maximum amount of debt and what does that amount look like?</li>
<li>What is the average amount of debt owed by countries across different debt indicators?</li>
</ul>
<p><img src="https://assets.datacamp.com/production/project_754/img/image.jpg" alt></p>
<p>The first line of code connects us to the <code>international_debt</code> database where the table <code>international_debt</code> is residing. Let's first <code>SELECT</code> <em>all</em> of the columns from the <code>international_debt</code> table. Also, we'll limit the output to the first ten rows to keep the output clean.</p>
