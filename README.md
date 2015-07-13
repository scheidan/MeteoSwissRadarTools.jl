Utilities to handle radar products of Meteo Swiss
==================================================

[![Build Status](https://travis-ci.org/scheidan/MeteoSwissRadarTools.jl.svg?branch=master)](https://travis-ci.org/scheidan/MeteoSwissRadarTools.jl)
[![Coverage Status](https://img.shields.io/coveralls/scheidan/MeteoSwissRadarTools.jl.svg)](https://coveralls.io/r/scheidan/MeteoSwissRadarTools.jl?branch=master)


Installation
------------

```Julia
Pkg.clone("git://github.com/scheidan/MeteoSwissRadarTools.jl.git")
```


Usage
-----

So far the only functionality this package provides is to convert radar
`gif` files from Meteo Swiss into arrays of rain intensities.

TZC or RZC products can be imported with
```Julia
# The string contains the path to a radar gif file
A = read_radar(imagepath::String, x1, y1, x2, y2)

# alternatively an already imported as Image can be converted
A = read_radar(image::Image, x1, y1, x2, y2)

# The array `A` has the same orientation as the gif, i.e. `A[1,1]` is
# the northwest corner, `A[end,end]` southeast.
```

The region of interest is specified with:
 - (`x1`, `y1`), the coordinate CH1903 of the *bottom left* (southwest) point,
 - (`x2`, `y2`), the coordinate CH1903 of the *top right* (northeast) point.

Note, all coordinates must be multiples of 1000.


The conversion from RGB values ot rain intesities is based on the file
[`8bit_Metranet_v102.txt`](references/8bit_Metranet_v102.txt). Negative rain intensities encode the
following information:

```
-10.0  # echo suppressed
-90.0  # reserved
-100   # no echo / pixel not covered by any radar
```