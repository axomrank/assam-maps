# 🗺️ Assam Geospatial Map Data Hub (`Assam_MAP_file`)

High-precision GeoJSON, KML, and administrative geospatial boundary datasets for the State of **Assam, India**.

This repository contains cleaned, validated territorial vectors covering state, district, sub-district, revenue circle, village, assembly constituency, parliamentary constituency, headquarters, and infrastructure layers (railways, energy facilities).

---

## 📂 Repository Contents & Layer Index

| Filename | Format | Description | Features / Resolution |
| :--- | :---: | :--- | :--- |
| **`Assam_districts.geojson`** | GeoJSON | **Updated 35-District Boundary Map** (Includes newly created districts: **Bajali** and **Tamulpur**) | 35 Districts |
| **`NEW_Assam_districts.kml`** | KML | Google Earth & GIS compatible 35-district boundary overlay (Includes Bajali & Tamulpur) | 35 Districts |
| **`ASSAM_DISTRICTS.geojson`** | GeoJSON | Baseline administrative district boundaries with Census 2011 & LGD codes | 33 Districts |
| **`ASSAM_SUBDISTRICTS.geojson`** | GeoJSON | Sub-districts / Tehsils / Revenue Circles administrative boundaries | 154 Sub-districts |
| **`ASSAM_VILLAGES.geojson`** | GeoJSON | Granular village-level cadastral and revenue village polygon boundaries | 26,000+ Villages |
| **`ASSAM_STATE.geojson`** | GeoJSON | Complete outer territorial polygon boundary of the State of Assam | 1 State Polygon |
| **`ASSAM_ASSEMBLY.geojson`** | GeoJSON | Assam Legislative Assembly (Vidhan Sabha) constituency boundaries | 126 AC Boundaries |
| **`ASSAM_parliament.geojson`** | GeoJSON | Lok Sabha Parliamentary Constituency boundaries for Assam | 14 PC Boundaries |
| **`ASSAM District Hq.geojson`** | GeoJSON | Point coordinates and metadata for District Headquarters across Assam | 33+ District HQs |
| **`ASSAM Sub District Hq.geojson`**| GeoJSON | Point coordinates and metadata for Sub-District / Circle Headquarters | 150+ Sub-district HQs |
| **`ASSAM_RAILWAYS.geojson`** | GeoJSON | Railway network track vectors spanning Assam (Northeast Frontier Railway) | 747 Railway Segments |
| **`ASSAM_ENERGY_PLANTS.geojson`** | GeoJSON | Thermal, hydro, and gas power plant installations with generation capacity data | 8 Major Plants |

---

## 🌟 Key Updates: Bajali & Tamulpur Districts

The primary updated district dataset [`Assam_districts.geojson`](Assam_districts.geojson) and Google Earth KML layer [`NEW_Assam_districts.kml`](NEW_Assam_districts.kml) incorporate Assam's updated administrative reorganization, including:
1. **Bajali District** (carved out from Barpeta)
2. **Tamulpur District** (carved out from Baksa / BTR)

### 35 Administrative Districts Included:
* Bajali, Baksa, Barpeta, Biswanath, Bongaigaon, Cachar, Charaideo, Chirang, Darrang, Dhemaji, Dhubri, Dibrugarh, Dima Hasao, Goalpara, Golaghat, Hailakandi, Hojai, Jorhat, Kamrup, Kamrup Metropolitan, Karbi Anglong, Karimganj, Kokrajhar, Lakhimpur, Majuli, Morigaon, Nagaon, Nalbari, Sivasagar, Sonitpur, South Salmara-Mankachar, Tamulpur, Tinsukia, Udalguri, West Karbi Anglong.

---

## 🛠️ Usage & Integration

### Web Mapping (Leaflet / Mapbox / OpenLayers)
```javascript
fetch('Assam_districts.geojson')
  .then(res => res.json())
  .then(data => {
    L.geoJSON(data, {
      style: {
        color: '#d97706',
        weight: 2,
        fillOpacity: 0.15
      },
      onEachFeature: (feature, layer) => {
        layer.bindPopup(`<strong>${feature.properties.name}</strong>`);
      }
    }).addTo(map);
  });
```

### Python (GeoPandas / Shapely)
```python
import geopandas as gpd

# Load 35-district boundary
districts = gpd.read_file('Assam_districts.geojson')
print(districts[['name', 'geometry']].head())

# Load village-level polygons
villages = gpd.read_file('ASSAM_VILLAGES.geojson')
print(f"Total villages: {len(villages)}")
```

### QGIS / ArcGIS / Google Earth
- Load `.geojson` directly via **Layer -> Add Layer -> Add Vector Layer**.
- Load `NEW_Assam_districts.kml` into **Google Earth Pro** or Google Earth Web for 3D terrain and satellite boundary inspection.
