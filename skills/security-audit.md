# Security Audit Checklist

## Input Validation
- Validate all user inputs on both client and server
- Use whitelists instead of blacklists
- Sanitize inputs to prevent injection attacks
- Check input length and type

## Authentication & Authorization
- Use secure password hashing (bcrypt, argon2)
- Implement JWT or session-based auth properly
- Validate permissions before resource access
- Use HTTPS only for sensitive operations

## Data Protection
- Encrypt sensitive data at rest
- Use HTTPS for all communications
- Never log sensitive information
- Implement proper access controls

## Code Security
- Keep dependencies updated
- Avoid hardcoding secrets or API keys
- Use environment variables for configuration
- Implement rate limiting on APIs
- Validate API responses

## Error Handling
- Don't expose sensitive error details to users
- Log errors for debugging but sanitize logs
- Use custom error pages
- Implement proper CORS policies
