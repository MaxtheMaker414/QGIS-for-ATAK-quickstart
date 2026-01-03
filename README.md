QGIS Georeferencer Quickstart

1. Prerequisites

QGIS

A photo, orthophoto, or a historical map

Reference coordinates or a suitable basemap (e.g. OpenStreetMap, Google Satellite)



---

2. Installation of Required Layers

Adding a WMS Layer

To add a WMS basemap (e.g. Basemap Germany):

1. Right-click on WMS Layers → Add New Connection


2. Add the source:

https://sgx.geodatenzentrum.de/wms_basemapde?



Adding XYZ Tiles

To add XYZ tiles (e.g. Google Satellite):

1. Right-click on XYZ Tiles → Add New Connection


2. Add the source:

http://mt1.google.com/vt/lyrs=s&x={x}&y={y}&z={z}




---

3. Load an Image into the Georeferencer

1. Open the Georeferencer via Layer → Georeferencing.


2. Click Open Raster (image icon).


3. Select your non-georeferenced map (e.g. a historical map as PNG, JPG, TIFF).




---

4. Set Ground Control Points (GCPs)

Choose the Basis for Georeferencing

Option 1: Load a basemap in QGIS (e.g. OpenStreetMap) and manually transfer points.

Option 2: Use known coordinates from map borders or distinctive features.


Add Ground Control Points

1. Click Add GCP Point (icon with the red cross).


2. Select a distinctive point in your image (e.g. a road intersection or a building).


3. Enter the known coordinates manually or select them directly from a basemap:

Click From Map Canvas.

QGIS automatically switches to the main map view, where you can mark the point.

The coordinates are transferred automatically.




Note: Repeat this step for at least 4 GCPs (more points improve accuracy).


---

5. Choose Transformation Settings

Transformation Type

Depending on the type of distortion in the map, an appropriate transformation can be selected:

Transformation Type	Description	Use Cases

Linear (Affine)	Translates, scales, rotates, and skews the image while preserving straight lines. Requires at least 3 points.	When the map has only minor distortions.
Polynomial 1 (Linear)	Identical to the affine transformation. Uses a simple mathematical relationship. At least 3 points required.	For maps with minor distortions.
Polynomial 2 (Quadratic)	Adds quadratic curvature. At least 6 points required.	If the original map shows moderate distortions.
Polynomial 3 (Cubic)	Uses a more complex calculation for strong distortions. At least 10 points required.	Historical maps with major deformations.
Thin Plate Spline (TPS)	An elastic model for flexible deformations without a fixed mathematical function. At least 3 points required.	Maps with strong local distortions (e.g. hand-drawn maps).
Projective Transformation	Allows perspective distortions to fit an image onto a flat plane. At least 4 points required.	Aerial and satellite imagery.
Helmert Transformation	Scaling, rotation, and translation without distortion. At least 2 points required.	When only rotation or translation is needed.


Resampling Method

The resampling method determines how pixel values are interpolated:

Method	Description	Use Cases

Nearest Neighbor	Takes the value of the nearest pixel. Fast, but stair-step effects may occur.	Categorical data (e.g. land use maps).
Bilinear Interpolation	Averages the values of the 4 nearest pixels for smooth transitions.	Aerial and satellite imagery.
Cubic Convolution	Uses 16 neighboring pixels for smoother transitions (may introduce slight blur).	High-resolution raster images.
Cubic Spline	Uses a mathematical spline function for very smooth interpolation.	Maps with smooth transitions, elevation models.
Lanczos	Uses a larger pixel neighborhood for sharp, precise interpolation. Computationally intensive.	High-precision image processing, remote sensing.


Compression Settings

Compression Type	Description	Use Cases

None (No Compression)	Stores the raster without compression. Maximum quality, but large file size.	When storage space is not a concern.
LZW	Lossless compression, efficiently reduces file size.	Topographic maps, DEMs.
PackBits	Older, fast lossless compression, but less efficient than LZW.	Binary rasters (e.g. black-and-white scans).
DEFLATE (Zlib/GZIP)	Lossless, effective compression with higher computational cost than LZW.	Large GeoTIFF files with numeric data.


After selecting the settings, choose the output location for the georeferenced map and click OK.


---

6. Start Georeferencing

1. Click Start (green arrow).


2. QGIS processes the image and saves it as a georeferenced raster.


3. Close the Georeferencer.




---

7. Load the Georeferenced Map in QGIS

1. Go to Layer → Add Layer → Add Raster Layer.


2. Select the newly georeferenced TIFF file.


3. Check whether the map aligns with other basemaps.



Tip: If the map does not align correctly, review the GCPs and transformation settings.


---

8. Convert PDF to GeoTIFF

If a georeferenced PDF already exists, it can be converted to a GeoTIFF:

1. Open QGIS.


2. Go to Raster → Conversion → Translate (Convert).


3. Select the PDF file as input.


4. Set the output format to GeoTIFF.


5. Choose an appropriate coordinate reference system (e.g. EPSG:4326).


6. Click OK to convert the PDF to GeoTIFF.



If the PDF contains multiple layers, a specific layer can be selected before export.