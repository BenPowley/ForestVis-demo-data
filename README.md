# ForestVis demo data: Lower Teakettle (NEON TEAK)

Prebaked data for the ForestVis static demo. The demo's GitHub Pages workflow
copies this repository into the site's `data/` folder at build time.

A 300 × 300 m crop centred on the TEAK tower (UTM 11N, EPSG:32611,
x 321366–321666, y 4097250–4097550), split into three 100 m wide areas
(West, Centre, East).

| File | Contents |
|---|---|
| `aoi-config.json` | App configuration: CRS, file paths, area names |
| `teak/teak.copc.laz` | 1.96 M points; `PredInstance`, `PredSemantic`, per-point NDVI/GNDVI/LCI/NDRE/OSAVI, per-tree `Avg*` and `Height` |
| `teak/tree_centroids_umap.geojson` | 3456 trees with crown index statistics and UMAP coordinates |
| `teak/tree_centroids_umap_metadata.json` | UMAP inputs and parameters |
| `teak/region_statistics.geojson`, `teak/region_{0,1,2}.geojson` | Area outlines and per-area means |
| `teak/instance-z-filter.tif` | `PredInstance` of the highest point per 0.1 m cell |
| `teak/ndvi.tif` | 1 m NDVI |
| `teak/aerial.tif` | 10 cm RGB orthophoto |
| `teak/color_categorization.qml` | Instance colour palette |

## Sources and processing

- NEON AOP, TEAK, July 2023:
  - Discrete return LiDAR point cloud, DP1.30003.001, RELEASE-2026, https://doi.org/10.48443/5ts2-rc92
  - High-resolution orthorectified camera imagery mosaic, DP3.30010.001, RELEASE-2026, https://doi.org/10.48443/8vq2-s021
  - Spectrometer bidirectional surface reflectance mosaic, DP3.30006.002, provisional
- Noise classes 7 and 18 and points outside −3 to 75 m above ground removed.
- Tree instances from SegmentAnyTree (Wielgosz et al. 2024); instances under
  50 points or 3 m tall are not trees (`PredInstance` 0).
- Indices from the reflectance mosaic using green 560, red 670, red edge 715
  and NIR 840 nm (each averaged with its neighbouring bands); pixels with NIR
  below 3 % or visible/red-edge below 0.5 % are nodata. OSAVI uses the 1.16
  factor (Rondeaux et al. 1996).

The pipeline scripts are in the code repository under `pipeline/teak/`.

## Licence

Derived from NEON data, released under CC BY 4.0. Credit: National Ecological
Observatory Network (NEON), operated by Battelle and sponsored by the National
Science Foundation.
