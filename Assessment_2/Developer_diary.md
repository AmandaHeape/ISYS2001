# 28/09/2026 - Worked Example  
Today I created a small fake CSV and manually calculated totals, categories, and monthly spending.
I asked Copilot to help structure the example, but I manually checked all calculations.
This step helped me understand what functions I will need later (category grouping, monthly totals, etc.).

Prompt: Generate a fake CSV file with 10-20 transactions with catagories, merchant, dates, amount ect

CoPilot: I’ll give you two things:

A CSV you can paste directly into a file

A Pandas‑ready version you can drop straight into Colab

No tools needed — just pure data you can copy.

# 3/10/2026 - Progress update
This week I made substantial progress across multiple sections of the project, moving from initial pseudocode into functional code and refining several components based on testing.

I created pseudocode for each section 
1) Testing and input 
2) Data cleaning
3) Calculate spending summaries
4) Savings goal planner
5) Visuals
6) Alfies Personalised insights
7) Gradio
8) Testing


   <img width="485" height="174" alt="Screenshot 2026-10-03 160450" src="https://github.com/user-attachments/assets/99fe4e8c-e9ac-4f5a-88f5-89e0396426e9" />
<img width="489" height="180" alt="Screenshot 2026-10-03 160331" src="https://github.com/user-attachments/assets/cd263959-41c9-46f9-9afd-897380e1ce5b" />
<img width="495" height="179" alt="Screenshot 2026-10-03 160013" src="https://github.com/user-attachments/assets/63d32c6b-0af5-484d-beae-24790d97ff37" />
<img width="485" height="146" alt="Screenshot 2026-10-03 155916" src="https://github.com/user-attachments/assets/33ca0315-4cab-4187-b210-db65911a571a" />
<img width="484" height="160" alt="Screenshot 2026-10-03 155819" src="https://github.com/user-attachments/assets/a49cbcec-b617-4c32-9b2d-731d996b3df7" />
<img width="485" height="156" alt="Screenshot 2026-10-03 155633" src="https://github.com/user-attachments/assets/720536a2-2357-4618-8cd5-16ce48f7e681" />

1. Testing and input handling
Originally, my input section only supported CSV uploads. After testing with real bank data, I realised this wasn’t user‑friendly. I expanded the input logic to support PDF bank statements, using the Google API to extract structured transaction data.
During testing, Gemini produced incorrect outputs because it was using the wrong model. I identified the issue, rejected the faulty output, and corrected the model to "gemini-3.5-flash", which successfully processed the data.
Screenshots have been saved as evidence of debugging.

2. Data Cleaning
I generated the initial cleaning code from my pseudocode, then asked Gemini for feedback.
Here is Geminis output:
My Thoughts on Your Pseudocode
Your plan is excellent and covers the fundamentals:

Converting the date column to actual date objects so we can sort chronologically.
Removing rows with missing or invalid amounts to keep our math accurate.
Sorting from oldest to newest so our monthly timelines make sense.
Extra Things That Would Be Highly Beneficial to Include:
To make your data processing completely robust and prevent errors down the line, I suggest we also address these common CSV pitfalls in our code:

Standardising Case & Stripping Spaces in Text Columns: Sometimes text columns contain accidental leading/trailing spaces (e.g., ' Groceries ' or 'groceries'). Converting text categories and merchants to standard title case (e.g., 'Groceries') and stripping spaces ensures our calculations group them together correctly.
Handling Empty or Missing Merchant/Category Names: If a transaction has a valid amount but a blank merchant or category, we should either fill them with a default value like 'Unknown' or drop those rows entirely so our grouping doesn't crash.
Filtering Out Non-Positive Amounts (Optional but Recommended): In some files, refunds (negative amounts) or zero-value transactions might exist. For a pure spending analysis, we should decide how to handle negative values or zero values (e.g., treat them as income/adjustments, or ignore them).

I accepted these suggestions and implemented them. So the cleaning process now handles real‑world bank data more reliably.

3. Spending Summaries
The core spending summary functions were generated based on pseudocode. Refinement is still pending, especially around grouping logic and improving readability.

4. Savings Goal Planner
The initial version was implemented, but I've identified limitations. The current logic is too simplistic and doesn’t use realistic savings behaviour.
Planned improvements:
- Allow users to select savings categories (e.g, house, car, holiday) I will prompt them with suggestions.
- Add priority ranking and timeframe
- Generate a savings forecast, adding this to the visual component will work nicely
- Assess achievability based on current transaction history
- Produce a savings timeline

5. Alfie’s Personalised Insights 
Alfie currently explains spending patterns, but I plan to expand his insights. I will include feasible budgeting suggestions based on spending history, expenses and income. Savings commentary and Category specific savings guidance (non‑advisory).

6. Visuals
I uses gemini to generate the code to add visuals based on my pseudocode:

Category spending (pie chart)
Monthly totals (bar chart)
Spending over time (line graph)
Merchant totals (horizontal bar chart)
Output was accepted, the future visuals pending will include savings timelines and goal progress charts.

7. Gradio Interface and 8. Testing
Planning phase -still to be implemented, pseudocode written.

Next steps:
Build the on the savings planner
Add savings timeline visuals
Possible integration of a stock portfolio section
Refine Alfie’s insights matching new features
Continue testing with data

