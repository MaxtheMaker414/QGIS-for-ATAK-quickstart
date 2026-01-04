
# QGIS Georeferencer – Quickstart

## 1. Prerequisites

| Requirement | Description |
|------------|-------------|
| QGIS | Installed desktop version |
| Raster image | Photo, orthophoto, or historical map |
| Reference data | Known coordinates or a basemap (e.g. OpenStreetMap, Google Satellite) |

---

## 2. Installation of Required Layers

### Adding a WMS Layer

Example: **Basemap Germany**

1. Right-click **WMS Layers** → **Add New Connection**
2. Add the source URL:
[https://sgx.geodatenzentrum.de/wms_basemapde](https://sgx.geodatenzentrum.de/wms_basemapde)?

---

### Adding XYZ Tiles

Example: **Google Satellite**

1. Right-click **XYZ Tiles** → **Add New Connection**
2. Add the source URL:
[http://mt1.google.com/vt/lyrs=s&x={x}&y={y}&z={z}](http://mt1.google.com/vt/lyrs=s&x={x}&y={y}&z={z})

---

## 3. Load an Image into the Georeferencer

1. Open **Layer → Georeferencing**
2. Click **Open Raster**
3. Select the non-georeferenced image  
*(PNG, JPG, TIFF – e.g. historical maps)*

---

## 4. Set Ground Control Points (GCPs)

### Choose the Basis for Georeferencing

- **Option 1:** Load a basemap (e.g. OpenStreetMap) and transfer points manually  
- **Option 2:** Use known coordinates from map borders or distinctive features  

---

### Add Ground Control Points

1. Click **Add GCP Point**
2. Select a distinctive point in the image  
*(road intersection, building, landmark)*
3. Define coordinates:
- Enter them manually **or**
- Click **From Map Canvas** and select the point on the basemap

> **Note:**  
> At least **4 GCPs** are required. More points improve accuracy.

---

## 5. Choose Transformation Settings

### Transformation Types

| Transformation | Description | Typical Use Case |
|---------------|------------|------------------|
| Linear (Affine) | Translation, scaling, rotation, skewing (≥ 3 points) | Minor distortions |
| Polynomial 1 | Same as affine (≥ 3 points) | Minor distortions |
| Polynomial 2 | Adds quadratic curvature (≥ 6 points) | Moderate distortions |
| Polynomial 3 | Complex cubic calculation (≥ 10 points) | Strongly distorted historical maps |
| Thin Plate Spline (TPS) | Elastic deformation model (≥ 3 points) | Local distortions, hand-drawn maps |
| Projective | Perspective correction (≥ 4 points) | Aerial or satellite imagery |
| Helmert | Scale, rotate, translate only (≥ 2 points) | No distortion required |

---

### Resampling Methods

| Method | Description | Use Case |
|------|-------------|----------|
| Nearest Neighbor | Fast, no interpolation | Categorical data |
| Bilinear | Averages 4 pixels | Aerial imagery |
| Cubic Convolution | Uses 16 pixels | High-resolution rasters |
| Cubic Spline | Smooth spline interpolation | Elevation models |
| Lanczos | Sharp, precise, slow | High-precision processing |

---

### Compression Settings

| Compression | Description | Use Case |
|------------|-------------|----------|
| None | Maximum quality, large files | Storage not an issue |
| LZW | Lossless, efficient | Topographic maps, DEMs |
| PackBits | Legacy lossless compression | Binary rasters |
| DEFLATE | Strong lossless compression | Large GeoTIFFs |

After configuration, select the output location and confirm with **OK**.

---

## 6. Start Georeferencing

1. Click **Start** (green arrow)
2. QGIS generates the georeferenced raster
3. Close the Georeferencer

---

## 7. Load the Georeferenced Map

1. Go to **Layer → Add Layer → Add Raster Layer**
2. Select the generated GeoTIFF
3. Verify alignment with basemaps

> **Tip:**  
> If alignment is incorrect, review GCP placement and transformation settings.

---

## 8. Convert PDF to GeoTIFF

For already georeferenced PDFs:

1. Open QGIS
2. **Raster → Conversion → Translate**
3. Select the PDF as input
4. Set output format to **GeoTIFF**
5. Choose the CRS (e.g. `EPSG:4326`)
6. Click **OK**

> If the PDF contains multiple layers, select the required layer before export.
