# GrobTree Documentation

Central knowledge base for the GrobTree ecosystem. Start with the quick start guide if you're new, then explore how-to guides for daily workflows, and use the reference section when extending the platform.

## 🚀 Quick Start
- [5-Minute Quick Start](./quick-start.md) – Get up and running in minutes with step-by-step instructions
- [Starter Templates](#-starter-templates) – Ready-to-use configuration templates

## Onboarding
- [Getting Started Guide](./getting-started.md) – Install the plugin, configure sources, and tour the CXF demo.

## How-to Guides
- [Using GrobTree](./using-grobtree.md) – Navigate the tool window, manage tabs, and tune parsing behaviour.
- [Replay Apache CXF Requests](./cxf-request-replay.md) – Generate cURL commands and IntelliJ HTTP requests from CXF log nodes.
- [User Interface](./ui/user-interface.md) – Understand the tool window layout and primary actions.
- [Toolbar Buttons](./ui/toolbar-buttons.md) – Icon reference and behaviour for every GrobTree toolbar control.
- [IntelliJ Settings](./intellij-settings.md) – Configure GrobTree’s settings and advanced options inside the IDE.

## Reference
- [Extending GrobTree](./extending-grobtree.md) – Integrate custom listeners, factories, and log providers.
- [ConverterConfig.xml Reference](./converter-config.md) – Schema walkthrough covering regex, listeners, variables, and more.

## Legal
- [End User License Agreement](./legal/eula.md) – Terms for using the proprietary GrobTree IntelliJ plugin.
- [Privacy Policy](./legal/privacy.md) – Local data processing and privacy information.

## 📁 Starter Templates

Jumpstart your GrobTree configuration with these ready-to-use templates:

### 🟢 Beginner Templates
- [Minimal Template](./templates/minimal-template.xml) – Basic log parsing for standard formats
- [Web Application Template](./templates/web-app-template.xml) – HTTP request/response handling

### 🟡 Intermediate Templates
- [Microservices Template](https://github.com/bgronostay/grobtree-example-extension) – Trace ID correlation and distributed tracing
- [Database Query Template](https://github.com/bgronostay/grobtree-example-extension) – SQL query analysis

### 🔴 Advanced Templates
- [Custom Extension Template](https://github.com/bgronostay/grobtree-example-extension) – Full extension framework
- [Statistics Dashboard Template](https://github.com/bgronostay/grobtree-example-extension) – Metrics and KPI tracking

## 📚 Learning Resources

### Video Tutorials
- [Getting Started in 5 Minutes](https://youtu.be/example1) – Installation and first steps
- [Creating Your First Configuration](https://youtu.be/example2) – ConverterConfig.xml basics
- [Advanced Features](https://youtu.be/example3) – Custom processing and extensions

### Community & Support
- [FAQ & Troubleshooting](./faq.md) – Common issues and solutions
- [GitHub Discussions](https://github.com/bgronostay/grobtree/discussions) – Ask questions and share ideas
- [Report Issues](https://github.com/bgronostay/grobtree/issues) – Bug reports and feature requests

## 🤝 Get Help

### Common Issues Quick Fixes
- **"No nodes appear"**: Check your regex pattern in tab settings
- **"Slow performance"**: Reduce import range or optimize your configuration
- **"Tree too cluttered"**: Use search and filtering features

### Share Your Configurations
Found a great pattern? Share it with the community!
- Open a PR with your `ConverterConfig.xml`
- Include sample logs if possible
- We'll add it to the templates!
