+++
title = 'Creating browser extension icon files with Bash'
date = 2025-05-26T23:34:59-07:00
+++

When creating a browser extension, you will probably want an icon as an SVG and multiple PNGs of various sizes.

Below is a small Bash function that converts an SVG into several PNGs. It takes one input of the file path of the SVG and creates the PNGs in the same folder. The function depends on Inkscape.

```bash
# ,ext-icons converts an SVG into all the PNGs needed for a browser extension
my-ext-icons() {
    svg_path="$1"
    # echo "svg_path=$svg_path"
    svg_dir="${svg_path%/*}"
    # echo "svg_dir=$svg_dir"
    svg_name="${svg_path##*/}"
    # echo "svg_name=$svg_name"
    svg_stem="${svg_name%.*}"
    # echo "svg_stem=$svg_stem"

    widths=(16 32 48 96 128)

    for width in "${widths[@]}"; do
        dest_png="${svg_dir}/${svg_stem}-${width}.png"
        inkscape "${svg_path}" --export-width="${width}" --export-type="png" --export-filename="${dest_png}"
    done
}
alias ,ext-icons=my-ext-icons
```

This function demonstrates some file path processing and Inkscape's CLI. ImageMagick would probably also work well here in place of Inkscape.
