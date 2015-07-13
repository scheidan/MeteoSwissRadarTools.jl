*******************************************************************************
*                                                                             *              
*                     DATASET OF 4th GENERATION RADAR DATA FROM METEOSWISS    *
*                                                                             *
*                                                                             *
*                           MeteoSwiss RASA Group, Locarno-Monti              *
*                                                                             *
*                                   v. 1.4, 24/07/2013                        *
*                                                                             *
*                                                                             *
*******************************************************************************





Table of Contents
-----------------

1. Content of this package

	1.1 PRECIP product

	1.2 PRECIP-SV product

2. Decoding of numerical products

	2.1 File format and intensity scale
	
	2.2 Georef

	2.3 Metadata

3. Additional release notes





1. Content of this package
--------------------------

This package contains some sample data of the MeteSwiss new 4th generation weather radar network.
These products are provided as a base for technical tests such as reading and decoding (see following paragarph): their
meteorological content shall not be taken into account.

Two products are provided: PRECIP and PRECIP-SV.


1.1 PRECIP product
------------------

The product ID for PRECIP is 'RZC'. The sample data contain four different types of PRECIP product, subdivided in the following sub-folders:

- RZC-numerical: this product is intended for numerical use. This means its values can be read and converted to 256 classes of rain intensities
(including missing value). The scale to be applied for decoding is given below.

- RZC-numerical-georef: same as RZC-numerical, but in TIFF format with additional georef information (well suited for GIS application)

- RZC-web-alps: this product is intended for the web and it comes as a finished product, with over- and underlay. It cannot be decoded as
a numerical product. The domain of this product covers the Alps region and it corresponds to the standard, 4th generation radar data
domain (see below for further information about the geographical domain).

- RZC-web-swiss: same as RZC-web-alps, but with a smaller domain that covers only Switzerland. It cannot be decoded as a numerical product.

- RZC-web-transparent: this product is very similar to RZC-web-alps (same number of intensity classes and same domain), but it has no
overlay and underlay (underlay and overlay maps can be delivered separately, if required).


1.2 PRECIP-SV product
---------------------

The product ID for PRECIP-SV is 'TZC'. The sample data contain three different types of PRECIP-SV product, subdivided in the following sub-folders:

- TZC-numerical: this product is intended for numerical use. This means its values can be read and converted to 256 classes of rain intensities
(including missing value). See below for the scale to be applied for decoding.

- TZC-web-alps: this product is intended for the web and it comes as a finished product, with over- and underlay. It cannot be decoded as
a numerical product. The domain of this product covers the Alps region and it corresponds to the standard, 4th generation radar data
domain (see below for further information about the geographical domain).

- TZC-web-transparent: this product is very similar to TZC-web-alps (same number of intensity classes and same domain), but it has no
overlay and underlay (underlay and overlay maps can be delivered separately, if required). It cannot be decoded as a numerical product.


2. Decoding of numerical products
---------------------------------

2.1 File format and intensity scale
-----------------------------------

All products come in GIF format. The numerical products, that is the ones that can be read and decoded in order to use the content for
numerical computations (see also the previous paragraph), use the so called "RGB_datalevels256.dat" scale. This scale allows mapping the 
RGB code of the gif file to a phisical value in mm/h of precipitation.

The "RGB_datalevels256.dat" scale can be found in the file '8bit_Metranet_v102.txt'.

Special values:

index     R       G       B        mm/h
  0	  147	      163	 160      -10.0 --> no data
[...]
255	    0	        0	  55      9999.9 --> missing value


All modern programming languages provide interfaces to read GIF encoded files, it should therefore be quite easy to convert the provided
gif files into a matrix with physical values in mm/h of precipitation.


2.2 Georef
----------

PRECIP domain
-------------

The standard, 4th generation MeteoSwiss radar data domain is illustrated in the file 'RZC-georef.png'.

The size of one pixel is of 1x1 km.
The swiss coordinates of the corners are defined as follows:

Lower-left corner   : -160, 255
Upper-right corner  :  480, 965

