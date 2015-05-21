# Best Practices: Images

## Responsible Responsive Images
## Background Images
## Native Images
## Tools
Use these tools to make your image optimization workflow easier.

### [TinyPNG](http://tinypng.com)
This tool allows you to drag and drop files from your desktop and have them optimized. Usually removes unused colors and has little to no noticeable effect on the quality of the image. Not uncommon to have 50% reduction in file size.

### `sips`
This is a command line tool on Mac which lets you batch crop and resize images.

Example usage (folder has a bunch of JPGs):

```sh
# Replace all JPGs in folder in a max image width or height of 1500px
$ sips -z 1500 *.JPG
```
