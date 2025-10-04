# RailsStringMethods

RailsStringMethods brings Ruby on Rails string manipulation utilities to Python. This module provides familiar string transformation methods that Rails developers know and love, making string handling more intuitive and expressive.

## Key Features
- Rails-style string transformations: `titleize()`, `camelize()`, `underscore()`
- Pluralization and singularization with proper English grammar rules
- Parameterization and humanization for URL-friendly and readable strings
- Case manipulation utilities: `upcase()`, `downcase()`
- Text truncation with customizable endings
- Rails naming conventions: `tableize()`, `classify()`

## Installation
```bash
pip install RailsStringMethods
```

## Dependencies
- `inflect` - For proper English pluralization and singularization
- `re` (built-in) - For regular expression operations

## Core Functions

### Case Transformations

#### `upcase(s)`
Converts string to uppercase.
```python
from RailsStringMethods import upcase

upcase("hello world")    # "HELLO WORLD"
upcase("Python")         # "PYTHON"
```

#### `downcase(s)`
Converts string to lowercase.
```python
from RailsStringMethods import downcase

downcase("HELLO WORLD")  # "hello world"
downcase("PyThOn")       # "python"
```

#### `titleize(s)`
Converts string to title case (capitalizes each word).
```python
from RailsStringMethods import titleize

titleize("hello world")     # "Hello World"
titleize("API_KEY_NAME")    # "Api Key Name"
titleize("user_profile")    # "User Profile"
```

### Rails Naming Conventions

#### `camelize(s, uppercase_first_letter=True)`
Converts underscore-separated string to CamelCase.
```python
from RailsStringMethods import camelize

camelize("user_profile")              # "UserProfile"
camelize("api_key_name")              # "ApiKeyName"
camelize("user_profile", False)       # "userProfile" (lowerCamelCase)
```

#### `underscore(s)`
Converts CamelCase string to underscore-separated format.
```python
from RailsStringMethods import underscore

underscore("UserProfile")    # "user_profile"
underscore("APIKeyName")     # "a_p_i_key_name"
underscore("XMLParser")      # "x_m_l_parser"
```

#### `dasherize(s)`
Converts underscores to dashes (useful for CSS classes and URLs).
```python
from RailsStringMethods import dasherize

dasherize("user_profile")      # "user-profile"
dasherize("api_key_name")      # "api-key-name"
```

#### `humanize(s)`
Converts underscore-separated string to human-readable format.
```python
from RailsStringMethods import humanize

humanize("user_profile")      # "User profile"
humanize("api_key_name")      # "Api key name"
humanize("first_name")        # "First name"
```

### Database Naming Conventions

#### `tableize(s)`
Converts string to database table name format (pluralized and underscored).
```python
from RailsStringMethods import tableize

tableize("User")           # "users"
tableize("BlogPost")       # "blog_posts"
tableize("Category")       # "categories"
```

#### `classify(s)`
Converts table name to class name format (singularized and camelized).
```python
from RailsStringMethods import classify

classify("users")          # "User"
classify("blog_posts")     # "BlogPost"
classify("categories")     # "Category"
```

### Pluralization and Singularization

#### `pluralize(s)`
Converts singular noun to plural using proper English grammar rules.
```python
from RailsStringMethods import pluralize

pluralize("user")          # "users"
pluralize("category")      # "categories"
pluralize("child")         # "children"
pluralize("mouse")         # "mice"
pluralize("person")        # "people"
```

#### `singularize(s)`
Converts plural noun to singular using proper English grammar rules.
```python
from RailsStringMethods import singularize

singularize("users")       # "user"
singularize("categories")  # "category"
singularize("children")    # "child"
singularize("mice")        # "mouse"
singularize("people")      # "person"
```

### URL and Parameter Handling

#### `parameterize(s, separator='-')`
Converts string to URL-friendly format by replacing non-word characters.
```python
from RailsStringMethods import parameterize

parameterize("Hello World!")           # "hello-world"
parameterize("User's Profile Page")    # "user-s-profile-page"
parameterize("API & Documentation", '_') # "api_documentation"
```

### Text Utilities

#### `truncate(s, length, ending='...')`
Truncates string to specified length, adding custom ending if truncated.
```python
from RailsStringMethods import truncate

truncate("This is a long sentence", 10)              # "This is a..."
truncate("Short text", 20)                           # "Short text"
truncate("Long content here", 8, " [more]")          # "Long con [more]"
```

## Common Usage Patterns

### Converting User Input to Database Format
```python
from RailsStringMethods import tableize, parameterize

user_input = "Blog Post Category"
table_name = tableize(user_input)        # "blog_post_categories"
url_slug = parameterize(user_input)      # "blog-post-category"
```

### Converting Database Names to Display Format
```python
from RailsStringMethods import classify, humanize

table_name = "user_profiles"
class_name = classify(table_name)        # "UserProfile"
display_name = humanize(table_name)      # "User profiles"
```

### API Response Formatting
```python
from RailsStringMethods import camelize, underscore

# Convert snake_case to camelCase for JSON APIs
api_field = camelize("user_profile_id", False)  # "userProfileId"

# Convert camelCase back to snake_case
db_field = underscore("userProfileId")           # "user_profile_id"
```

### Form Field Generation
```python
from RailsStringMethods import humanize, parameterize

field_name = "email_address"
label = humanize(field_name)              # "Email address"
html_id = parameterize(field_name, '_')   # "email_address"
css_class = parameterize(field_name)      # "email-address"
```

## Rails Integration

This module is designed to work seamlessly with Rails conventions:

```python
# Model naming
model_name = classify("blog_posts")      # "BlogPost"
table_name = tableize("BlogPost")        # "blog_posts"

# URL generation
url_path = parameterize("User Profile Settings")  # "user-profile-settings"

# Form helpers
field_label = humanize("first_name")     # "First name"
field_id = underscore("FirstName")       # "first_name"
```

## Module Structure

The module exports all functions from `rails_string_methods_core.py`:

- Core string transformation functions
- Pluralization/singularization utilities  
- Rails naming convention helpers
- URL parameterization tools
- Text manipulation utilities

All functions are stateless and thread-safe, making them suitable for use in web applications and concurrent environments.