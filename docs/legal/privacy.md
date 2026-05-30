# GrobTree Privacy Policy

Effective date: May 30, 2026

This Privacy Policy describes how the GrobTree IntelliJ Plugin ("Plugin") handles data.

## Summary

GrobTree is designed for local log analysis inside JetBrains IDEs. The Plugin does not intentionally collect telemetry, analytics, crash reports, log contents, clipboard contents, or configuration data for transmission to the Developer.

## Data Processed Locally

Depending on how you use it, the Plugin may locally access and process:

- application logs imported from files or IDE run/debug configurations;
- external log files selected for tailing;
- GrobTree configuration files such as `ConverterConfig.xml`;
- selected tree nodes, generated output views, and temporary files created by Plugin actions;
- clipboard text when you explicitly use clipboard-related Plugin actions;
- Apache CXF request data when you explicitly use replay or curl-generation actions.

This processing happens locally in your JetBrains IDE environment.

## Data Sent to the Developer

The Plugin does not intentionally send your logs, files, clipboard contents, configuration data, telemetry, or analytics to the Developer.

If you contact the Developer, open a GitHub issue, send logs, or provide sample data, you choose what information to share through that separate communication channel.

## Third-Party Services

The Plugin is distributed through JetBrains Marketplace and runs inside JetBrains IDEs. JetBrains Marketplace, JetBrains IDEs, GitHub, and other services you choose to use are governed by their own privacy notices and terms.

The Plugin may open or generate local requests for JetBrains IDE features, such as the IntelliJ HTTP Client, when you explicitly use the relevant action. GrobTree does not automatically send those generated requests.

## Your Responsibility

Logs and configuration files can contain personal data, secrets, credentials, tokens, customer data, or confidential business information. Review your data before sharing it in bug reports, examples, screenshots, or support requests.

## Changes

This Privacy Policy may be updated when the Plugin changes. The current version is published in the GrobTree documentation repository.

## Contact

Bernd Gronostay  
Email: develop@gronostay.net  
GitHub: https://github.com/BGronostay
