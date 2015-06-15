# Best Practices: WordPress

## General Theme Setup
## Editor Styles
## Using Advanced Custom Fields
## Linking to Pages and Forms in Templates
Try to avoid linking to specific pages, posts, or forms from your template file. While using Post IDs inside templates will often work just fine, we need to make sure our templates are portable from site to site.

__Rule of Thumb__: Build your templates assuming the database could get wiped out at any time or that the rows in the database could get jumbled.

### Solutions
To get around using Post IDs in template files, you can take an option-based approach. For example, create an Options page and use a [Post Object field type](http://www.advancedcustomfields.com/resources/post-object/) to allow the user to set the correct post, page, or form to load in the template.

__Note__: By default, Gravity Forms are hidden from the Advanced Custom Fields Post Object field types. To combat this, use [Gravity Forms ACF Field](https://github.com/stormuk/Gravity-Forms-ACF-Field).
