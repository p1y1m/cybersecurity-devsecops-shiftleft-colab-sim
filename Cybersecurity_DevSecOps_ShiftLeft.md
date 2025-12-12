# Cybersecurity, DevSecOps and Shift-Left Security (Colab)

**Author: Pedro Yanez Melendez**

This lab shows how I use Python in Google Colab to practice security analytics, DevSecOps and shift-left security.
I work with synthetic security events and code examples to connect blue team monitoring with secure coding practices.

## 1. Overview

- Use Python, pandas and scikit-learn to build a small security analytics environment.
- Combine red team vs blue team ideas with DevSecOps and shift-left security.
- Show how runtime monitoring, anomaly detection and secure coding fit together.
- Present the results in simple tables that look like a security dashboard.

## 2. Main concepts

- Red team and blue team mindset.
- Brute-force login attacks at the log level.
- SIEM-style log aggregation and correlation.
- Threshold-based detection rules inspired by tools like Fail2ban and WAFs.
- Anomaly detection and UEBA-style analysis with IsolationForest.
- SOC, XDR and SOAR as modern security operation platforms.
- Zero trust ideas for stronger checks on suspicious activity.
- DevSecOps and shift-left security in the development lifecycle.
- Static Application Security Testing (SAST) for source code.
- CI/CD security gates and combined risk scoring per service.

## 3. Tools and platforms referenced

These tools are not installed in the notebook, but I use them as real-world references:

- SIEM and analytics: Splunk, Elastic Security, Microsoft Sentinel, IBM QRadar.
- Endpoint and XDR: Microsoft Defender XDR, CrowdStrike Falcon, Palo Alto Cortex XDR.
- Network and prevention: Fail2ban, WAF appliances (Palo Alto, Fortinet), firewalls.
- DevSecOps and SAST: SonarQube, Checkmarx, Snyk, Bandit, OWASP Dependency-Check.
- CI/CD security: GitHub Actions, GitHub Advanced Security, GitLab CI pipelines.

## 4. Notebook structure

### 4.1 Security event generation

- Create a baseline of normal security events with users, IPs and actions.
- Model red team activity as repeated login failures from one attacker IP.
- Merge both sets into a single security event stream.
- Label events by role (normal activity vs red team) and by behavior (benign vs suspicious).

### 4.2 Blue team detection logic

- Group login failures in 5-minute time buckets, similar to SIEM rules.
- Count failures per IP and time bucket.
- Raise a brute-force alert when counts pass a defined threshold.
- Suggest blue team actions, such as blocking the IP and forcing password resets.

### 4.3 Anomaly detection with IsolationForest

- Aggregate events per IP and time bucket to build feature tables.
- Engineer features such as total events, failures, locked logins and ratios.
- Train an IsolationForest model on these features.
- Score every IP/time bucket and label anomalous behavior.
- Rank the most anomalous buckets for analyst review, similar to XDR or UEBA.

### 4.4 Zero trust and alert console

- Merge anomaly ranks back into the detailed event stream.
- Mark events that belong to the top anomalous buckets.
- Add a zero trust flag for events that need strong verification.
- Build a compact “alert console” table that shows key fields:
  - Timestamp, IP, user, action.
  - Behavior label and blue team recommendation.
  - Zero trust flag and anomaly rank.

### 4.5 Shift-left and secure coding checks

- Define a small repository of service files and infrastructure code.
- Use regular expressions to search for common insecure patterns:
  - Hardcoded passwords and secrets.
  - Plain-text API keys.
  - Weak hashing such as MD5.
  - Wide-open security groups (0.0.0.0/0).
- Treat these checks as a SAST-style scan over the code base.

### 4.6 DevSecOps security gate

- Aggregate SAST findings per service and severity level.
- Apply security gate rules similar to a CI/CD pipeline:
  - Block releases when high-severity issues exist.
  - Warn and require fixes when there are too many medium issues.
  - Pass the gate when thresholds are respected.
- Add a shift-left action that explains what the team should do next.

### 4.7 Unified DevSecOps risk dashboard

- Map IP ranges from runtime events to services.
- Aggregate runtime risk metrics per service:
  - Total events, suspicious events, brute-force alerts, anomaly buckets.
- Merge runtime metrics with code-level findings and gate status.
- Compute a combined risk score per service.
- Recommend next actions for DevSecOps and SOC teams, such as:
  - Prioritize hotfix and block new deployments.
  - Schedule a security sprint and improve monitoring.
  - Keep current controls and review regularly.

## 5. Skills used

- Use Python and pandas to manipulate and analyze security event data.
- Design security features and build anomaly detection with scikit-learn.
- Think like a blue team and a DevSecOps engineer at the same time.
- Translate security concepts into clear, developer-friendly tables.
- Connect runtime monitoring with secure coding and CI/CD controls.
- Communicate complex security ideas in simple and practical language.

## 6. How to run the code

- Open the notebook in Google Colab.
- Run the cells in order from top to bottom.
- Inspect the DataFrames to see how detection and scoring evolve.
- Adjust thresholds and parameters to explore different security behaviors.

## 7. Possible extensions

- Add more attack patterns, such as password spraying or suspicious file access.
- Include extra features and models, like sequence-based analysis of events.
- Enrich the SAST rules with more patterns from secure coding guides.
- Simulate a simple CI/CD pipeline flow inside the notebook.
- Export selected tables as images for use in presentations or reports.
