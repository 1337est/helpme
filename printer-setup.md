# Initial setup steps for printer
- Print the network settings page from your printer
- Find the section that either says "IP IPv4" or "IPP"
    - **IP IPv4**: Note the IP address
    - **IPP**: Note the IPPS/IPP URL (should contain the IP Address)
* Install `cups` and `cups-pdf` if not already installed.
* `sudo systemctl enable --now cups.service`
* To determine whether the printer supports driverless printing, run the command:
```nu
ipptool -tv https://<ip-address>:631/ipp/print get-printer-attributes.test
| ^grep -E "ipp-versions-supported|document-format-supported|get-printer-attributes|printer-uri-supported|printer-info|printer-make-and-model|printer-resolution-default|printer-resolution-supported|print-color-mode-default|print-color-mode-supported|printer-location"
```
Not the output should have at least these values:
- The get-printer-attributes test returns PASS.
- The IPP version that the printer supports is 2.0 or higher.
- The list of formats contains one of the following:
    - application/pdf
    - image/urf
    - image/pwg-raster 
- For color printers, the output contains one of the mentioned formats and, additionally, image/jpeg.

Now you can run the commands:
```nu
# First enable share printing
cupsctl --share-printers

# Add the printer
lpadmin -p <printer-name> -E -D "Printer Description" -L "Downstairs Office" -v ipps://<ip-address>:631/ipp/print -m everywhere -o printer-is-shared=true
# -p is just the name of the printer. You can put anything you want technically
# -E enables the printer and accepts new print jobs immediately
# -D is the description for the printer
# -L is the location of the printer
# -v is one of the printer-uri-supported values
# -m is the driver, and must be everywhere. All others are deprecated.
# -o printer-is-shared=true just means it's a shared printer

# Now set the printer as your default printer
lpoptions -d <printer-name>
```

- Now set the default options. But first list available options for your printer:
`lpoptions -p <printer-name> -l`
Example output
```
PageSize/Media Size: 3.5x5 3.5x5.Borderless 4x6 4x6.Borderless 5x7 5x7.Borderless 8x10 8x10.Borderless A4 A4.Borderless A6 Env10 Executive FanFoldGermanLegal FolioSP Legal *Letter Letter.Borderless Oficio Statement Custom.WIDTHxHEIGHT
MediaType/Media Type: *Stationery PhotographicHighGloss Photographic PhotographicSemiGloss PhotographicGlossy PhotographicMatte StationeryLetterhead Envelope StationeryCoated
cupsPrintQuality/cupsPrintQuality: Draft *Normal High
ColorModel/Output Mode: *RGB Gray
Duplex/Duplex: *None DuplexNoTumble DuplexTumble
OutputBin/OutputBin: *FaceUp
```
The options with the * next to the value annotate the current default options.

- For PageSize, go look at your paper. It's either going to be Letter (8.5x11) or A4 (8.27x11.69)
- For MediaType, use Stationery since most likely your just printing documents mostly
- For cupsPrintQuality, use Normal, or High if you used Photographic* for MediaType
- For ColorModel, use RGB, not Gray
- For Duplex, use None (single sided printing), vs. DuplexNoTumble (flip on long) DuplexTumble (flip on short)

To change any of the options you would use:
```nu
lpoptions -p <printer-name> -o PageSize=Letter -o MediaType=Stationery -o cupsPrintQuality=Normal -o ColorModel=RGB -o Duplex=None
```
