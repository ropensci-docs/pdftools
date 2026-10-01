# Render / Convert PDF

High quality conversion of pdf page(s) to png, jpeg or tiff format, or
render into a raw bitmap array for further processing in R.

## Usage

``` r
pdf_render_page(
  pdf,
  page = 1,
  dpi = 72,
  numeric = FALSE,
  antialias = TRUE,
  opw = "",
  upw = ""
)

pdf_convert(
  pdf,
  format = "png",
  pages = NULL,
  filenames = NULL,
  dpi = 72,
  antialias = TRUE,
  opw = "",
  upw = "",
  verbose = TRUE
)

poppler_config()
```

## Arguments

- pdf:

  file path or raw vector with pdf data

- page:

  which page to render

- dpi:

  resolution (dots per inch) to render

- numeric:

  convert raw output to (0-1) real values

- antialias:

  enable antialiasing. Must be `"text"` or `"draw"` or `TRUE` (both) or
  `FALSE` (neither).

- opw:

  owner password

- upw:

  user password

- format:

  string with output format such as `"png"` or `"jpeg"`. Must be equal
  to one of `poppler_config()$supported_image_formats`.

- pages:

  vector with one-based page numbers to render. `NULL` means all pages.

- filenames:

  vector of equal length to `pages` with output filenames. May also be a
  format string which is expanded using `pages` and `format`
  respectively.

- verbose:

  print some progress info to stdout

## See also

Other pdftools:
[`pdf_ocr_text()`](https://docs.ropensci.org/pdftools/reference/pdf_ocr.md),
[`pdftools`](https://docs.ropensci.org/pdftools/reference/pdftools.md),
[`qpdf`](https://docs.ropensci.org/pdftools/reference/qpdf.md)

## Examples

``` r
# Rendering should be supported on all platforms now
# convert few pages to png
file.copy(file.path(Sys.getenv("R_DOC_DIR"), "NEWS.pdf"), "news.pdf")
#> [1] TRUE
pdf_convert("news.pdf", pages = 1:3)
#> Converting page 1 to news_1.png... done!
#> Converting page 2 to news_2.png... done!
#> Converting page 3 to news_3.png... done!
#> [1] "news_1.png" "news_2.png" "news_3.png"

# render into raw bitmap
bitmap <- pdf_render_page("news.pdf")

# save to bitmap formats
png::writePNG(bitmap, "page.png")
webp::write_webp(bitmap, "page.webp")

# Higher quality
bitmap <- pdf_render_page("news.pdf", page = 1, dpi = 300)
png::writePNG(bitmap, "page.png")

# slightly more efficient
bitmap_raw <- pdf_render_page("news.pdf", numeric = FALSE)
webp::write_webp(bitmap_raw, "page.webp")

# Cleanup
unlink(c('news.pdf', 'news_1.png', 'news_2.png', 'news_3.png',
 'page.jpeg', 'page.png', 'page.webp'))
```
