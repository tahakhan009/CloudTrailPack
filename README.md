# Cribl Pack for AWS Security Lake (OCSF to CEF Conversion)

This Cribl Pack converts AWS Security Lake logs (in OCSF format) into Common Event Format (CEF). It includes support for multiple AWS sources and Palo Alto Networks Firewall logs. The following data sources are supported:

## Supported Sources

---

1. AWS CloudTrail
2. AWS VPC Flow Logs
3. AWS Route 53
4. AWS Security Hub
5. Palo Alto Networks Firewalls

## Features

---

* Parses OCSF-format logs from AWS Security Lake.
* Maps OCSF fields to standard CEF headers.
* Outputs in CEF key-value format.
* Reduces events by removing irrelevant or redundant fields.

## Directory Structure

```
aws-seclake-ocsf-to-cef-pack/
├── package.json
├── pipelines/
│   ├── cloudtrail_to_cef.json
│   ├── vpc_flow_to_cef.json
│   ├── route53_to_cef.json
│   ├── securityhub_to_cef.json
│   ├── paloalto_to_cef.json
├── functions/
│   └── ocsf_cef_transform.js
├── lookups/
│   └── ocsf_cef_field_mapping.csv
├── files/
├── readme.md
```

## Installation

---

1. Download the latest version of the Pack or clone it from your repository.
2. Zip the `aws-seclake-ocsf-to-cef-pack` folder correctly with the root `package.json` file present at the top level.
3. Upload it to your Cribl instance:

   * Go to Packs > Manage Packs > Install Pack > Upload `.zip`
4. Create routes for each source:

   * Set filters for identifying each log source (e.g. CloudTrail vs VPC Flow Logs).
   * Route to appropriate pipelines (e.g. `cloudtrail_to_cef`).
5. Optional: Edit the `ocsf_cef_field_mapping.csv` to adjust or add field mappings.

## Example Pipeline Usage

Each pipeline performs the following steps:

* Parses OCSF JSON event
* Extracts key metadata (e.g., `event.class`, `metadata.product`) to determine mapping
* Uses lookup table to convert to CEF
* Serializes as CEF string for downstream use

## Author Information

---

This Cribl Pack was authored and maintained by \Taha Khan, designed to enable streamlined integration between AWS Security Lake and any CEF-compatible SIEM.

For support or questions, contact: **\[[taha.khan@inetsystemsinc.com](mailto:taha.khan@inetsystemsinc.com)]**

## License

---

Apache 2.0 License
