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
