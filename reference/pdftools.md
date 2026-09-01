# PDF utilities

Utilities based on libpoppler for extracting text, fonts, attachments
and metadata from a pdf file.

## Usage

``` r
pdf_info(pdf, opw = "", upw = "")

pdf_text(pdf, opw = "", upw = "", raw = FALSE)

pdf_data(pdf, font_info = FALSE, opw = "", upw = "")

pdf_fonts(pdf, opw = "", upw = "")

pdf_attachments(pdf, opw = "", upw = "")

pdf_toc(pdf, opw = "", upw = "")

pdf_pagesize(pdf, opw = "", upw = "")
```

## Arguments

- pdf:

  file path or raw vector with pdf data

- opw:

  string with owner password to open pdf

- upw:

  string with user password to open pdf

- raw:

  return text in raw stream order. Default is to use physical layout
  order.

- font_info:

  if TRUE, extract font-data for each box. Be careful, this requires a
  very recent version of poppler and will error otherwise.

## Details

The `pdf_text` function renders all textboxes on a text canvas and
returns a character vector of equal length to the number of pages in the
PDF file. On the other hand, `pdf_data` is more low level and returns
one data frame per page, containing one row for each textbox in the PDF.

Note that `pdf_data` requires a recent version of libpoppler which might
not be available on all Linux systems. When using `pdf_data` in R
packages, condition use on `poppler_config()$has_pdf_data` which shows
if this function can be used on the current system. For Ubuntu 16.04
(Xenial) and 18.04 (Bionic) you can use [the
PPA](https://github.com/ropensci/pdftools#installation) with backports
of Poppler 0.74.0.

Poppler is pretty verbose when encountering minor errors in PDF files,
in especially `pdf_text`. These messages are usually safe to ignore, use
[`suppressMessages`](https://rdrr.io/r/base/message.html) to hide them
altogether.

## See also

Other pdftools:
[`pdf_ocr_text()`](https://docs.ropensci.org/pdftools/reference/pdf_ocr.md),
[`qpdf`](https://docs.ropensci.org/pdftools/reference/qpdf.md),
[`rendering`](https://docs.ropensci.org/pdftools/reference/pdf_render_page.md)

## Examples

``` r
# Just a random pdf file
pdf_file <- file.path(R.home("doc"), "NEWS.pdf")
info <- pdf_info(pdf_file)
text <- pdf_text(pdf_file)
fonts <- pdf_fonts(pdf_file)
files <- pdf_attachments(pdf_file)
```
