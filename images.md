# Best Practices: Images

## Responsible Responsive Images
## Background Images
## Native Images
## Tools
Use these tools to make your image optimization workflow easier.


### [TinyPNG](http://tinypng.com)
This tool allows you to drag and drop files from your desktop and have them optimized. Usually removes unused colors and has little to no noticeable effect on the quality of the image. Not uncommon to have 50% reduction in file size.


### [Kraken.io](https://kraken.io/web-interface)
This tool allows you to drag and drop files from your desktop and have them optimized. You can then download individual images or a zip file with all of them.

There are two options:

- Lossless - This mode will push your images to the extreme without changing a single pixel. (Better for large background images)
- Lossy - This mode will sacrifice a small amount of image quality, allowing you to save up to 90% of the image weight.


### [Sips](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/sips.1.html)
This is a command line tool on Mac which lets you batch crop and resize images.

Example usage (folder has a bunch of JPGs):

```sh
# Replace all JPGs in folder in a max image width or height of 1500px
$ sips -z 1500 *.JPG
```


### [Mogrify](http://www.imagemagick.org/script/mogrify.php)
This is a command line tool which lets you do pretty much anything to an image.

```sh
# Resize: Retain Aspect Ratio
# Usage: mogrify -resize [largest dimension] [filename]
# Usage: mogrify -resize [max width]x[max height] [filename]
$ mogrify -resize 500 logo.jpg

# Resize: Exact Dimensions
# Usage: mogrify -crop [width]x[height]+[x position]+[y position] +repage *.[file type]
$ mogrify -crop 250x250+0+0 +repage *.jpg

# Resize: Batch
# Usage: mogrify -resize [largest dimension] *.[file type]
# Usage: mogrify -resize [max width]x[max height] *.[file type]
$ mogrify -resize 1920x1200 *.jpg

# Conversion: Single
# Usage: mogrify -format [new image type] [filename]
$ mogrify -format png logo.jpg

# Conversion: Batch
# Usage: mogrify -format [new image type] *.[file type]
$ mogrify -format jpg *.png

# Conversion: Change the color of single color images (i.e. icons)
# Usage: convert [filename] -fill "[hex color]" -colorize 100%  [filename]
# Usage: for i in *.[filetype]; do convert $i -fill "[hex color]" -colorize 100%  $i; done
$ for i in *.png; do convert $i -fill "#555555" -colorize 100%  $i; done
```
