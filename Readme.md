# Can I Buy It?

An Excel-based affordability calculator that helps users decide whether they can safely purchase an item without using money reserved for essential expenses.

## What it does

The workbook answers three questions:

1. **Am I currently in my financial safe zone?**
2. **If not, when will I enter the safe zone?**
3. **When can I safely buy a particular item?**

It follows a cash-only approach. It does not recommend loans, EMI, credit, or Buy Now Pay Later.

## How the safe zone works

The user chooses how many months of essential commitments they want to keep as a safety buffer.

```text
Monthly commitments = Loan payments
                    + Investments marked as untouchable
                    + Transport
                    + Other essential expenses

Safety-buffer target = Monthly commitments × Buffer months
```

For example, choosing a buffer value of `6` means the workbook protects six months of essential commitments.

The buffer is customizable. Values such as `0.5`, `1`, `3`, `6`, or `12` can be used.

## Main calculations

### Monthly surplus

```text
Monthly surplus = Monthly income − Monthly commitments
```

This is the amount assumed to be available for building the safety buffer and saving for purchases.

### Money needed to enter the safe zone

```text
Safe-zone shortage = MAX(
    0,
    Safety-buffer target
    + Upcoming unavoidable expenses
    − Current balance
)
```

### Time needed to enter the safe zone

```text
Months until safe zone = ROUNDUP(
    Safe-zone shortage ÷ Monthly surplus
)
```

The workbook uses the selected salary day to estimate the date on which the user will enter the safe zone.

### Purchase affordability

A purchase is considered safe only when the user can pay for the item and still retain the complete safety buffer.

```text
Total cash required = Safety-buffer target
                    + Upcoming unavoidable expenses
                    + Item price

Money still needed = MAX(
    0,
    Total cash required − Current balance
)

Months until purchase = ROUNDUP(
    Money still needed ÷ Monthly surplus
)
```

The workbook then estimates the earliest salary date when the purchase becomes safe.

## Workbook sheets

### Quick Check

Checks the affordability of one item.

The user enters:

- Item name
- Category
- Item price
- Priority

The sheet displays:

- Current safe-zone status
- Safety-buffer target
- Money needed to enter the safe zone
- Estimated safe-zone date
- Safe spending money currently available
- Total money needed for the buffer and item
- Months of saving required
- Earliest safe purchase date
- Final purchase decision

### My Budget

Contains the financial information used by all calculations.

Editable fields include:

- Current balance
- Monthly income
- Salary day
- Monthly loan payments
- Monthly investments that should not be paused
- Transport expenses
- Other essential expenses
- Upcoming unavoidable expenses
- Desired safety-buffer months

Yellow cells are intended for user input. Calculated cells update automatically.

### Compare Items

Allows multiple products to be compared using the same financial information.

The user enters only:

- Item name
- Item price

For each item, the sheet calculates:

- Total cash required
- Money still needed
- Months to wait
- Earliest safe purchase date
- Final result

### How It Works

Provides short instructions inside the workbook.

## Result meanings

- **IN SAFE ZONE** — The current balance covers the complete selected safety buffer.
- **NEED MORE** — The current balance is below the safety-buffer target.
- **BUY NOW** — The item can be purchased while keeping the safety buffer intact.
- **WAIT UNTIL** — The item is not currently safe to buy; an estimated safe date is provided.
- **NOT AFFORDABLE** — Monthly commitments are equal to or greater than monthly income, leaving no positive monthly surplus.

## How to use

1. Open **My Budget**.
2. Update all yellow cells with current financial information.
3. Choose the desired number of safety-buffer months.
4. Check the safe-zone status and estimated safe-zone date.
5. Open **Quick Check** and enter an item and its complete price.
6. Use **Compare Items** when comparing multiple possible purchases.
7. Update the current balance whenever money is received or spent.

## Assumptions

- Income is received regularly on the selected salary day.
- Monthly commitments remain reasonably stable.
- The calculated monthly surplus is saved.
- Unexpected expenses are entered manually.
- No interest, investment returns, inflation, or price changes are included.
- Estimated dates change when the balance, income, expenses, or buffer preference changes.

## Privacy

The workbook works locally. It does not connect to bank accounts and does not require login credentials. Financial information is stored only inside the Excel file.

## Disclaimer

This workbook is a personal budgeting tool and not professional financial advice. Its results depend on the accuracy of the information entered by the user.