15/10/2026
This week and last week I focused on building an interactive application with a Gradio interface. I used AI to help structure the interface with my object design, I made sure to critically evaluate the output. I have the full analysis with file upload, data cleaning, spending summaries, savings projections, visualisations. I learned about how Gradios block layout works and how to organise using rows, columns and tabs. I made sure error handling was in place with messages and validations. AI was helpful for drafting and the final implementation requires my own judgement. I want to enhance the interface by making Alfie feel more conversational. This week so far has advanced the useability of the tool and increased my confidence in integrating AI-assisted development with my own coding knowledge and skills.   

16/10/2026
<img width="740" height="273" alt="image" src="https://github.com/user-attachments/assets/9a825507-9130-4fb1-9f31-14f9ad1d911c" />

<img width="415" height="185" alt="image" src="https://github.com/user-attachments/assets/54532f4d-04dc-427b-b908-b5d7270f3273" />

Switched to gemini-3.8-flash still having the 503 error I used Gemini to add a failsafe and other models of the API to reduce error risk, unfortunately after going back and forth it transformed my code into something too large and complicated for me to comprehend with my current coding knowledge and it unfortunately still did not work. It added a duplicated Gradio interface and unorganised blocks of code throughout the textbook that appeared redundant to the project. I rejected the output and reverted back to my original through my code path in the Github repository. 
<img width="800" height="209" alt="image" src="https://github.com/user-attachments/assets/154c14b1-38ef-4745-bebf-4a024c06eef3" />


To ensure accuracy I implemented testing with my pseudocode and requirements I worked with Gemini who helped in targeting accuracy and edge cases.

Calculation Verification 

Verified that Alfie’s data-cleaning and scripts matched manual transaction from the sample_transactions.csv file:

Total spending, category subtotals, top merchant identification, monthly totals breakdown results all as expected.

To prevent from crashing if users upload messy real world data, I simulated five scenarios. Below are the tested conditions.

Edge Case A: Empty Dataframes

Edge Case B: Missing Columns

Edge Case C: Non-Numeric/Corrupted Amounts

Edge Case D: Negative Amounts (Refund Offsets)

Edge Case E: Irregular Date Formats (Bug was caught in testing)
Condition Tested: Mixed chronological formats in a single upload (e.g., combining 03/01/2024, 2024-01-05, and 7-Jan-2024).
Bug/Issue Caught: Standard pd.to_datetime parsers failed or threw out entries when encountering multiple styles.
Solution/Handling: Updated the core cleaning helper to use pd.to_datetime(..., format='mixed', errors='coerce') which parsed all styles into standard timestamp objects, allowing sorting.

With this testing there is now 100% pass across all the verification steps.

16/10 Entry 2

I managed to gain API connection with gemini-3.5-flash.
I enchanced and rewrote code for each section:

*Input and validation* 
I manually added notes to each section, improved readability, and clarified expectations.

*Cleaning data* 
I rewrote the code to handle column name discrepancies and validated that rows still remained after cleaning.
For total spending, I used pandas.sum() to simplify the loop logic.

*Savings goal planner*
I added sentinel loops and Gemini API insights.  

*Alfies personalised insights*
I created the chatbot function so users can ask real questions and receive insightful responses from Alfie based on the uploaded data.

*Gradio interface*
The Gradio interface needed reworking with all the new features added.
It now includes Alfie’s personalised insights chatbot, and testing on PDF and CSV documents worked once the API connection issue was resolved.
The savings tracker feature was included.
The previous versions generated by Gemini were more basic and didn’t encompass all sections, which showed me the importance of checking generated code and tailoring it to my requirements with more thoughtful oversight.

*Testing*
The draft testing section was a good start but didn’t assert the correct tests for the project.
I built on the foundations with more depth and test cases for each possible section.
I AI‑generated the test cases with more thoughtful prompting, including each section of the project and asserting for every scenario.

Overall, across every section today I actively tested, rewrote sections, added notes and improved logic for much better clarity. I added new features where I saw opportunity for improvement. I removed code that was not necessary and repetitive, such as downloading the Gemini API, as it added visual clutter. I made each sections logic build on the previous rather than acting as standalone features. 

I decided not to action the following items brainstormed in previous weeks, as I did not feel they were required.
The project is already advanced and provides a well‑rounded user experience.
Too many features could overcomplicate it and distract from the purpose of the tool:
- Add savings timeline visuals
- Possible integration of a stock portfolio section
  I did, however, action making Alfie more conversational in its personalised insights and chat feature.

# Lessons Learned 
 The biggest lesson I learned was the importance of treating AI as a supporting tool. Even when Gemini generated helpful starting points, the code only became correct, reliable and user friendly once I rewrote sections myself, validated assumptions, and tested every scenario. 
 
 It became essential to understand the logic behind each feature and not take AI output at face value. Building features that work together not in isolation was very important to understand. Earlier versions of the project felt disconnected, once I went through line by line, rewrote code, improved validations, loops, and logic the tool became useful and cohesive. Knowing when not to add a feature was important, for example I was initially adding the chatbot feature in both my saving goal planner and personalised insights. Iterating deliberately and thoughtful design choices helped create better functionality in this project.  
