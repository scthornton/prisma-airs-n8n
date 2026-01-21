# Security Policy

## Reporting a Vulnerability

The security of this project is taken seriously. If you discover a security vulnerability, please report it privately.

### How to Report

**Email:** scott@perfecxion.ai

Please include the following information in your report:

- Description of the vulnerability
- Steps to reproduce the issue
- Potential impact of the vulnerability
- Any suggested fixes or mitigations

### Response Timeline

- **Initial Response:** Within 48 hours of report submission
- **Status Update:** Within 7 days with assessment and planned actions
- **Resolution:** Timeline depends on severity and complexity

### Disclosure Policy

- Please allow reasonable time for the vulnerability to be fixed before public disclosure
- We will credit reporters in security advisories (unless anonymity is requested)
- We follow coordinated vulnerability disclosure practices

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| Latest  | :white_check_mark: |
| < 1.0   | :x:                |

## Security Best Practices

When using this project:

1. **Protect API Keys:** Never commit `.env` files or expose API keys
2. **Use Strong Credentials:** Rotate API keys regularly
3. **Monitor Access:** Review n8n access logs and Prisma AIRS security events
4. **Keep Updated:** Use the latest version of n8n and dependencies
5. **Network Security:** Run in isolated networks or use proper firewall rules
6. **Review Workflows:** Audit imported workflows before execution
7. **Enable Logging:** Monitor all security events in Prisma Cloud Console

## Known Security Considerations

- This project handles sensitive API keys and requires proper secret management
- n8n workflows can execute arbitrary code - only import trusted workflows
- Prisma AIRS provides runtime protection but cannot prevent all attacks
- Keep all dependencies updated to patch known vulnerabilities

## Contact

For general security questions or concerns:
- **Primary:** scott@perfecxion.ai
- **Alternative:** scthornton@gmail.com
