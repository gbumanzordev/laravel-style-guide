# Community Laravel Style Guide :pencil:

This style guide is a compilation of online articles and existing documentation about the style guide you must follow, feel free to create issues and submit pull requests if there are typos or any other misleading information.

## Table of contents:

This table is order alphabetically and therefore its order is not mandatory to be followed.

1. Configuration
2. Database Conventions
3. Design Patterns
4. Environment
5. Naming Conventions
6. Scalability
7. Testing

## Configuration

### Environment Variables

**All the sensitive information must be put into .env files**
Use .env files to store any secure information and retrieve it via `env()` function. There should be no instance on which you will put it inside models/controllers and commit it to git.

**Good**\

```php
// .env
API_HOST=https://example.com/api
API_USERNAME=foo
API_PASSWORD=bar

// access the value from app/config.php file

return [
  ...
  'api_host' => env('API_HOST', 'https://defaultdomain.com')
  'api_username' => env('API_USER', 'foo')
  'api_password' => env('API_USER', 'bar')
]

```

**Bad**

```php

define('API_HOST', 'https://laravel.com');
define('API_USERNAME', 'foo');
define('API_PASSWORD', 'bar');

class DomainController extends Controller
{
    public function index()
    {
      $api_username
    }

```
