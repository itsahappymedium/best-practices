# Best Practices: PHP

## Brackets
## Quotes
Use single quotes to denote strings unless the string contains characters that would need to be escaped.

### Example

__INCORRECT__:

```php
$foo = "bar";
```

__CORRECT__:

```php
$foo = 'bar';
```

__INCORRECT__:

```php
$foo = 'I don\'t like that it\'s raining';
```

__CORRECT__:

```php
$foo = "I don't like that it's raining";
```

## Spacing
