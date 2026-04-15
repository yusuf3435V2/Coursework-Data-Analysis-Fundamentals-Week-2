# WEEK 8: DATA ANALYSIS
- database.describe(): Shows numeric stats for numeric columns, gives the count, mean, std, min, quartiles and max value.
- database.info(): Gives column information including datatype and name.
- database.apply(): Applies a function to the data.
- pd.to_datetime(shark_data['date']): Converts data into a datetime object.
- pd.to_numeric(shark_data['age']): Converts the data into a numeric value.
- shark_data['date'].dt.year, shark_data['date'].dt.month, shark_data['date'].dt.day: Access date time values from a datetime object.

## GOOGLE PROMPT
MODULE 1 - START WRITING PROMPTS LIKE A PRO

- Prompting is the process of providing specific instructions to a Gen AI tool to receive new information or to achieve a desired outcome on a task.

- Multimodal (Text, images, Sound, Videos, code)

- 5 step frame work
1) TASK - What you want the AI to do
Persona - "Act as an expert"
Format - "Organize in table"
2) CONTEXT - The more context, the better output
"Turning 26 yrs old"
3) REFERENCES - Examples 
4) EVALUATE - Check if the result is what I wanted
5) ITERATE - Keep adding things.

- Thoughtfully Create Really Excellent Inputs 

- ITERATION METHODS: 
1) Revisit the prompting framework
2) Separate Prompts into shorter sentences
3) Trying different phrasing or switching to an analogous task
4) Introduce Constraints

- Hallucinations & Biases are common problems sometimes. So always be responsible and evaluate your results. 

MODULE 2 -  DESIGN PROMPTS FOR EVERYDAY WORK TASKS

- Have a prompt library. 
- Instead of a generic "Write a summary" be specific "Write a summary in a friendly, easy to understand tone like explaining to a curious friend"

MODULE 3 - SPEED UP DATA ANALYSIS & PRESENTATION BUILDING

- Be careful of the data that you are entering into the Gen AI. 
- It can help in Google sheets for formulas and trends if u include the sheet.
- Build a presentation prompt structure.

MODULE 4 - USE AI AS A CREATOR OR EXPERT PARTNER

- Prompt Chaining: A way of guiding Gen AI tools through a series of interconnected prompts, adding new layers of complexity along the way. example: author trying to market his book using Google AI studio

- 2 ways: 
1) Chain of thought prompting: Ask AI to explain its reasoning in a step-by-step process (explain your thought process)
2) Tree of thought prompting: Allows multiple reasoning paths and branches simultaneously. Helpful for abstract and complex problems. 
Pro-tip: use them combined 

- Meta prompting: Use AI to generate a prompt for you, when you get stuck.

- AI AGENT: An expert designed to help with tasks and answer questions. Ex: coding agent, marketing agent, learning agent, friend etc.

- AGENT SIM: simulation agent. [Interviewer - Job interviews]
- AGENT X: Agent for expert feedback.
 
I write in a strict, formal manner and use bullet points a lot.

## Incident Report: System Availability Variance (April 14, 2026)

**Executive Summary**
A localized system instability resulted in intermittent service degradation for a duration of 135 minutes. The incident impacted a calculated incidence of approximately 15% of active user sessions. Systematic mitigation was achieved within 135 minutes of detection, with full restoration of standard operational parameters completed by 15:00.

### 1. Incident Timeline and Technical Metrics
* **Total Observation Period:** 10:15 – 12:30 (Initial Mitigation)
* **Total System Recovery:** 15:00 (Final Deployment)
* **Detection Mechanism:** Automated Monitoring Latency Thresholds
* **Session Impact Rate:** $\approx 15\%$ of total concurrent users
* **Status Update Frequency:** $t = 30$ minutes

### 2. Analysis and Causal Factors
The primary root cause is currently under quantitative review. Preliminary data suggests a high probability of a memory leak; however, the correlation between the outage and a concurrent load spike is being evaluated to determine if the latter acted as a primary catalyst or a secondary stressor.

### 3. Mitigation and Response Protocols
Initial recovery was facilitated through a horizontal scaling of instances to distribute the load and stabilize the environment. Comprehensive monitoring remains active to ensure system stability. 

### 4. Direct Communication Logistics
* **External Updates:** Status page synchronization maintained at 30-minute intervals.
* **Direct Notification:** Affected users ($N \approx 15\%$ of active sessions) were notified via email at 13:00.

### 5. Strategic Next Steps
A formal post-mortem analysis will be conducted to isolate the precise variable responsible for the memory depletion. The timeline for a permanent code-level correction is currently TBD, pending the completion of the diagnostic phase.

## MAKING BAR CHARTS
```python
alt.Chart(delay_chart_data).mark_bar().encode(
    #Y axis settings
    y=alt.Y( 
        "delay_type:N",
        sort="-x",
        title=None
    ),
    #X axis settings
    x=alt.X(
        "minutes_lost:Q",
        title="Total Minutes Lost"
    ),
    # colour settings
    # uses a condition and checks if a column is a highlight, and then colours in a different column
    color=alt.condition(
        alt.datum.highlight,
        alt.value("#d62728"),
        alt.value("#9ecae1")
    ),
    # a tool tip is when hovering you get information on the data
    tooltip=[
        alt.Tooltip("delay_type:N", title="Delay Type"),
        alt.Tooltip("minutes_lost:Q", title="Minutes Lost", format=",")
    ]
    # properties of the chart
).properties(
    width=700,
    height=300,
    title="Total Minutes Lost by Delay Type"
)
```

## MAKING PIE CHARTS
```python
# Clean the data for what you want to make a pie chart on
injury_status = michigan_laser["injury"].value_counts()
print(injury_status)

#Make the columns that u want for the pie chart
injury_percent = (injury_status / injury_status.sum()) * 100
harm_df = injury_percent.reset_index()
harm_df.columns = ['injury', 'percentage']

#Initialise the pie chart
alt.Chart(harm_df).mark_arc().encode(
    theta=alt.Theta(field="percentage", type="quantitative"),
    color=alt.Color(field="injury", type="nominal"),
    tooltip=[
        alt.Tooltip("injury", title="Harmful?"),
        alt.Tooltip("percentage", format=".2f")
    ]
).properties(
    title="Percentage of harmful injuries from laser"
)
```
