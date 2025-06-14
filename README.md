# 🌤️ Weather Forecast Logger and Accuracy Analyzer

This project is a real-world Bash scripting application that automates the collection of daily weather data for **Casablanca**, logs it, and calculates the accuracy of forecasted temperatures compared to observed values. It includes tools to assess forecast precision over time and generate weekly statistics.

---

## 📁 Project Structure

| File                          | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| `rx_poc.sh`                  | ETL script: fetches weather data using `curl`, extracts observed & forecasted temps, and logs to `rx_poc.log`. |
| `fc_accuracy.sh`             | Compares today's forecasted and observed temperatures, labels accuracy, and appends results to `historical_fc_accuracy.tsv`. |
| `weekly_stats.sh` (optional) | Analyzes the past 7 days of forecast accuracy and reports min/max absolute errors. |
| `rx_poc.log`                 | Daily weather log with date, observed temp, and forecasted temp. |
| `historical_fc_accuracy.tsv`| Tab-delimited report of forecast accuracy per day with accuracy labels. |

---

## 🛠️ How It Works

### 1. **Weather Data Extraction**
- Uses [`wttr.in`](https://wttr.in) to fetch raw weather data.
- Extracts observed and forecasted temperatures.
- Stores daily results in a tab-delimited log file.

### 2. **Forecast Accuracy Calculation**
- Compares forecasted temp from yesterday with today’s actual observed temp.
- Computes accuracy (forecast - actual).
- Labels accuracy:
  - `excellent`: ±1°C
  - `good`: ±2°C
  - `fair`: ±3°C
  - `poor`: >±3°C

### 3. **Weekly Stats**
- Calculates minimum and maximum absolute forecast error over the past 7 days.

---

## 🧪 Example

`rx_poc.log`:
```

2025	06	14	27°C	30°C

```

`historical_fc_accuracy.tsv`:
```

year	month	day	obs\_temp	fc\_temp	accuracy	accuracy\_range
2025	06	14	27°C	30°C	3	fair

````

---

## ⏰ Automation

- `rx_poc.sh` is scheduled via `cron` to run every day at **7:00 AM local time**, which matches **12:00 PM Casablanca time** (UTC+1 during DST).
- The script appends new weather data daily without overwriting logs.

---

## ▶️ How to Run

```bash
./rx_poc.sh          # Fetch today's weather and log it
./fc_accuracy.sh     # Calculate and label forecast accuracy
./weekly_stats.sh    # Show weekly error stats (optional)
````

---

## 🔧 Requirements

* Bash 4+
* `curl`
* UNIX tools: `grep`, `cut`, `tr`, `date`

---

## 📈 Learning Outcomes

Through this project, you will:

* Practice real-world ETL using Bash scripting
* Schedule jobs with `cron`
* Use command-line data extraction (e.g., `grep`, `cut`)
* Perform basic error analysis and conditional logic in Bash
* Learn how to push code to GitHub and manage scripts as projects
