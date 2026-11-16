# Installing and running IB Tax Report

Download the latest version from the
[Releases page](https://github.com/jibberjabba/ib-tax-report-releases/releases/latest).
You don't need to install Python.

| Computer | Download | Works on |
|---|---|---|
| Mac | `IB-Tax-Report-…-mac.dmg` | macOS 10.13 High Sierra or later, Intel or Apple Silicon |
| Windows PC | `IB-Tax-Report-…-windows.zip` | Windows 10 or 11, 64-bit |
| Either | `IB-Tax-Report-…-sample-data.zip` | Made-up sample files to try the app with (optional) |

## Mac

1. Open the `.dmg` file.
2. Drag **IB Tax Report** onto the **Applications** folder shortcut.
3. Open **IB Tax Report** from Applications (or Launchpad).

The Mac app is signed and notarised by Apple, so it opens without a security
warning.

<details>
<summary>If macOS says the app "can't be opened" (unsigned pre-release builds only)</summary>

- **macOS 10.13 to 14:** right-click (or Control-click) the app → **Open** → **Open**.
- **macOS 15 and later:** try to open it once. Then go to **System Settings →
  Privacy & Security**, scroll down, and click **Open Anyway** next to the
  IB Tax Report message.

You only need to do this the first time.
</details>

## Windows

1. Right-click the `.zip` file → **Extract All…** → choose a location (for
   example `Documents`) → **Extract**.
2. Open the extracted **IB Tax Report** folder and double-click
   **IB Tax Report.exe**.
   - Keep the `.exe` inside its folder. It needs the `_internal` folder
     next to it.
   - To make a desktop shortcut: right-click the `.exe` → **Send to → Desktop
     (create shortcut)**.
3. The first time, Windows may show **"Windows protected your PC"** (the
   Windows build isn't code-signed yet). Click **More info → Run anyway**.

## Try it with the sample files first

Before setting up a Flex Query for a client, check the app works on your
computer with the sample files. They're made-up Flex Query statements: every
name, account number and figure in them is fictional.

1. Download `IB-Tax-Report-…-sample-data.zip` from the
   [Releases page](https://github.com/jibberjabba/ib-tax-report-releases/releases/latest).
2. Extract it. On Windows, right-click → **Extract All…** → **Extract**; on a
   Mac, double-click it. Don't open the files from inside the zip: the app
   saves its workbooks next to the XML files, and it can't write into a zip.
3. Open **IB Tax Report** and choose the extracted
   **IB Tax Report Sample Data** folder.
4. You should get **13 workbooks**. If you do, the app works. Open a few of
   them to see how each kind of entry is reported.

The folder has five files, one per kind of client:

| File | What it shows |
|---|---|
| `Test_Personal_Multi_Tax_Assessment.xml` | Two individual accounts, plus a combined `ALL` workbook |
| `Test_SMSF_Tax_Assessment.xml` | One self-managed super fund (CGT discount 1/3) |
| `Test_Trust_Multi_Tax_Assessment.xml` | Two family trusts, plus a combined workbook; includes GST on fees |
| `Test_Company_Multi_Tax_Assessment.xml` | Two companies, plus a combined workbook (no CGT discount) |
| `Test_Mixed_Entity_Tax_Assessment.xml` | An individual and a trust in one file (combined workbook named `Mixed_ALL`) |

`READ ME FIRST.txt` in the folder has the same steps. Keep real client files
in their own folder, not in the sample folder.

## Using it

1. Put the client's IB Flex Query XML file(s) in a folder. See the
   [Flex Query setup guide](flex-query-setup.md).
2. Open **IB Tax Report**. A folder picker appears. Choose that folder.
3. Wait a few seconds (longer the first time, while it downloads RBA rates).
   A message lists the workbooks it created, and the folder opens.

The workbooks (`IB_Tax_…_FY2026.xlsx`) are saved **in the same folder** as the
XML files, along with `rba_fx_rates.csv`, a cache of RBA exchange rates.

### Internet access

- **First run for a folder:** needs internet to download RBA daily exchange rates.
- **Later runs:** work offline if the cached rates already cover the dates
  needed. Copying `rba_fx_rates.csv` into a new client folder also lets that
  folder run offline.

### If something goes wrong

| Message | What to do |
|---|---|
| *The Flex Query is missing data this report needs* | Tick the listed section or level of detail in the Flex Query, run it again, and download a fresh XML. See the [setup guide](flex-query-setup.md). |
| *uses a date format this report can't read* | In the Flex Query's Delivery Configuration, set Date Format to `yyyyMMdd`. |
| *No Flex Query XML files (.xml) found* | You picked the wrong folder, or the file was saved as CSV. Re-download it as XML. |
| *Could not download RBA exchange rates* | Check the internet connection (some office networks block downloads), or copy an `rba_fx_rates.csv` from another folder. |
| *Something went wrong while building the workbooks* | A file called `ib_tax_report_error.log` was saved in the folder. Please send it with a description of the problem. It contains the program's progress messages (including account numbers) and error details, but no transaction figures. |

*IB Tax Report prepares figures for review. It isn't tax advice. Review all
figures before lodgement.*
