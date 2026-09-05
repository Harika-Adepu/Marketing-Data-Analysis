# Assignment B — Healthcare Marketing Data Analysis

This project analyzes healthcare marketing outreach data to physicians and calculates key marketing metrics such as **Reach, Frequency, and Engagement**.

The analysis evaluates these metrics overall and across:

* Communication Source
* Channel
* Month

The objective is to identify meaningful patterns, compare marketing performance across segments, and provide data-driven recommendations for improving physician engagement.

---

## 🎯 Objective

The analysis focuses on:

* Understanding the marketing outreach dataset
* Performing data quality checks
* Handling duplicate records
* Processing dates
* Understanding marketing activity types
* Calculating Reach
* Calculating Frequency
* Calculating Engagement
* Segmenting results by source, channel, and month
* Creating visualizations
* Identifying trends and patterns
* Providing data-driven recommendations

---

## 📂 Dataset

The dataset is:

```text
Marketing Data - Hiring.xlsx
```

The original dataset contains **100,040 rows and 9 columns**.

The main fields are:

| Column                    | Description                          |
| ------------------------- | ------------------------------------ |
| Communication Source      | Source/system used for communication |
| Source Channel Name       | Communication channel                |
| Therapeutic Area          | Medical/therapeutic area             |
| Device                    | Device category                      |
| Source Device Name        | Specific device/source device        |
| Activity                  | Marketing activity type              |
| Count of Activity Metrics | Activity count where available       |
| Activity Date             | Date of the marketing activity       |
| Physician ID              | Identifier for the physician         |

---

## 🔄 Analysis Pipeline

```text
Marketing Dataset
       ↓
Data Inspection
       ↓
Missing Value Analysis
       ↓
Duplicate Detection
       ↓
Duplicate Removal
       ↓
Date Processing
       ↓
Activity Analysis
       ↓
Metric Calculation
       ↓
┌──────────────┬──────────────┬──────────────┐
│    Reach     │  Frequency   │  Engagement  │
└──────────────┴──────────────┴──────────────┘
       ↓
Segmentation
       ↓
Source / Channel / Month
       ↓
Comparison & Visualization
       ↓
Insights
       ↓
Recommendations
```

---

## 🧹 Data Cleaning

### Column Names

Column names were standardized by:

* Removing leading/trailing spaces
* Replacing spaces with underscores

For example:

```text
Communication Source
```

became:

```text
Communication_Source
```

---

## 🔍 Duplicate Handling

The raw dataset contained:

```text
100,040 rows
```

A total of:

```text
4,275 exact duplicate rows
```

were identified.

These duplicates were removed because duplicate activity records could artificially inflate marketing activity and engagement metrics.

After duplicate removal:

```text
95,765 rows
```

remained for analysis.

---

## 📅 Date Processing

The `Activity_Date` column was converted into a proper datetime format.

A new:

```text
Month
```

field was created using the activity date.

This allowed monthly analysis of marketing performance.

---

## 📊 Activity Types

The dataset contains activities such as:

* Sent
* Delivered
* Open
* Click
* Bounce
* Hard Bounce
* Unsubscribe

These activity types were interpreted according to their role in the marketing journey.

---

# 📈 Marketing Metrics

## 1. Reach

### Definition

Reach represents the number of unique physicians represented in the marketing activity data.

### Formula

```text
Reach = Number of unique Physician IDs
```

Overall Reach:

```text
25,208 physicians
```

---

## 2. Frequency

### Definition

Frequency measures the average number of outbound contact events per reached physician.

### Formula

```text
Frequency =
Total outbound contact events
/
Unique physicians reached
```

Overall Frequency:

```text
2.95
```

This means that, on average, each reached physician had approximately 2.95 outbound contact events under the defined methodology.

---

## 3. Engagement

Engagement represents physician interaction with marketing communications.

The analysis considers:

### Positive Engagement

```text
Open
Click
```

### Negative Engagement

```text
Unsubscribe
```

### Total Engagement

```text
Open + Click + Unsubscribe
```

Overall results:

| Metric              |  Value |
| ------------------- | -----: |
| Reach               | 25,208 |
| Contact Events      | 74,448 |
| Frequency           |   2.95 |
| Positive Engagement | 16,777 |
| Negative Engagement |     61 |
| Total Engagement    | 16,838 |

---

## 🧠 Activity Mapping Methodology

Different communication sources use different activity labels.

Therefore, the analysis uses a source-aware approach.

