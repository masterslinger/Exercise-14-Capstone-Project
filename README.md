# Exercise-14-Capstone-Project
# Capstone Project - Personal Finance Categorization and Summary Automation
~~~
Name : M.JOHN PALL
Reg. No : 212224040140 
~~~

## Aim
To automate the process of reading personal transaction data from a CSV file, categorizing expenses into various groups (Food, Transport, Bills, Others), and generating a summary report with total amounts and current date in an Excel file using UiPath.

## Materials Required
UiPath Studio (Community/Enterprise Edition)
Windows OS
Input transaction file (CSV format)
Basic knowledge of UiPath:
Read CSV
For Each Row
If Condition
Dictionary & Variables
Add Data Row
Write CSV

## Procedure

Step 1: Prepare Input File
  Create a CSV file named transactions.csv
  Columns: Date, Description, Amount
  Example:
  ~~~
  2025-05-21, TNEB Online Payment, 600
  2025-05-21, Swiggy Order, 250
  ~~~

Step 2: Build Category Logic
  Read the CSV file using Read CSV → Output: dtTransactions.
  Create a Dictionary variable:
  Name: categoryTotals
  Type: Dictionary<String, Double>
  Default value:
  ~~~
  New Dictionary(Of String, Double) From {
     {"Food", 0},
     {"Transport", 0},
     {"Bills", 0},
     {"Others", 0}
  }
  ~~~
  Loop through each row in dtTransactions with For Each Row.
  
  Inside the loop:
  
  Assign: desc = row("Description").ToString.ToLower
  
  Assign: amount = Convert.ToDouble(row("Amount").ToString)
  
  Use If conditions to match descriptions:
  
  If desc.Contains("swiggy") Or desc.Contains("zomato") Or desc.Contains("food")
      → categoryTotals("Food") += amount
  
  ElseIf desc.Contains("uber") Or desc.Contains("ola") Or desc.Contains("bus") Or desc.Contains("train")
      → categoryTotals("Transport") += amount
  
  ElseIf desc.Contains("tneb") Or desc.Contains("recharge") Or desc.Contains("bill")
      → categoryTotals("Bills") += amount
  
  Else
      → categoryTotals("Others") += amount
  📊 Step 3: Create a Summary Table
  Add Build Data Table activity → Name it dtSummary
  
  Columns: Category (String), Total (Double), Date (String)
  
  Use For Each item In categoryTotals
  
  Add Data Row:
  ~~~
  { item.Key, item.Value, Now.ToString("dd-MM-yyyy") }
  📤 Step 4: Write Output
  Use Write CSV activity
  ~~~

# Sequence :
![Screenshot 2025-05-24 214511](https://github.com/user-attachments/assets/f6805393-1bf2-4969-9b41-8e16190a8f9a)

![Screenshot 2025-05-24 214524](https://github.com/user-attachments/assets/4c081d6a-a646-4be7-a0ec-0b1acd4e5d2c)

![Screenshot 2025-05-24 214531](https://github.com/user-attachments/assets/d8dcdece-f510-4976-88fb-6ad91573dbf7)

![Screenshot 2025-05-24 214540](https://github.com/user-attachments/assets/c5d5acbb-9857-4150-b64b-bb5cbdb9f3ec)

![Screenshot 2025-05-24 214549](https://github.com/user-attachments/assets/c1204893-5e98-4da3-b96c-16d8e8cea658)

![Screenshot 2025-05-24 214600](https://github.com/user-attachments/assets/e123ffb2-caea-4ec5-af27-e55466d01e6b)


# Input:
![Screenshot 2025-05-24 214636](https://github.com/user-attachments/assets/2119e283-bd32-4ef8-bfc7-01e8c3034a12)

# Output :
![Screenshot 2025-05-24 214645](https://github.com/user-attachments/assets/a4f6940b-24ad-4e17-95c6-9799fc3dd69f)


# Result :
The workflow successfully categorizes transaction data based on their description into 4 groups and generates a daily summary in a structured CSV file with date tracking.
