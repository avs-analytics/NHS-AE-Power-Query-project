# NHS Emergency Care Activity Dashboard

**Excel | Power Query | PivotTables | PivotCharts**

## What is this project?

This project explores Type 1 and Type 2 Emergency Care activity across NHS England.

I built an interactive Excel dashboard to look at three main aspects of emergency care activity:

- how the number of attendances changes over time and differs between NHS regions;
- how admission rates vary between regions;
- whether particular complaint categories are more or less represented among admitted patients than in the overall patient population.

The aim was not simply to create a dashboard, but to build a **repeatable reporting workflow** that could handle new monthly data without manually rebuilding the analysis.

---

## The dashboard



The final dashboard brings the main findings together in one view.

It allows the user to filter the analysis by:

- NHS Region
- Integrated Care Board (ICB)
- Year
- Quarter
- Month

The main visuals show:

- total patient attendances by NHS region over time;
- admitted and non-admitted patients together with the admission rate;
- complaint profiles among all patients compared with admitted patients;
- the difference in complaint representation between admitted patients and the overall patient population.

---

## How I built it

The source data was provided as **monthly files**. Rather than manually combining the files, I built a folder-based Power Query workflow.

The process is:

**Monthly source files → Power Query → cleaned and reshaped dataset → PivotTables → PivotCharts → Dashboard**

Power Query handles the preparation of the data, including:

- combining the monthly files;
- cleaning and restructuring the source format;
- promoting, transposing and unpivoting data where required;
- splitting fields into analytical attributes;
- converting data types;
- creating reporting dates;
- reshaping the measures into an analysis-ready format;
- creating the calculated field for admission representation difference.

The intention was to make the workflow **scalable**: when a new monthly file is added to the source folder, the workbook can be refreshed instead of manually rebuilding the dataset.

---

## Analysis

I used **PivotTables and PivotCharts** as the analytical layer between the transformed data and the dashboard.

Some of the key calculations are:

- Total attendances
- Admitted attendances
- Admission rate
- Share of total patients by complaint category
- Share of admitted patients by complaint category
- Difference in complaint representation between admitted patients and all patients

One of the main analytical measures is the **admission representation difference**:

> Share of a complaint category among admitted patients  
> minus  
> share of the same complaint category among all patients

This helps highlight complaint categories that are disproportionately represented among admitted patients.

---

## Testing the workflow

I wanted to make sure that the workflow was genuinely scalable rather than simply looking scalable.

As a test, I removed one monthly source file from the folder and refreshed the workbook.

The Power Query pipeline successfully updated the dataset and PivotTables without manually appending or rebuilding the data.

The test also highlighted two chart-formatting issues that can occur after a refresh. These are documented below as known limitations.

---

## Known limitations

### 1. Data suppression

The source data contains suppressed counts between 1 and 7, represented by `*`.

These values cannot be treated as zero because the actual value is unknown. In the current version, suppressed values are therefore treated as missing and excluded from the relevant calculations.

The number of affected records is very small, so I consider this unlikely to materially affect the high-level patterns shown in the dashboard.

### Planned improvement: 

The next version will retain the suppression status throughout the Power Query transformation and explicitly identify analytical records affected by suppressed values.

### 2. Chart formatting after refresh

The data and calculations update successfully when the workbook is refreshed, but two chart-formatting settings are not currently preserved reliably:

- In the **Admitted and Not-Admitted Patients vs Admission Rate** chart, the Admission Rate series can move from the secondary axis to the primary axis. As a result, the admission-rate line can become difficult to interpret or disappear from view.

- In the **Complaint Representation Difference** chart, the **Invert if negative** formatting setting can be reset. Negative values therefore lose their intended red formatting and may appear in the same colour as positive values.

These are **presentation and formatting limitations rather than problems with the underlying data or calculations**.

### Planned improvement

The chart configuration will be redesigned so that the secondary axis and positive/negative formatting are preserved more reliably after a data refresh.

---

## Tools used

- **Microsoft Excel**
- **Power Query**
- **PivotTables**
- **PivotCharts**
- **Excel formulas**

---

## What this project demonstrates

This project demonstrates my ability to:

- work with multiple monthly source files;
- build a repeatable data-cleaning workflow in Power Query;
- reshape data for analysis;
- create calculated analytical measures;
- use PivotTables and PivotCharts for analysis;
- design an interactive Excel dashboard;
- test a data-refresh workflow for scalability;
- identify and document data-quality and presentation limitations.

