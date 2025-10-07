# Aikido Firewall Setup

This document describes the Aikido Firewall setup for the OWASP Juice Shop application.

## Overview

Aikido Firewall is an in-app runtime protection solution that helps defend Node.js applications against various security threats including:
- SQL injection
- NoSQL injection
- Command injection
- Path traversal
- Server-Side Request Forgery (SSRF)
- And more

## Setup Steps Completed

### 1. Package Installation

Added `@aikidosec/firewall` package to `package.json`:
```json
"dependencies": {
  "@aikidosec/firewall": "^1.7.14",
  ...
}
```

Run the following to install all dependencies:
```bash
npm install
```

### 2. Environment Configuration

Created `.env` file with the Aikido token:
```bash
AIKIDO_TOKEN=AIK_RUNTIME_41519_30917_EU_WKYuSUr5q4uQrSXlwJnnwQJ25ZYfQV9JsyG0S9bjmgozXXoK
```

**Important**: The `.env` file is excluded from version control via `.gitignore` to keep the token secure.

### 3. Code Integration

Added Aikido Firewall initialization at the top of `server.ts`:
```typescript
require('@aikidosec/firewall')
```

This must be the first require statement to ensure the firewall can properly intercept and protect all module loads.

## Running the Application

To start the application with Aikido Firewall enabled:

```bash
# Load environment variables and start
npm start
```

Or for development:
```bash
npm run serve:dev
```

The Aikido Firewall will automatically:
1. Load the token from the `AIKIDO_TOKEN` environment variable
2. Connect to the Aikido platform
3. Begin monitoring and protecting the application
4. Report security events to your Aikido dashboard

## Verification

Once the application is running, you can verify the Aikido Firewall setup by:

1. Checking the application logs for Aikido initialization messages
2. Visiting your Aikido account dashboard at https://app.aikido.dev
3. Confirming the application appears in the "Apps" section
4. Reviewing any security events or alerts

## Configuration Options

Additional Aikido configuration can be set via environment variables:

- `AIKIDO_BLOCK=true` - Enable blocking mode (default is detection only)
- `AIKIDO_DEBUG=true` - Enable debug logging
- `AIKIDO_DISABLE=true` - Temporarily disable the firewall

## Troubleshooting

If the Aikido Firewall is not working:

1. Ensure the `.env` file exists and contains the correct token
2. Verify the `require('@aikidosec/firewall')` is the first line after comments in `server.ts`
3. Check that `@aikidosec/firewall` is installed in `node_modules`
4. Review application logs for any Aikido-related errors
5. Ensure network connectivity to Aikido's platform

## Security Notes

- Keep your `AIKIDO_TOKEN` secure and never commit it to version control
- Regularly update the `@aikidosec/firewall` package to get the latest security protections
- Monitor the Aikido dashboard for security alerts and events
- Consider enabling blocking mode (`AIKIDO_BLOCK=true`) after testing

## Documentation

For more information, visit:
- [Aikido Documentation](https://docs.aikido.dev/)
- [Aikido NPM Package](https://www.npmjs.com/package/@aikidosec/firewall)
- [Aikido GitHub](https://github.com/AikidoSec)
