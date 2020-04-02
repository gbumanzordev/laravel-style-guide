# Community Laravel Style Guide :pencil:

This style guide is a compilation of online articles and existing documentation about the style guide you must follow, feel free to create issues and submit pull requests if there are typos or any other misleading information.

## Table of contents:

This table is order alphabetically and therefore its order is not mandatory to be followed.

1. [Configuration](https://github.com/gbumanzor/laravel-style-guide#configuration)
2. [Database Conventions]()
3. [Design Patterns]()
4. [Environment]()
5. [Naming Conventions](https://github.com/gbumanzor/laravel-style-guide#naming-conventions)
6. [Scalability]()
7. [Testing]()

## Configuration

### Environment Variables

**All the sensitive information must be put into .env files**
Use .env files to store any secure information and retrieve it via `env()` function. There should be no instance on which you will put it inside models/controllers and commit it to git.

**Good:**

```php
// .env
API_HOST=https://example.com/api
API_USERNAME=foo
API_PASSWORD=bar

// access the value from app/config.php file

return [
  ...
  'api_host' => env('API_HOST', 'https://defaultdomain.com'),
  'api_username' => env('API_USER', 'foo'),
  'api_password' => env('API_USER', 'bar'),
  ...
]

```

**Bad:**

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
}
```

Your application key MUST be set. This is the APP_KEY variable in your `.env` file. You can generate one via `php artisan key:generate`

### Package Configuration

Custom or package configuration filename **must** be in snake_case.
\
**Good:**

```php
config/my_config.php
```

**Bad:**

```php
config/myConfig.php // or
config/MyConfig.php // or
config/myconfig.php
```

\
Config and language files indexes **should** be in snake_case:
**Good:**

```php
// config/my_config.php
return [
  'my_api' => [
    'domain' => env('API_DOMAIN'),
    'secret' => env('API_SECRET'),
  ],
]
```

**Bad:**

```php
// config/myconfig.php
return [
  'MyApi' => [
    'DOMAIN' => env('API_DOMAIN'),
    'SECRET' => env('API_SECRET'),
  ],
]
```

## Naming Conventions

The following is the generally accepted naming conventions being used by **Laravel** Community.

### Controllers

Controller names must start with a noun (in singular form) followed by the word "Controller":

**Good:**

```php
class ArticleController extends Controller
{
  ...
}
```

**Bad:**

```php
class ArticlesController extends Controller
{
  ...
}

// or
class wp_articlesController extends Controller
{
  ...
}

// or
class Article extends Controller
{
  ...
}
```

**You should use [resource controllers](https://laravel.com/docs/5.7/controllers#resource-controllers) unless you have any particular reason not to do so.**

**Good:**

```php
class DomainController extends Controller
{
    public function index()
    {
      // list domains
    }
    public function create()
    {
      // show create form
    }
    public function store(Request $request)
    {
      // handle the form POST
    }
    public function show($id)
    {
      // show a single domain
    }
    public function edit($id)
    {
      // show edit page
    }
    public function update(Request $request, $id)
    {
      // handle show edit page POST
    }
    public function destroy($id)
    {
      // delete a domain
    }
}
```

**Bad:**

```php
class DomainController extends Controller
{
    public function list()
    {
      // list domains
    }
    public function create_or_save()
    {
      // show create form then handle save
    }
    public function show_edit($id)
    {
      // show a single domain then show edit page
    }
    public function delete($id)
    {
      // delete a domain
    }
}
```

### Models

Model names **must** be in singular form with its first letter in uppercase:

**Good:**

```php
class Flight extends Model
{
  ...
}
```

**Bad:**

```php
class Flights extends Model
{
  ...
}
```

`hasOne` or `belongsTo` relationship **must** be in singular form:

**Good:**

```php
class User extends Model
{
  public function phone()
  {
    return $this->hasOne('App\Phone');
  }
}
```

**Bad:**

```php
class User extends Model
{
  public function phones()
  {
    return $this->hasOne('App\Phone');
  }
}
```

Any other relationships other than above, **must** be in plural form:

Good:

```php
class Post extends Model
{
  public function comments()
  {
    return $this->hasMany('App\Comment');
  }
}
```

**Bad:**

```php
class Post extends Model
{
    public function comment()
    {
        return $this->hasMany('App\Comment');
    }
}
```

Model propierties **should** be in snake_case:

**Good:**

```php
$user->created_at
```

**Bad:**

```php
$user->createdAt
```

Methods should be in camelCase:

**Good:**

```php
class User extends Model
{
    public function scopePopular($query)
    {
        return $query->where('votes', '>', 100);
    }
}
```

**Bad:**

```php
class User extends Model
{
    public function scope_popular($query)
    {
        return $query->where('votes', '>', 100);
    }
}
```

### Functions:
