# 🕵️ LogSleuth: Named Entity Recognition for Cybersecurity Logs

LogSleuth uses spaCy to pull useful intelligence out of raw security logs. It combines spaCy's pretrained NER, regex-based IP extraction, and custom rule-based threat patterns to turn messy log lines into structured, reportable data.

## What's Covered

- **Sample log dataset**: 10 synthetic security events (failed logins, malware, DDoS, phishing, ransomware, SQL injection, and more)
- **Standard NER**: organizations, products, dates and times with `en_core_web_sm`
- **Regex IP extraction**: spaCy doesn't recognize IPs reliably, so regex fills the gap
- **IP classification**: private (Class A/B/C), loopback, link-local, and public addresses
- **Custom threat detection**: spaCy `Matcher` patterns for `MALWARE`, `ATTACK`, and `NETWORK_COMPONENT`
- **Combined results**: standard and custom entities merged into one summary
- **Visualization**: displaCy HTML entity highlighting and entity count charts
- **Security report**: auto-generated text report with threat counts, organizations, and recommendations
- **CSV export**: entities, IPs, and threats ready for further analysis

## Tech Stack

Python, spaCy, pandas, Matplotlib, Seaborn, regex

## Setup

```bash
git clone https://github.com/<your-username>/LogSleuth.git
cd LogSleuth
pip install spacy pandas matplotlib seaborn
python -m spacy download en_core_web_sm
```

## Usage

Run the script or notebook top to bottom. It prints results at each step and writes the output files below.

```python
import spacy
from spacy.matcher import Matcher

nlp = spacy.load("en_core_web_sm")
matcher = Matcher(nlp.vocab)
matcher.add("ATTACK", [[{"LOWER": "sql"}, {"LOWER": "injection"}]])

doc = nlp("SQL injection attempt detected on web application")
matcher(doc)
```

## Output Files

| File | Description |
|---|---|
| `entities_visualization.html` | displaCy NER highlights for sample logs |
| `security_analysis_report.txt` | Summary report with recommendations |
| `standard_entities.csv` | Entities found by spaCy NER |
| `ip_addresses.csv` | IPs extracted with regex |
| `custom_threats.csv` | Matches from custom threat patterns |

## Key Takeaways

- Pretrained NER models aren't built for security logs, so they miss IPs and threat terms
- Regex and rule-based matching complement statistical NER well
- Structured output makes logs easy to filter, count, and report on
- The logs are synthetic, so this shows the workflow, not production detection

## Next Steps

- Train a custom spaCy NER model on labeled security logs
- Add detection for hashes, CVE IDs, URLs, and domains
- Feed results into a SIEM or dashboard
- Connect to real log sources such as AWS CloudWatch or CloudTrail

## Author

**Farhad Ali Zahid**
AI Operations student | Linux, AWS, Cloud, DevOps

[LinkedIn](https://www.linkedin.com/in/farhad-ali-zahid-99a846446)