### Outbound Contact

* `Sent` → one contact event
* `Delivered` → one contact event when a source does not separately record `Sent`

### Engagement

* `Open` → positive engagement
* `Click` → positive engagement
* `Unsubscribe` → negative engagement

### Delivery Failures

* `Bounce` → delivery failure
* `Hard Bounce` → delivery failure

Bounce and Hard Bounce are not treated as physician engagement.

Where `Count_of_Activity_Metrics` is missing for event-level records, the recorded row itself is treated as one activity event.

This approach avoids incorrectly assigning zero contact frequency to sources that use `Delivered` instead of `Sent`.

---

# 📊 Segmentation

The marketing metrics were analyzed across three dimensions.

## 1. Communication Source

The sources include:

* Internal CRM Tool
* Medspace360
* Oncopulse
* Remission Report
* Sales Reps

This allows comparison of performance across different communication sources.

---

## 2. Communication Channel

The channels include:

* Email
* Email Alert
* SMS

The analysis compares Reach, Frequency and Engagement across these channels.

---

## 3. Month

The activity date was converted into a monthly field to identify changes and trends over time.

The analyzed period includes:

* January 2024
* February 2024
* March 2024

---

# 📊 Key Findings

### Communication Source

**Internal CRM Tool**

* Highest total engagement
* Highest frequency

**Remission Report**

* Highest engagement efficiency when measured relative to reach

Therefore, total engagement and engagement efficiency should be considered separately.

---

### Communication Channel

**Email**

* Highest reach
* Highest total engagement

**SMS**

* Lower overall reach
* Strong engagement efficiency relative to its reach

This suggests that high-volume channels and high-efficiency channels may serve different purposes.

---

### Monthly Trends

**January 2024**

* Highest reach
* Highest total engagement

**March 2024**

* Highest frequency

**February 2024**

* Lower engagement compared with January and March

These differences indicate that campaign scale and contact intensity varied across months.

---

# 📈 Visualizations

The analysis includes visualizations for:

* Reach by Communication Source
* Engagement by Communication Source
* Engagement Efficiency by Communication Source
* Reach by Channel
* Engagement by Channel
* Monthly Engagement Trend
* Monthly Reach Trend

These visualizations make segment-level comparisons and monthly trends easier to interpret.

---

# 💡 Recommendations

Based on the analysis:

### 1. Maintain high-reach channels

Email provides broad physician reach and high total engagement, so it can continue to serve as a major communication channel.

### 2. Test and selectively scale efficient channels

SMS shows strong engagement efficiency despite having lower reach. It can be tested for targeted physician segments rather than replacing high-reach channels entirely.

### 3. Monitor communication frequency

High frequency should not automatically be considered better. Excessive contact can lead to communication fatigue.

Frequency should therefore be evaluated together with engagement and negative signals such as unsubscribes.

### 4. Compare scale and efficiency separately

A source with the highest total engagement is not necessarily the most efficient source.

Both:

```text
Total Engagement
```

and:

```text
Engagement per Reached Physician
```

should be considered when evaluating campaign performance.

### 5. Use monthly trends for campaign planning

Monthly differences in reach, frequency and engagement can help identify periods of stronger performance and guide future campaign planning.

---

## 🛠️ Technologies Used

* Python
* Pandas
* NumPy
* Matplotlib
* Jupyter Notebook / Google Colab
* Excel

---

## 📁 Project Structure

```text
Assignment-B/
│
├── Assignment_B.ipynb
├── Marketing Data - Hiring.xlsx
├── Marketing_Analysis_[your_id].xlsx
├── Report / Presentation
└── README.md
```

---

## 📌 Important Assumptions

* Reach is measured using unique `Physician_ID` values.
* Frequency is based on outbound contact events.
* `Sent` is treated as a contact event.
* `Delivered` is treated as a contact event when a source does not separately record `Sent`.
* `Open` and `Click` are treated as positive engagement.
* `Unsubscribe` is treated as a negative engagement signal.
* `Bounce` and `Hard Bounce` are treated as delivery failures.
* Missing activity-count values on event-level records are represented by the recorded activity row itself.
* Exact duplicate records were removed before calculating metrics.

---

## 💡 Key Learning Outcomes

This project demonstrates:

* Data cleaning
* Data quality analysis
* Duplicate handling
* Date/time processing
* Business metric definition
* Marketing analytics
* Segmentation
* Comparative analysis
* Data visualization
* Business insight generation
* Data-driven recommendation development