Size in pixels: 640 x 710 (columns x rows)


PRECIP-SV domain
----------------

The PRECIP-SV prodcut also uses the standard, 4th generation MeteoSwiss radar domain. However, due to the presence of the side views,
the size in pixels of these files is larger. Please refer to the file 'TZC_georef.png' for the details.


PRECIP product, web format, swiss domain
----------------------------------------

This product provides a zoom over Switzerland.
The swiss coordinates of the corners are defined as follows:

Lower-left corner   :   32, 435
Upper-right corner  :  302, 845

Size in pixels: 270 x 410 (columns x rows)

Important note: since this product is not yet final, only one sample is provided, in PDF format.
The sample data for this product will be delivered later.


2.3 Metadata
------------

Every product comes with a set of metadata, which are written as an ASCII text in the comments field of the GIF file.

Here is an example of the metadata that are currently available:

PID=RZC RADAR=ADL REQ_RADAR=ADL QUALITY=777 THR_QUAL=555 TIME=132051200
ROW=640 COLUMN=710 RESOLUTION=1 filter=0
LATSW=43.630 LONSW=3.169 LATNW=49.377 LONNW=2.690 LATNE=49.365 LONNE=12.463 LATSE=43.620 LONSE=11.957
CHXNW=480 CHYNW=255 CHXNE=480 CHYNE=965 CHXSW=-160 CHYSW=255 CHXSE=-160 CHYSE=965
DATA=PRECIP UNIT=mm/h
SCALE=/opt/local/opkg/share/ccs4/etc/gifs/RGB_datalevels256.dat



Metadata description:

PID: product identifier
RADAR: radars used in the composite product (A for Albis, D for La Dole, L for Mt. Lema)
REQ_RADAR: requested radars to be inserted in the composite product (A for Albis, D for La Dole, L for Mt. Lema)
QUALITY: quality of the single site radar data (7 being the best, 0 the worst)
THR_QUAL: only radar with quality greater or equal this number are inserted in the composite
TIME: timestamp of the image, coded as follows: YYJJJHHmm (YY = year, JJJ = julian day of year, HH = UTC hour, mm = minutes)
ROW: number of rows
COLUMN: number of columns
RESOLUTION: size of the pixel in km
LATSW = latitute of the SW corner of the SW pixel of the image
LONSW = longitude of the SW corner of the SW pixel of the image
LATNW = latitute of the NW corner of the NW pixel of the image
LONNW = longitude of the NW corner of the NW pixel of the image
LATNE = latitute of the NE corner of the NE pixel of the image
LONNE = longitude of the NE corner of the NE pixel of the image
LATSE = latitute of the SE corner of the SE pixel of the image
LONSE = longitude of the SE corner of the SE pixel of the image
CHYSW = swiss-CHY of the SW corner of the SW pixel of the image
CHXSW = swiss-CHX of the SW corner of the SW pixel of the image
CHYNW = swiss-CHY of the NW corner of the NW pixel of the image
CHXNW = swiss-CHX of the NW corner of the NW pixel of the image
CHYNE = swiss-CHY of the NE corner of the NE pixel of the image
CHXNE = swiss-CHX of the NE corner of the NE pixel of the image
CHYSE = swiss-CHY of the SE corner of the SE pixel of the image
CHXSE = swiss-CHX of the SE corner of the SE pixel of the image
DATA = type of product
UNIT = unit 
SCALE = scale used to map RGB values to physical values


Filename: please note that the filename will of the real-time delivered files will be different from 
the one in this dataset.


3. Additional release notes
---------------------------

- The products are intended as a sample dataset, the meteorological content shall not be considered.
- The 4th generation MeteoSwiss radar data geographical domain is defined and will not change.
- The metadata of the files may undergo some adaptations, based on the feedback we will receive
after distributing this dataset.
- Also the RGB_datalevels256 conversion scale could be slightly modified in the future.
- Please send your comments, feedback and questions to the address rad4alp_spoc@meteoswiss.ch




Locarno-Monti, july 24th, 2013
