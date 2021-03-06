# esc2text

`esc2text` extracts text from binary ESC/POS files.

The plaintext output is UTF-8 encoded, and written to standard output.

It operates by reading all of the commands in the input file, and discarding
those which do not contain text or line breaks. Add `-v` as the last argument
to see all the other commands for debugging purposes.

## Installation

This utility is included with escpos-tools. See the
[escpos-tools documentation](https://github.com/receipt-print-hq/escpos-tools)
for installation instructions.

## Usage

```
php esc2text.php FILE [ -v ]
```

## Example

```
$ php esc2text.php receipt-with-logo.bin
ExampleMart Ltd.
Shop No. 42.

SALES INVOICE
                                               $
Example item #1                             4.00
Another thing                               3.50
Something else                              1.00
A final item                                4.45
Subtotal                                   12.95

A local tax                                 1.30
Total            $ 14.25

Thank you for shopping at ExampleMart
For trading hours, please visit example.com

Monday 6th of April 2015 02:56:25 PM
```

The same binary data, when sent to a printer, renders as below:

```
$ cat receipt-with-logo.bin > /dev/usb/lp0
```

![receipt-with-logo-small.png](https://raw.githubusercontent.com/receipt-print-hq/escpos-tools/master/doc/receipt-with-logo-small.png)

The input file used as an example here was generated by [escpos-php](https://github.com/mike42/escpos-php), and is available [here](https://raw.githubusercontent.com/receipt-print-hq/escpos-tools/master/receipt-with-logo.bin).

## Further conversions

This utility will create unformatted plaintext files. Other formats can be accessed
by performing a second conversion via the `unoconv` and `pandoc` utilites.

These can produce  DOC, HTML, PDF or RTF versions of the same output, among other formats.

In some cases, drivers convert text to a series of image before printing, so there is no
text the ESC/POS file. In this case, `esc2text` will correctly return a blank text file.
Images can be extracted with `escimage` and put through a suitable OCR tool.

## See also

- [esc2html](esc2html.md)
- [escimages](escimages.md)
