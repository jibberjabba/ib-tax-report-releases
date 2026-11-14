# Setting up the IB Flex Query

IB Tax Report reads an **Activity Flex Query** that you export from Interactive
Brokers as XML. Create the query once per client login; after that it's just
"Run → download" each financial year.

> The app checks every file before it builds anything. If a section or level
> of detail below is missing, it stops and names the exact checkbox to tick,
> so you won't get a workbook with figures quietly missing.

## 1. Create the query

1. Log in to **IB Client Portal** (as the client, or with your advisor login).
2. Go to **Performance & Reports → Flex Queries**.
3. Next to **Activity Flex Query**, click **+** (Create).
4. Give it a name, e.g. `Tax Report FY`.

## 2. Tick these sections

For each section, click it, tick the **levels of detail** shown, and choose
**Select All** for the fields. Selecting all fields is simplest; the app
ignores anything it doesn't need.

| Section | Levels of detail to tick | Used for |
|---|---|---|
| **Account Information** | (no options) | Account number, name, base currency, and entity type (Personal / SMSF / Trust / Company) |
| **Trades** | **Execution** *and* **Closed Lots** | Execution = brokerage commissions. Closed Lots = cost base, proceeds and gains for each CGT event |
| **Cash Transactions** | **Detail** | Dividends, withholding tax, interest, fees, deposits and withdrawals |
| **Open Positions** | **Lot** | Holdings at year end, with each lot's open date (used for the buy-date FX rate) |
| **Forex P/L Details** | (all) | AUD/USD currency conversions and realised FX gain/loss |
| **Transfers** | (all) | Movements between the client's own IB accounts (for reconciliation) |
| **Sales Tax Details** *(optional)* | (all) | GST charged by IB on fees. Only Australian-domiciled accounts have this |

Other sections (Cash Report, Change in Dividend Accruals, etc.) are harmless
if ticked; they're ignored.

> **Open Positions:** tick **Lot**. If you also tick **Summary**, that's
> fine: the app uses the Lot rows and ignores the Summary rows, so holdings
> aren't counted twice.

## 3. Delivery configuration

| Setting | Value |
|---|---|
| **Format** | **XML** |
| **Period** | **Custom Date Range**: 1 July to 30 June of the financial year |
| **Date Format** | **`yyyyMMdd`** (IB's default; the app can't read other date formats) |
| **Time Format** | `HHmmss` (default) |
| **Date/Time Separator** | `;` (semi-colon, default) |
| Include Canceled Trades | No |
| Include Currency Rates | optional (the app uses RBA rates, not IB's) |

Under **Accounts**, tick every account to include. **Accounts in the same
XML file are combined** into an extra "ALL" rollup workbook. So:

- put a client's **personal** accounts in one query, and
- run their **SMSF** (or trust/company) accounts as a **separate** query/file
  if you don't want them rolled up together.

Click **Continue → Create**.

## 4. Run and download

1. Back on the Flex Queries page, click **Run** (▶) next to the query.
2. Choose **XML** and download the file.
3. Put the XML file(s) for one client in their own folder. The workbooks
   are written into the same folder.

## 5. Things to check

- **The date range must cover the whole financial year.** The workbooks are
  named from the statement's end date (`FY2026` = year ending 30 June 2026).
- **Shares bought before the financial year are fine.** The app downloads
  RBA rates back to each lot's purchase date automatically.
- **Accounts in different base currencies are fine.** USD-base and AUD-base
  accounts are both supported, in the same file or in separate files.

<!-- TODO: add screenshots of the section checkboxes and delivery settings -->
