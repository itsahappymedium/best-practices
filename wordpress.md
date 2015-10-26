# Best Practices: WordPress

## General Theme Setup

### Dealing with the Admin Bar

When a WordPress user is logged in as an administrator, manager or editor, they'll get the WordPress admin bar which is fixed at the top of the screen.

This is fine, but it will often interfere with a fixed header.

Luckily, WordPress provides an `.admin-bar` utility class on the `<body>` element when this is active. We can use the utility class to push the fixed header below the admin bar using CSS:

```css
.admin-bar & {
    top: 48px;

    @media (min-width: 48em) {
        top: 32px;
    }
}
```

__Note__: Avoid attaching the position of the fixed header to whether the WordPress user is logged in. Remember, only certain WordPress users get an admin bar.


### Sass Mixin

In the latest Pattern Lab, there's a `nudge-admin-bar` mixin to produce the above CSS.

```scss
.header {
    @include nudge-admin-bar;
}
```

## Editor Styles
## Using Advanced Custom Fields
## Linking to Pages and Forms in Templates
Try to avoid linking to specific pages, posts, or forms from your template file. While using Post IDs inside templates would normally work fine, we should make our templates flexible.

__Rule of Thumb__: Build your templates assuming the database could get wiped out at any time or that the rows in the database could get jumbled.

### Solutions
To get around using Post IDs in template files, you can take an option-based approach. For example, create an Options page and use a [Post Object field type](http://www.advancedcustomfields.com/resources/post-object/) to allow the user to set the correct post, page, or form to load in the template.

__Note__: By default, Gravity Forms are hidden from the Advanced Custom Fields Post Object field types. To combat this, use [Gravity Forms ACF Field](https://github.com/stormuk/Gravity-Forms-ACF-Field).

#### Example: Printing out a Gravity Form

__INCORRECT__:

```php
gravity_form(1, false, false, false, null, true, 99);
```

__CORRECT__:

```php
$chosen_gravity_form = (int) get_field('contact_form', 'options');
gravity_form($chosen_gravity_form, false, false, false, null, true, 99); ?>
```

#### Example: Getting Child Pages

__INCORRECT__:

```php
function hm_get_team_members() {
    $team_members = hm_get_child_pages(96);

    return $team_members;
}
```

__CORRECT__:

```php
function hm_get_team_members() {
    $team_members_page = get_field('team_members_page', 'options');
    $team_members = hm_get_child_pages( $team_members_page->ID );

    return $team_members;
}
```
