---
title: gimp integration
id: gimp-integration
weight: 85
draft: false
author: "people"
---

GIMP can use darktable to open a raw file if the darktable executable is on the PATH. If the GIMP user opens a raw file, then GIMP invokes darktable with some special command line options to get a JPEG file:

```
darktable --gimp [version]
                 [file <path>]
                 [thumb <path> <dim>]
```

In all cases, darktable will report its result to GIMP wrapped in tags like this (where `<res>` depends on the command given):

```
<<<gimp
<res>
gimp>>>
```

`version`
: `<res>` is the version of the GIMP API (_not_ the darktable version).

`file <path>`
: Starts darktable in darkroom mode using the image defined by `<path>`. The user is prevented from switching to another mode. When the user closes the darkroom window the file is exported as an EXR file to a temporary location. The full path of the exported file is returned as `<res>`.

`thumb <path> <dim>`
: darktable writes a thumbnail JPEG file to a temporary location. `<path>` is the image file, `<dim>` (in pixels) is used for the greater of width/height required and the ratio is kept. The returned `<res>` has the following format:

* The full path of the exported file on the first line.
* The width and height of the original file as space-separated integers on the second line. These dimensions are informational and may not be accurate. For raw files this is the sensor size.


