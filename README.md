# Security Checklists

A comprehensive collection of security checklists designed for security auditors, penetration testers, and security professionals conducting security assessments across various IT domains. This project serves as the database and source code for [securitychecklists.org](https://securitychecklists.org) - for the best user experience and to access these checklists during your security assessments, visit the website directly.

## Overview

This repository contains a curated collection of security checklists covering a wide range of cybersecurity topics. These checklists are designed to help security professionals ensure thorough and consistent security assessments, whether conducting penetration tests, security audits, or compliance reviews.

## Available Categories

### 1. Blockchain Security
Comprehensive security assessment checklists for blockchain technologies, smart contracts, decentralized applications, and cryptocurrency systems.

### 2. Cloud Security
Security checklists covering major cloud platforms, cloud infrastructure security, identity management, and compliance monitoring.

### 3. Application Security
Web application security, API security, authentication systems, secure coding practices, and dependency management security.

### 4. Mobile Security
Mobile application security assessments for both Android and iOS platforms, including app store compliance and privacy considerations.

### 5. Container Security
Containerization security including Docker, Kubernetes, image scanning, and supply chain security for containerized environments.

### 6. Infrastructure & Network Security
Network infrastructure security, server hardening, firewall configurations, and remote access security assessments.

### 7. Identity & Access Management
User lifecycle management, privileged access control, and multi-factor authentication implementation security.

### 8. CI/CD & DevSecOps
Secure development pipeline practices, secrets management, and automated security testing integration.

### 9. Compliance & Governance
Regulatory compliance frameworks, data privacy regulations, and industry standard security requirements.

### 10. Incident Response & Monitoring
Security monitoring systems, logging practices, SIEM deployment, and incident response procedures.

## Usage

Each checklist is provided in JSON format and follows a consistent structure:

```json
{
  "title": "Checklist Title",
  "description": "Checklist description",
  "categories": [
    {
      "id": 1,
      "category": "Category Name",
      "description": "Category description",
      "items": [
        {
          "id": "1.1",
          "item": "Security check item description",
          "severity": "Critical|High|Medium|Low|Optional"
        }
      ]
    }
  ]
}
```

## Collaboration

This project is open to collaboration from the security community. We welcome:

- **Contributions**: New checklists, improvements to existing ones, or additional security domains
- **Feedback**: Suggestions for improvements, corrections, or new areas to cover
- **Reviews**: Security professionals reviewing and validating checklist items
- **Translations**: Making these checklists available in multiple languages

### How to Contribute

1. **Fork the repository**
2. **Create a feature branch** for your changes
3. **Follow the existing JSON structure** for consistency
4. **Submit a pull request** with your improvements
5. **Include clear descriptions** of your changes

### Contribution Guidelines

- Maintain the established JSON structure and naming conventions
- Ensure all checklist items are actionable and specific
- Include appropriate severity levels for each item
- Provide clear, concise descriptions
- Follow security best practices and industry standards

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Disclaimer

These checklists are provided for educational and professional use. They should be used as part of a comprehensive security assessment methodology and do not guarantee complete security coverage. Always adapt checklists to your specific environment and requirements.

---

**Note**: Some checklists are marked as "Coming Soon" and are currently under development. These will be populated with comprehensive security guidelines as they are completed.
