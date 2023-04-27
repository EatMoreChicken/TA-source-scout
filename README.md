# 🔍 Source Scout
## 📌 Description
Source Scout is a simple Splunk app that helps you monitor your data sources.

## 🔒 Prerequisites
- Splunk 8.0+ or later (I haven't tested it for older versions)
- Basic knowledge of Splunk search language (SPL)
- *Optional* Splunk App for Lookup File Editing (https://splunkbase.splunk.com/app/1724)

## 🚀 Installation
1. Clone or download the Source Scout app `.tar.gz` file.
2. Install the app via Splunk UI or copy it into the `$SPLUNK_HOME/etc/apps` directory.
3. Restart Splunk if necessary.

## 🎉 Features
- Monitors index-sourcetype pairs for outages or issues based on user-defined tolerance limits.
- Provides alerts with data source, latest timestamps, and state.

## ⚒ Usage
1. Run a search to determine the sources you would like to monitor. Add these sources and your preferred acceptable tolerance in seconds to the `source-scout-data-sources` KV-store lookup using the Splunk App for Lookup File Editing or other methods. The source should be in the `<index>|<sourcetype>` format. For example, the `windows` index and `xmlwineventlog` sourcetype should be `windows|xmlwineventlog`.
2. Update the `source-scout-search-constraint` macro to limit the data that's searched for monitoring. The search utilizing this macro is leveraging `tstats`, so you will need to use fields accepted in the `where` clause of `tstats` (Ex. `index, sourcetype, source`).
3. Enable the `Source Scout - Detect Source Outages` alert to start detections. Make sure to test the alerting.

## 📃 Drawbacks and Alternatives
- The alert uses `tstats` to pull information about data sources. Keep in mind that the `_time` used is based on the parsed timestamp. If you have timestamping issues for your log sources, it could through this off.
- This app was created to be a "lightweight" option for testing. However, if you require a more robust solution, [TrackMe](https://splunkbase.splunk.com/app/4621) is a well built and highly recommended alternative.

## 🤝 Contributing
Please feel free to contribute to the Source Scout project by creating pull requests, filing bug reports, or providing feedback.
