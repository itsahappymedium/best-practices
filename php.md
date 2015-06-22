# Best Practices: PHP

## Brackets
When writing functions, place the leading bracket on the same line of the function declaration, and the trailing bracket on its own line:

__INCORRECT__:
```php
function foo()
{
  // Do the things
}
```

__CORRECT__:
```php
function foo() {
  // Do the things
}
```

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
Keep your PHP code readable to _humans_ (i.e. the rest of us). The great thing about PHP is that you can put space between blocks and chunk related lines together to make it easier to decipher.

- Add a space after function definition and the leading bracket
- Add a new line before a function's `return` call
- Pad function parameters in a function definition
- If passing a variable to a function, pad it with space. If sending only a string, no space is necessary

### Examples

__INCORRECT__:

```php
function foo($dogs){
  $bar=$dogs;
  return $bar;
}
foo('cats');
```

__CORRECT__:

```php
function foo( $dogs ) {
  $bar = $dogs;
  
  return $bar;
}

// Incorrect
$foo = 'cats';
foo($foo);

// Correct
foo('cats');

// Correct
$foo = 'cats';
foo( $foo );
```
