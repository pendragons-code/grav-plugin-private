## Context
I have decided that this project is something that I would like to work on, I am an amateur and do not have a history so please be patient with me.<br>
While using this plugin, I noticed a few glaring issues, such as the project using SHA1, which has been long deprecated, alongside some of the existing community issues. Therefore, I would just be making my own "fork" to get this a little more secure.

## Current Security Issues

1. **Weak Password Hashing**: 
   - Using simple SHA-256 without salt is vulnerable to rainbow table attacks
   - No adaptive hashing mechanism (like bcrypt) that can be strengthened over time

2. **Predictable Session Management**:
   - Session tokens are derived directly from usernames (hash('sha256', $username))
   - Session tokens never change between logins
   - No session timeout functionality

3. **No Brute Force Protection**:
   - No mechanism to limit or delay repeated login attempts
   - No account lockout after failed attempts

4. **Authentication Implementation**:
   - Does not leverage native Grav authentication mechanisms
   - Could benefit from integration with existing Grav user management

5. **Input Validation**:
   - Basic form validation but no real sanitization of inputs
   - Potential for injection if usernames or other inputs aren't properly validated

6. **No Auditing or Logging**:
   - No logging of login attempts, successful or failed
   - No logging of access to protected pages

## Todo List for More Secure Version

```
TODO for Private Plugin Security Upgrade:

1. Password Management
   - [ ] Implement PHP's password_hash() and password_verify() functions
   - [ ] Add mechanism to upgrade legacy passwords
   - [ ] Add password complexity requirements (optional for admins)

2. Session Security
   - [ ] Generate random session tokens using random_bytes()
   - [ ] Implement session timeout/expiration
   - [ ] Add session regeneration on privilege level changes

3. Brute Force Protection
   - [ ] Implement failed login attempt tracking
   - [ ] Add progressive delays or temporary lockouts
   - [ ] Add IP-based throttling (optional)

4. Code Improvements
   - [ ] Consider integration with Grav's user management
   - [ ] Refactor to follow modern PHP practices
   - [ ] Add proper PHPDoc comments
   - [ ] Implement PSR-12 coding standards

5. Additional Features
   - [ ] Add login/access logging
   - [ ] Add configurable redirect options
   - [ ] Add two-factor authentication support (optional)
   - [ ] Add remember-me functionality (optional)

6. Documentation
   - [ ] Document secure configuration for production
   - [ ] Provide upgrade path guidance for existing users
   - [ ] Document all configuration options
```

These improvements would significantly enhance the security posture of the plugin while maintaining its core functionality. The most critical changes would be implementing proper password hashing with PHP's password_hash() function and improving the session management system to use truly random tokens instead of username-derived ones.
