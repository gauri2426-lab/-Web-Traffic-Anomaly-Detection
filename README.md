# 🔍 Web Traffic Anomaly Detection Using CloudWatch Logs

## 📌 Objective

To detect and analyze patterns in web interactions captured from AWS CloudWatch logs in order to identify suspicious or potentially harmful activities.

---

## 📁 Dataset Overview

This dataset contains web traffic records from a production web server. Logs were collected via AWS CloudWatch and flagged using rule-based detection mechanisms.

**Key Columns:**

* `bytes_in`, `bytes_out`: Network traffic volume.
* `src_ip`, `src_ip_country_code`: Source IP and geographic origin.
* `protocol`, `response.code`, `dst_port`, `dst_ip`: Connection metadata.
* `rule_names`, `observation_name`, `detection_types`: Threat labeling.
* `creation_time`, `end_time`, `duration`, `hour`: Temporal features.

---

## 📊 Exploratory Data Analysis (EDA)

* Time-series plots revealed **clear traffic surges during business hours**, and long periods of inactivity likely corresponding to downtime or off-hours.
* **Top IPs and country codes** identified frequent traffic sources, with the U.S. and Canada being dominant.
* Features like `bytes_ratio` helped capture abnormal sessions where inbound traffic greatly outweighed outbound traffic.

---

## 🧠 Modeling Approach

### 🔹 Unsupervised Anomaly Detection

* **Model**: Isolation Forest
* **Features Used**: `bytes_in`, `bytes_out`, `bytes_ratio`, `hour`, and one-hot encoded country codes
* **Outcome**:

  * \~5.3% of the traffic flagged as anomalous
  * Frequent anomalies from a small number of IPs (e.g., `155.91.45.242`)
  * Behavior aligned with possible bot or automated attack activity

### 🔹 Supervised Classification (Optional)

* Prepared for future use using `rule_names` as target labels (all labeled "Suspicious Web Traffic").
* Feature selection and encoding handled, model-ready data pipeline created.

---

## 📈 Key Findings

* **Anomalous traffic** is concentrated in a **few high-frequency IPs**, indicating repeated scanning or probing.
* Sudden **traffic spikes** could imply possible attack attempts like **data exfiltration or malware spread**.
* **Geographic concentration** suggests **targeted interaction** patterns.

---

## 🛡️ Potential Use Cases

* **Real-time anomaly detection pipeline** integrated with AWS Lambda and CloudWatch.
* **Threat intelligence enrichment** using geographic and behavioral profiling.
* **Alert systems** based on model predictions for early breach detection.

---

## 🛠️ Next Steps

* Deploy the anomaly detection model as a cloud-based API or Lambda function.
* Extend to supervised classification as more diverse labels are introduced.
* Introduce behavioral clustering for deeper pattern mining.

---

## 🧾 Requirements

* Python 3.8+
* pandas, scikit-learn, matplotlib, seaborn
* Jupyter or compatible Python IDE

---

## 👨‍💻 Author

Gauri Badhe
Data Scientist | Cloud Security Enthusiast
