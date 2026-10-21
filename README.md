<h1 align="center">📊 Data Jobs Salary &amp; Skills Analysis</h1>

<p align="center">
  <b>Which data roles pay the most, which skills are most requested, and do more skills mean better pay?</b><br>
  An Excel project built with Power Query, the Data Model, DAX, PivotTables and slicers.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Excel-Analysis-217346?logo=microsoftexcel&logoColor=white" alt="Excel">
  <img src="https://img.shields.io/badge/Power%20Query-ETL-F2C811" alt="Power Query">
  <img src="https://img.shields.io/badge/DAX-Measures-4C72B0" alt="DAX">
  <img src="https://img.shields.io/badge/PivotTables-Slicers-F37626" alt="PivotTables">
</p>

<hr>

<h2>📑 Table of Contents</h2>

<ol>
  <li><a href="#overview">Overview</a><br></li>
  <li><a href="#questions">The Questions</a><br></li>
  <li><a href="#tools">Tools I Used</a><br></li>
  <li><a href="#preparation">Data Preparation with Power Query</a><br></li>
  <li><a href="#analysis">The Analysis</a><br></li>
  <li><a href="#learned">What I Learned</a><br></li>
  <li><a href="#challenges">Challenges I Faced</a><br></li>
  <li><a href="#run">How to Use This Project</a><br></li>
  <li><a href="#conclusion">Conclusion</a></li>
</ol>

<hr>

<h1 id="overview">🔎 Overview</h1>

<h3>Welcome to my analysis of data job salaries and skills.</h3>

<p>
This project explores what data professionals earn and which skills employers ask for.
I cleaned the data with <b>Power Query</b>, linked two tables in the <b>Data Model</b>,
calculated results with <b>DAX</b> measures, and presented them with <b>PivotTables, slicers and charts</b>.
</p>

<details>
  <summary><b>👉 Click to see what the data contains</b></summary>
  <br>
  <ul>
    <li><b><code>data_jobs_salary</code>:</b> 1,000 job postings with job title, location, platform, job type and salary</li>
    <li><b><code>data_jobs_skills</code>:</b> one row per job and skill, linked to the salary table by <code>job_id</code></li>
    <li><b>10 job titles</b>, such as Data Analyst, Data Engineer, Data Scientist and Business Analyst</li>
  </ul>
</details>

<br>

<h1 id="questions">❓ The Questions</h1>

<h3>Below are the questions I wanted to answer in this project:</h3>

<ol>
  <li><b>How does the median salary compare across data job titles?</b></li>
  <br>
  <li><b>How do salaries in India compare with salaries outside India?</b></li>
  <br>
  <li><b>Do more skills in a job posting mean better pay?</b></li>
  <br>
  <li><b>What are the top skills, how common are they, and what do they pay?</b></li>
</ol>

<br>

<h1 id="tools">🛠️ Tools I Used</h1>

<table align="center">
  <thead>
    <tr>
      <th align="left">Tool / Feature</th>
      <th align="left">Purpose</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><b>📗 Microsoft Excel</b></td><td>Main analysis and reporting tool</td></tr>
    <tr><td><b>🔧 Power Query</b></td><td>Cleaning and reshaping the raw data</td></tr>
    <tr><td><b>🗃️ Data Model (Power Pivot)</b></td><td>Linking the salary and skills tables</td></tr>
    <tr><td><b>🧮 DAX</b></td><td>Measures for median salary, skills per job and skill likelihood</td></tr>
    <tr><td><b>📋 PivotTables</b></td><td>Summarizing salary and skills by job title</td></tr>
    <tr><td><b>🎚️ Slicers</b></td><td>Filtering by country and job title</td></tr>
    <tr><td><b>📊 Charts</b></td><td>Scatter plot with trendline and a combo chart (bars and markers)</td></tr>
    <tr><td><b>🔀 Git &amp; GitHub</b></td><td>Version control and sharing the project</td></tr>
  </tbody>
</table>

<br>

<h1 id="preparation">🧹 Data Preparation with Power Query</h1>

