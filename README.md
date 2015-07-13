Utilities to handle radar products of Meteo Swiss
==================================================

[![Build Status](https://travis-ci.org/scheidan/MeteoSchweizRadarTools.jl.svg?branch=master)](https://travis-ci.org/scheidan/MeteoSchweizRadarTools.jl)


So far the only fuctionality this package povides is to convert radar
`gif` files from Meteo Swiss into arrays of rain intensities.

TZC or RZC products can be imported with
```Julia
# The string contains the path to a radar gif file
read_radar(imagepath::String, x1, y1, x2, y2)

# alternatively an already imported as Image can be converted
read_radar(image::Image, x1, y1, x2, y2)
```

The region of interest to convert is specified with:
 - (`x1`, `y1`), the coordinate CH1903 of the *bottom left* (southwest) point,
 - (`x2`, `y2`), the coordinate CH1903 of the *top right* (north east) point.

Note, all coordinate must be multiples of 1000.
