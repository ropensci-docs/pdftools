# OCR text extraction

Perform OCR text extraction. This requires you have the `tesseract`
package.

## Usage

``` r
pdf_ocr_text(
  pdf,
  pages = NULL,
  opw = "",
  upw = "",
  dpi = 600,
  language = "eng",
  options = NULL
)

pdf_ocr_data(
  pdf,
  pages = NULL,
  opw = "",
  upw = "",
  dpi = 600,
  language = "eng",
  options = NULL
)
```

## Arguments

- pdf:

  file path or raw vector with pdf data

- pages:

  which pages of the pdf file to extract

- opw:

  string with owner password to open pdf

- upw:

  string with user password to open pdf

- dpi:

  resolution to render image that is passed to
  [pdf_convert](https://docs.ropensci.org/pdftools/reference/pdf_render_page.md).

- language:

  passed to
  [tesseract](https://docs.ropensci.org/tesseract/reference/tesseract.html)
  to specify the languge of the engine.

- options:

  passed to
  [tesseract](https://docs.ropensci.org/tesseract/reference/tesseract.html)
  to specify OCR parameters

## See also

Other pdftools:
[`pdftools`](https://docs.ropensci.org/pdftools/reference/pdftools.md),
[`qpdf`](https://docs.ropensci.org/pdftools/reference/qpdf.md),
[`rendering`](https://docs.ropensci.org/pdftools/reference/pdf_render_page.md)