<h3>Cleaning the data before analysis keeps every result accurate.</h3>

<h2>1️⃣ Job Skills table: <code>data_jobs_skills</code></h2>

<p>
The raw <code>job_skills</code> column stored all skills of a job in one text cell.
I split it so that <b>each skill gets its own row</b>.
</p>

<ol>
  <li>Removed other columns, keeping only <code>job_id</code> and the skills</li>
  <li>Replaced the characters <code>[</code>, <code>]</code> and <code>'</code></li>
  <li>Split the skills column by delimiter</li>
  <li>Unpivoted the skill columns into rows</li>
  <li>Trimmed the text and capitalized each word</li>
  <li>Added a conditional column and renamed the columns</li>
</ol>

<p align="center">
  <img src="https://github.com/Sneha-AT12/data-jobs-salary-skills-analysis/blob/88cd65a763e55dbfe82db0554e44c70ea062bef0/1_power_query_skills.png" width="800" alt="Power Query steps for the job skills table">
</p>
<p align="center"><i>Power Query: one row per job and skill (for example SQL, Python, AWS for job 10001).</i></p>

<hr>

<h2>2️⃣ Job Salary table: <code>data_jobs_salary</code></h2>

<ol>
  <li>Promoted headers and changed data types</li>
  <li>Replaced the text <code>"via "</code> in <code>job_via</code> to get clean platform names</li>
  <li>Renamed the posting date column and inserted <b>Month</b> and <b>Date</b> columns</li>
  <li>Inserted a multiplication step to prepare the salary values</li>
  <li>Reordered the columns and added an <b>Index</b> column for <code>job_id</code></li>
</ol>

<p align="center">
  <img src="images/2_power_query_salary.png" width="800" alt="Power Query steps for the job salary table">
</p>
<p align="center"><i>Power Query: 1,000 unique jobs across 10 job titles.</i></p>

<br>

<h1 id="analysis">📈 The Analysis</h1>

<h2>1️⃣ How do salaries compare across job titles, and India vs. the rest?</h2>

<p>
I built a PivotTable with the <b>median salary</b> for each job title and split it into
<b>India</b> and <b>Non-India</b> using DAX measures.
</p>

<p align="center">
  <img src="images/3_median_salary_india.png" width="650" alt="Median salary by job title: overall, India and non-India">
</p>
<p align="center"><i>Median salary by job title: overall, India and Non-India.</i></p>

<h3>💡 Insights</h3>

<ul>
  <li><b>Data Analyst</b> has the same median in India as overall (<b>1,00,500</b>), and a lower median outside India (<b>90,000</b>).</li>
  <li><b>Senior Data Scientist</b> (1,57,500) and <b>Software Engineer</b> (1,57,500) have the highest overall medians in this table.</li>
  <li><b>Business Analyst</b> pays less in India (64,800) than outside India (85,120).</li>
  <li><b>Cloud Engineer</b> has no India value, so there are no India postings with salary for that role.</li>
  <li>The overall median across all jobs is <b>1,18,500</b>. It is <b>1,11,175</b> in India and <b>1,15,000</b> outside India.</li>
</ul>

<hr>

<h2>2️⃣ Do more skills get you better pay?</h2>

<p>
For each job title, I calculated the <b>median salary</b> and the <b>average number of skills per job posting</b>,
then plotted them against each other with a trendline.
</p>

<p align="center">
  <img src="images/4_salary_vs_skills.png" width="750" alt="Scatter plot: do more skills get you better pay?">
</p>
<p align="center"><i>Each dot is a job title. The dotted line is the trend.</i></p>

<h3>💡 Insights</h3>

<ul>
  <li>The trendline slopes upward, so roles that request <b>more skills tend to pay more</b>.</li>
  <li><b>Senior Data Engineer</b> sits at the top right: the most skills per posting (about 8) and a high median salary (about $147K).</li>
  <li><b>Data Engineer</b> requests about 7 skills per posting and has a median of $125K.</li>
  <li><b>Data Analyst</b> ($90K, about 3.6 skills) and <b>Business Analyst</b> ($85K, about 3.3 skills) sit at the bottom left.</li>
  <li><b>Senior Data Scientist</b> has the highest median salary (about $155K) with only about 5 skills per posting, so skill count is not the only factor.</li>
