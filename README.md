# QGIS Georeferencer Quickstart

## 1. Voraussetzungen  

**QGIS** 
- Eine Foto, Orthofoto oder eine historische Karte  
- **Referenzkoordinaten** oder eine geeignete Basiskarte (z. B. OpenStreetMap, Google Satellite)  

---

## 2. Installation erforderlicher Layer  

### WMS Layer hinzufügen  

Um eine **WMS-Basiskarte** (z. B. Basemap Deutschland) hinzuzufügen:  

1. Rechtsklick auf **WMS-Layer** → **Neue Verbindung hinzufügen**  
2. Quelle hinzufügen:  

   ```
   https://sgx.geodatenzentrum.de/wms_basemapde?
   ```

### XYZ-Tiles hinzufügen  

Um **XYZ-Kacheln** (z. B. Google Satellite) hinzuzufügen:  

1. Rechtsklick auf **XYZ Tiles** → **Neue Verbindung hinzufügen**  
2. Quelle hinzufügen:  

   ```
   http://mt1.google.com/vt/lyrs=s&x={x}&y={y}&z={z}
   ```

---

## 3. Bild in den Georeferenzierer laden  

1. Öffne den **Georeferenzierer** über **Layer → Georeferenzierung**.  
2. Klicke auf **Raster öffnen** (Symbol mit dem Bild).  
3. Wähle deine **nicht georeferenzierte Karte** aus (z. B. eine historische Karte als PNG, JPG, TIFF).  

---

## 4. Passpunkte setzen  

### Grundlage für die Georeferenzierung wählen  

- **Option 1**: Eine Basiskarte in QGIS laden (z. B. OpenStreetMap) und manuell Punkte übertragen.  
- **Option 2**: Bekannte Koordinaten von Kartenrändern oder markanten Punkten nutzen.  

### Passpunkte hinzufügen  

1. Klicke auf **GCP-Punkt hinzufügen** (Symbol mit dem roten Kreuz).  
2. Wähle einen **markanten Punkt** in deinem Bild (z. B. eine Straßenkreuzung oder ein Gebäude).  
3. Gib die **bekannten Koordinaten** manuell ein oder wähle sie direkt aus einer Basiskarte:  
   - Klicke auf **Aus Kartenansicht**.  
   - QGIS wechselt automatisch zur Hauptkarte – hier kannst du den Punkt markieren.  
   - Die Koordinaten werden automatisch übernommen.  

**Hinweis:** Wiederhole diesen Schritt für mindestens **4 Passpunkte** (mehr Punkte verbessern die Genauigkeit).  

---

## 5. Transformationseinstellungen wählen  

### Transformationstyp  

Je nach Art der Verzerrung der Karte kann eine geeignete Transformation gewählt werden:  

| **Transformationstyp** | **Beschreibung** | **Anwendungsfälle** |
|------------------------|-----------------|----------------------|
| **Linear (Affine)** | Verschiebt, skaliert, dreht und verzerrt das Bild, während gerade Linien beibehalten werden. Mindestens **3 Punkte** erforderlich. | Wenn die Karte nur geringe Verzerrungen aufweist. |
| **Polynomial 1 (Linear)** | Identisch zur Affinen Transformation. Nutzt eine einfache mathematische Beziehung. **Mindestens 3 Punkte erforderlich.** | Für Karten mit geringen Verzerrungen. |
| **Polynomial 2 (Quadratisch)** | Fügt eine quadratische Krümmung hinzu. **Mindestens 6 Punkte erforderlich.** | Falls die ursprüngliche Karte mäßige Verzerrungen aufweist. |
| **Polynomial 3 (Kubisch)** | Nutzt eine komplexere Berechnung für starke Verzerrungen. **Mindestens 10 Punkte erforderlich.** | Historische Karten mit großen Deformationen. |
| **Thin Plate Spline (TPS)** | Ein elastisches Modell für flexible Verformungen ohne feste mathematische Funktion. **Mindestens 3 Punkte erforderlich.** | Karten mit starken lokalen Verzerrungen (z. B. handgezeichnete Karten). |
| **Projective Transformation** | Erlaubt perspektivische Verzerrungen, um ein Bild an eine flache Ebene anzupassen. **Mindestens 4 Punkte erforderlich.** | Luft- und Satellitenbilder. |
| **Helmert Transformation** | Skalierung, Rotation und Verschiebung ohne Verzerrung. **Mindestens 2 Punkte erforderlich.** | Wenn nur eine Drehung oder Verschiebung nötig ist. |

