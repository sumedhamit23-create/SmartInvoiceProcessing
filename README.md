# SmartInvoiceProcessing

A UiPath automation that reads invoice data from Excel, checks each invoice, and saves passing invoices and exceptions in one results workbook.

## Invoice checks

- Vendor name must be filled in.
- Amount must be a number greater than zero.
- Invoice date must be filled in.
- Repeated invoice IDs are flagged after their first occurrence. Comparison ignores capitalization and surrounding spaces.

The workflow records all failed checks for each invoice. An invoice with multiple issues appears once in the Exceptions sheet with its reasons combined.

## Workflow

1. Read the Invoices sheet from Input_Invoices.xlsx.
2. Check each row for missing vendor, invalid amount, missing date, and duplicate ID.
3. Combine the reasons for that row.
4. Add passing rows to the valid-invoices table and failed rows to the exceptions table.
5. Write both tables to Invoice_Results.xlsx.

## Files

| File | Purpose |
| --- | --- |
| Main.xaml | Main UiPath workflow |
| project.json | Project configuration and dependencies |
| Input_Invoices.xlsx | Example invoice input |
| Invoice_Results.xlsx | Example output with Valid Invoices and Exceptions sheets |

## Requirements

- Windows with UiPath Studio and Microsoft Excel.
- A UiPath environment supporting the project's .NET 10 target.
- UiPath.Excel.Activities 3.6.0-preview and UiPath.System.Activities 26.10.0, as specified in project.json.

## Run the project

1. Download or clone this repository.
2. Open project.json in UiPath Studio and restore the listed dependencies.
3. Keep Input_Invoices.xlsx in the project folder. Its Invoices sheet must contain InvoiceID, Vendor, InvoiceDate, and Amount columns.
4. Close Invoice_Results.xlsx if it is open in Excel.
5. Run Main.xaml.
6. Open Invoice_Results.xlsx from the project folder to review the Valid Invoices and Exceptions sheets.

## Verified example results

| Result | Invoice count |
| --- | --- |
| Input | 51 |
| Valid invoices | 40 |
| Exceptions | 11 |

All output rows and recorded exception reasons were compared with the example input. These counts describe that dataset.

## Scope

The date check detects missing values. Date format and calendar validity checks can be added in a future version. Invoice IDs are expected to be populated, and duplicate detection applies across the whole input sheet.

## Skills practiced

Excel automation, DataTables, row iteration, If activities, Assign activities, numeric parsing, duplicate detection with a HashSet, and exception reporting.