</ul>

<hr>

<h2>3️⃣ What are the top skills of data professionals?</h2>

<p>
The combo chart shows the <b>median salary</b> of jobs that ask for each skill (bars)
and the <b>skill likelihood</b>, the share of postings that mention it (markers).
</p>

<p align="center">
  <img src="images/5_top_skills.png" width="750" alt="Top skills: median salary and skill likelihood">
</p>
<p align="center"><i>Bars: median salary for the skill. Markers: how often the skill appears in postings.</i></p>

<h3>💡 Insights</h3>

<ul>
  <li><b>Python</b> (about 54%) and <b>SQL</b> (above 50%) are by far the most requested skills.</li>
  <li><b>Spark</b> has the highest median salary at 1,40,000 but appears in only about 16% of postings.</li>
  <li><b>AWS</b> (1,35,000) and <b>Java</b> (1,34,241) also pay highly and are less common than Python and SQL.</li>
  <li><b>Python</b> combines a strong median (1,25,000) with very high demand, which makes it a safe skill to learn.</li>
  <li><b>Excel</b> has the lowest median of the top 10 skills, but it still appears in about 19% of postings.</li>
</ul>

<br>

<h1 id="learned">🎓 What I Learned</h1>

<ol>
  <li><b>Power Query:</b> splitting, unpivoting and cleaning text turns messy columns into analysis-ready tables.</li>
  <br>
  <li><b>Data Model:</b> linking tables by <code>job_id</code> lets one PivotTable use fields from both tables.</li>
  <br>
  <li><b>DAX measures:</b> median salary, skills per job and skill likelihood need measures, not simple sums.</li>
  <br>
  <li><b>Chart choice:</b> scatter plots show relationships, and combo charts show two measures on one axis pair.</li>
</ol>

<br>

<h1 id="challenges">🧗 Challenges I Faced</h1>

<ol>
  <li><b>Skills stored as text:</b> each job had all its skills in one cell, so I had to split and unpivot them.</li>
  <br>
  <li><b>Medians vs. averages:</b> the median needs DAX measures and is less affected by extreme salaries.</li>
  <br>
  <li><b>Small groups:</b> some job titles have few postings in India, so medians can be unreliable.</li>
  <br>
  <li><b>Two measures in one chart:</b> salary and percentage needed a secondary axis.</li>
</ol>

<br>

<h1 id="run">▶️ How to Use This Project</h1>

<ol>
  <li>Download <code>DAX.xlsx</code> from this repository.</li>
  <br>
  <li>Open it in <b>Microsoft Excel</b> (desktop version, because the Data Model and DAX need it).</li>
  <br>
  <li>Go to <b>Data → Queries &amp; Connections</b> to see the Power Query steps.</li>
  <br>
  <li>Open the analysis sheets and use the <b>slicers</b> to filter by country and job title.</li>
</ol>

<h3>📁 Project Structure</h3>

```text
📦 data-jobs-salary-skills-analysis
 ┣ 📂 images/
 ┃ ┣ 🖼️ 1_power_query_skills.png
 ┃ ┣ 🖼️ 2_power_query_salary.png
 ┃ ┣ 🖼️ 3_median_salary_india.png
 ┃ ┣ 🖼️ 4_salary_vs_skills.png
 ┃ ┗ 🖼️ 5_top_skills.png
 ┣ 📗 DAX.xlsx
 ┗ 📄 README.md
```

<br>

<h1 id="conclusion">✅ Conclusion</h1>

<p>
This project shows how Excel can handle a complete analysis: clean the data with Power Query, model it with DAX, and present it with PivotTables and charts.
The results show that senior and engineering roles earn the most, that Python and SQL are the most requested skills, and that roles asking for more skills tend to pay more.
</p>

<hr>

<p align="center">⭐ If you found this project useful, please consider giving it a star!</p>
