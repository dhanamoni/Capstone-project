# Capstone-project
## AIM:
To automate the process of reading personal transaction data from a CSV file, categorizing expenses into various groups (Food, Transport, Bills, Others), and generating a summary report with total amounts and current date in an Excel file using UiPath.

## ALGORITHM:
~~~
Step 1: Prepare Input File Create a CSV file named transactions.csv Columns: Date, Description, Amount Example:

2025-05-21, TNEB Online Payment, 600
2025-05-21, Swiggy Order, 250
Step 2: Build Category Logic Read the CSV file using Read CSV → Output: dtTransactions. Create a Dictionary variable: Name: categoryTotals Type: Dictionary<String, Double> Default value:

New Dictionary(Of String, Double) From {
   {"Food", 0},
   {"Transport", 0},
   {"Bills", 0},
   {"Others", 0}
}
Loop through each row in dtTransactions with For Each Row.

Inside the loop:

Assign: desc = row("Description").ToString.ToLower

Assign: amount = Convert.ToDouble(row("Amount").ToString)

Use If conditions to match descriptions:

If desc.Contains("swiggy") Or desc.Contains("zomato") Or desc.Contains("food") → categoryTotals("Food") += amount

ElseIf desc.Contains("uber") Or desc.Contains("ola") Or desc.Contains("bus") Or desc.Contains("train") → categoryTotals("Transport") += amount

ElseIf desc.Contains("tneb") Or desc.Contains("recharge") Or desc.Contains("bill") → categoryTotals("Bills") += amount

Else → categoryTotals("Others") += amount 📊 Step 3: Create a Summary Table Add Build Data Table activity → Name it dtSummary

Columns: Category (String), Total (Double), Date (String)

Use For Each item In categoryTotals

Add Data Row:

{ item.Key, item.Value, Now.ToString("dd-MM-yyyy") }
📤 Step 4: Write Output
Use Write CSV activity
~~~
## PROGRAM:
![image](https://github.com/user-attachments/assets/1d16b2bd-193a-4a82-ad1e-474a330a8350)
![image](https://github.com/user-attachments/assets/4c3addd4-baac-4650-b300-5a5e3ee9d755)
![image](https://github.com/user-attachments/assets/1ac922ff-b362-497c-bf2c-760656626831)
![image](https://github.com/user-attachments/assets/fba10d4d-05ba-4a2b-b04d-b77752d99c5c)
![image](https://github.com/user-attachments/assets/0044fd3e-48ec-40a9-b020-8d1fd6fcb3a9)
![image](https://github.com/user-attachments/assets/b881147c-83b4-48bc-bc94-520fb95d4407)

## OUTPUT:
![image](https://github.com/user-attachments/assets/bfd3307f-c10f-4a1a-9950-a5d8790d588f)

## RESULT:
The workflow successfully categorizes transaction data based on their description into 4 groups and generates a daily summary in a structured CSV file with date tracking.
