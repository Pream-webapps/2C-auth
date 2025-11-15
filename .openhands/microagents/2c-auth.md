---
name: 2C-Auth Authentication Microagent
type: knowledge
version: 1.0.0
agent: CodeActAgent
triggers: []
---

# 2C-Auth Authentication Microagent

This microagent provides specialized knowledge and capabilities for working with the 2C-Auth authentication library, a maintained fork of Myth\Auth for CodeIgniter 4 projects.

## Overview

2C-Auth is a flexible, powerful, and secure authentication & authorization package for CodeIgniter 4, customized for Twocoms Consulting / EDU-ERP 3.0 projects. It provides:

- Password-based authentication with remember-me functionality
- Role-Based Access Control (RBAC) per NIST standards
- Ready-made views for login, registration, forgot/reset password
- Email-based account verification
- Extendable and customizable authentication flows

## Key Components

### Authentication Services
- **authentication** service - Handles login/logout, credential checks
- **authorization** service - Handles RBAC roles and permissions  
- **passwords** service - Strong password validation

### Models and Entities
- `UserModel` - User data management with role assignment support
- `Myth\Auth\Entities\User` - User entity with authentication methods
- Group and Permission models for RBAC

### Filters
- `LoginFilter` - Restrict routes to authenticated users
- `RoleFilter` - Restrict routes by user roles
- `PermissionFilter` - Restrict routes by specific permissions

### Helper Functions
Available via `helper('auth')`:
- `logged_in()` - Check if user is logged in
- `user()` - Get current User entity
- `user_id()` - Get current user ID
- `in_groups($groups)` - Check group membership
- `has_permission($perm)` - Check user permissions

## Common Tasks

### Installation and Setup
1. Install via Composer: `composer require pream-webapps/2c-auth:dev-develop`
2. Configure email settings in `app/Config/Email.php`
3. Add validation rules to `app/Config/Validation.php`
4. Run migrations: `php spark migrate -all`

### Customization
- Run `php spark auth:publish` to copy configs and views to app directory
- Modify `app/Config/Auth.php` for custom settings
- Override views by updating the `$views` mapping in Auth config

### Route Protection
```php
// In routes
$routes->get('admin/users', 'UserController::index', ['filter' => 'role:admin']);
$routes->group('api', ['filter' => 'permission:api.access'], function($routes) {
    // Protected API routes
});
```

### User Management
```php
// Create user with role
$userModel = new \Myth\Auth\Models\UserModel();
$user = $userModel->withGroup('admin')->insert($userData);

// Check permissions
if (has_permission('users.edit')) {
    // Allow editing
}
```

## Configuration Files

### Key Config Files
- `Config/Auth.php` - Main authentication configuration
- `Config/AuthGroups.php` - Role and permission definitions
- `Config/Email.php` - Email settings for verification/reset
- `Config/Validation.php` - Password validation rules

### Database Tables
- `auth_users` - User accounts
- `auth_groups` - User roles/groups
- `auth_permissions` - Individual permissions
- `auth_groups_permissions` - Group-permission relationships
- `auth_users_permissions` - User-specific permissions
- `auth_groups_users` - User-group relationships

## Security Considerations

- Always validate and sanitize user input
- Use CSRF protection on authentication forms
- Implement rate limiting for login attempts
- Use HTTPS in production
- Regularly update password hashing algorithms
- Monitor for suspicious authentication patterns

## Troubleshooting

### Common Issues
1. **Migration errors** - Ensure database is properly configured
2. **Email not sending** - Check Email.php configuration
3. **Views not found** - Verify view paths in Auth.php config
4. **Permission denied** - Check user roles and permissions setup

### Debug Tools
- Enable Debug Toolbar for authentication insights
- Check logs in `writable/logs/` for authentication errors
- Use `php spark auth:check` command for configuration validation

## Best Practices

1. **Role Design** - Create granular roles and permissions
2. **Password Policy** - Enforce strong password requirements
3. **Session Security** - Configure secure session settings
4. **Audit Logging** - Log authentication events for security monitoring
5. **Regular Updates** - Keep the library updated for security patches

## Integration with CodeIgniter 4

This microagent works specifically with CodeIgniter 4 applications using the 2C-Auth library. It understands:
- CodeIgniter 4 service container and dependency injection
- CI4 routing and filter system
- CI4 database migrations and models
- CI4 configuration system
- CI4 view rendering and templating

When working with authentication-related tasks, this microagent can provide context-aware assistance for implementing secure authentication flows, managing user roles and permissions, and troubleshooting common authentication issues in CodeIgniter 4 applications.