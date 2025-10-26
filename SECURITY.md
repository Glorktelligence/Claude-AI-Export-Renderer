# Security Policy

## Supported Versions

The Claude AI Export Renderer is currently a single-file application. Security updates are provided for the latest version available in the repository.

| Version | Supported |
| ------- | --------- |
| Latest  | ✅        |
| < 1.0.2 | ❌        |

## Security Considerations

### Data Privacy

This tool is designed with privacy-first principles:

- **Local Processing Only**: All conversation data remains on your device
- **No Network Requests**: The application does not transmit any data externally
- **Browser-Based**: Runs entirely in your web browser without server dependencies
- **No Data Storage**: Does not save or cache your conversation data

### Client-Side Security

- The application processes potentially large JSON files containing personal conversation data
- All parsing and rendering happens locally in your browser
- No external JavaScript libraries are loaded from CDNs
- All dependencies are embedded within the single HTML file

## Reporting a Vulnerability

If you discover a security vulnerability in the Claude AI Export Renderer, please report it responsibly by following these steps:

### Where to Report

**Email**: security@glorktelligence.co.uk

### What to Include

Please include the following information in your report:

- A clear description of the vulnerability
- Steps to reproduce the issue
- Potential impact assessment
- Any suggested fixes or mitigations
- Your contact information for follow-up questions

### Response Timeline

- **Initial Response**: Within 48 hours of receiving your report
- **Assessment**: Security reports will be evaluated within 5 business days
- **Updates**: You will receive regular updates on the progress
- **Resolution**: Critical vulnerabilities will be addressed with high priority

### Responsible Disclosure

- Please allow reasonable time for the vulnerability to be addressed before public disclosure
- We request that you do not publicly disclose the vulnerability until we have had a chance to investigate and provide a fix
- Credit will be given to security researchers who responsibly disclose vulnerabilities

## Security Best Practices for Users

When using the Claude AI Export Renderer:

1. **Download from Official Sources**: Only download the tool from the official GitHub repository
2. **Verify File Integrity**: Check that the HTML file hasn't been modified if obtained from third parties
3. **Use Updated Browsers**: Ensure your web browser is up to date with the latest security patches
4. **Local Use Only**: Run the tool locally on your device rather than uploading it to web servers
5. **Conversation Data**: Only load conversation exports that you have legitimately obtained from your own Claude account

## Known Security Considerations

### Browser Security

- The tool relies on browser security features for safe JSON parsing
- Large files (50MB+) may impact browser performance but do not pose security risks
- Modern browsers provide sandboxing that isolates the application from your system

### Data Handling

- Conversation exports may contain sensitive personal information
- Users are responsible for the security of their conversation data files
- The tool does not implement additional encryption beyond what your browser provides

## Security Updates

Security updates will be:

- Released as updated versions of the HTML file
- Announced in the repository README and release notes
- Communicated to users who have reported security issues

## Contact

For security-related questions or concerns that are not vulnerabilities:

- **General Support**: support@glorktelligence.co.uk
- **Security-Specific**: security@glorktelligence.co.uk

## Acknowledgments

We appreciate the security research community's efforts to improve the safety of open source tools. Responsible disclosure helps protect all users while allowing time for proper fixes to be developed and deployed.