### Resampling-Methode  

Die Resampling-Methode bestimmt, wie die Pixelwerte interpoliert werden:  

| **Methode** | **Beschreibung** | **Anwendungsfälle** |
|------------|----------------|---------------------|
| **Nächster Nachbar** | Wählt den Wert des nächstgelegenen Pixels. Schnell, aber Treppeneffekte möglich. | Kategorische Daten (z. B. Landnutzungskarten). |
| **Bilineare Interpolation** | Mittelt die Werte der 4 nächsten Pixel für sanfte Übergänge. | Luft- und Satellitenbilder. |
| **Kubische Faltung** | Nutzt 16 benachbarte Pixel für weichere Übergänge (kann leichte Unschärfe erzeugen). | Hochauflösende Rasterbilder. |
| **Kubisch-Spline** | Verwendet eine mathematische Spline-Funktion für besonders weiche Interpolation. | Karten mit gleichmäßigen Übergängen, Höhenmodelle. |
| **Lanczos** | Nutzt ein größeres Pixelumfeld für scharfe, präzise Interpolation. Rechenintensiv. | Hochpräzise Bildverarbeitung, Fernerkundung. |

### Kompressionseinstellungen  

| **Kompressionstyp** | **Beschreibung** | **Anwendungsfälle** |
|---------------------|----------------|---------------------|
| **None (Keine Kompression)** | Speichert Raster ohne Kompression. Maximale Qualität, aber große Datei. | Wenn Speicherplatz keine Rolle spielt. |
| **LZW** | Verlustfreie Kompression, reduziert Dateigröße effizient. | Topografische Karten, DEMs. |
| **PackBits** | Ältere, schnelle verlustfreie Kompression, aber weniger effizient als LZW. | Binäre Raster (z. B. Schwarz-Weiß-Scans). |
| **DEFLATE (Zlib/GZIP)** | Verlustfreie, effektive Kompression mit mehr Rechenaufwand als LZW. | Große GeoTIFF-Dateien mit numerischen Daten. |

Nach der Auswahl der Einstellungen den **Speicherort für die georeferenzierte Karte** auswählen und auf **OK** klicken.  

---

## 6. Georeferenzierung starten  

1. Klicke auf **Starten** (grüner Pfeil).  
2. QGIS verarbeitet das Bild und speichert es als **georeferenziertes Raster**.  
3. Schließe den Georeferenzierer.  

---

## 7. Georeferenzierte Karte in QGIS laden  

1. Gehe zu **Layer → Layer hinzufügen → Rasterebene hinzufügen**.  
2. Wähle die **neu georeferenzierte TIFF-Datei** aus.  
3. Überprüfe, ob die Karte mit anderen Basiskarten übereinstimmt.  

**Tipp:** Falls die Karte nicht exakt passt, überprüfe die **Passpunkte und Transformationseinstellungen**.  

---

## 8. PDF in GeoTIFF umwandeln  

Falls bereits eine **georeferenzierte PDF** existiert, kann sie in ein **GeoTIFF** umgewandelt werden:  

1. Öffne **QGIS**.  
2. Gehe zu **Raster → Umwandlung → Übersetzung (Konvertierung)**.  
3. Wähle die **PDF-Datei** als Eingabe.  
4. Setze das **Ausgabeformat auf GeoTIFF**.  
5. Wähle ein passendes **Koordinatensystem (z. B. EPSG:4326)**.  
6. Klicke auf **OK**, um die PDF in GeoTIFF zu konvertieren.  

Falls das PDF mehrere Layer enthält, kann vor dem Export ein bestimmter Layer ausgewählt werden.  
