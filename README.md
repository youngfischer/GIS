# Advanced Satellite Image GIS Analysis Project

## Overview
This project provides a comprehensive framework for downloading, processing, and analyzing satellite imagery using the Google Earth Engine API and other GIS tools. It includes functionality for spatial data analysis, geographic feature extraction, climate data integration, change detection using historical imagery, and machine learning-based projections.

## Features
- Satellite imagery acquisition through Earth Engine API
- NDVI (Normalized Difference Vegetation Index) calculation
- Elevation and terrain analysis
- Land cover classification and statistics
- Population density mapping and analysis
- Multi-temporal change detection
- Hydrological analysis
- Socioeconomic data integration
- Future land use projections with machine learning
- Interactive map generation
- Export to standard GIS formats

## Installation

### Prerequisites
- Python 3.7+
- Google Earth Engine account with authentication

### Required Packages
```bash
pip install earthengine-api geopandas rasterio numpy matplotlib scikit-learn tensorflow pyproj folium shapely xarray netCDF4 pandas seaborn scipy requests fiona
```

### Google Earth Engine Authentication
Before using the script, authenticate with Earth Engine:
```bash
earthengine authenticate
```

## Usage

### Basic Example
```python
from satellite_gis_project import SatelliteGISProject

# Define your region of interest (longitude, latitude coordinates)
coordinates = [
    (-122.45, 37.75),  # Format: (longitude, latitude)
    (-122.42, 37.75),
    (-122.42, 37.78),
    (-122.45, 37.78),
    (-122.45, 37.75)
]

# Initialize the project
project = SatelliteGISProject(
    region_name="SanFrancisco",
    coordinates=coordinates,
    start_year=2015,
    end_year=2023
)

# Download satellite imagery
project.download_satellite_imagery()

# Calculate NDVI
project.calculate_ndvi()

# Get elevation data
project.get_elevation_data()

# Get land cover data
project.get_land_cover()

# Get population data
project.get_population_data()

# Perform spatial analysis
results = project.spatial_analysis()

# Create an interactive map
interactive_map = project.create_interactive_map()

# Create future projection
projection = project.create_future_projection(years=10)
```

## Class Documentation

### SatelliteGISProject

#### Initialization Parameters
- `region_name` (str): Name of the region for reference
- `coordinates` (list of tuples): List of (longitude, latitude) coordinates defining the region boundary
- `time_period` (int, optional): Number of months to look back for recent imagery. Default: 6
- `start_year` (int, optional): Start year for historical analysis. Default: 2015
- `end_year` (int, optional): End year for historical analysis. Default: 2023

#### Methods

##### `download_satellite_imagery`
Downloads satellite imagery from Google Earth Engine.

Parameters:
- `collection` (str, optional): Earth Engine collection ID. Default: "LANDSAT/LC08/C02/T1_TOA"
- `start_date` (str, optional): Start date in 'YYYY-MM-DD' format. Default: None (uses time_period)
- `end_date` (str, optional): End date in 'YYYY-MM-DD' format. Default: None (uses current date)
- `max_cloud_cover` (int, optional): Maximum cloud cover percentage. Default: 20
- `save_geotiff` (bool, optional): Whether to export as GeoTIFF. Default: True

##### `calculate_ndvi`
Calculates NDVI (Normalized Difference Vegetation Index) from satellite image.

Parameters:
- `save_geotiff` (bool, optional): Whether to export as GeoTIFF. Default: True

##### `get_elevation_data`
Gets elevation data from SRTM dataset on Earth Engine.

Parameters:
- `save_geotiff` (bool, optional): Whether to export as GeoTIFF. Default: True

##### `get_land_cover`
Gets land cover data from the ESA WorldCover dataset.

Parameters:
- `year` (int, optional): Year for land cover data. Default: 2020
- `save_geotiff` (bool, optional): Whether to export as GeoTIFF. Default: True

##### `get_population_data`
Gets population density data from WorldPop dataset.

Parameters:
- `year` (int, optional): Year for population data. Default: 2020
- `save_geotiff` (bool, optional): Whether to export as GeoTIFF. Default: True

##### `spatial_analysis`
Performs spatial analysis on the collected data.

Returns:
- Dictionary of analysis results

##### `create_interactive_map`
Creates an interactive map using Folium.

Returns:
- Folium map object

##### `create_future_projection`
Creates a simplified land use projection model based on collected data.

Parameters:
- `years` (int, optional): Number of years to project into the future. Default: 10

Returns:
- Dictionary of projection results

## Output Files
The project creates a directory named `{region_name}_GIS_Analysis` containing:
- Satellite imagery (PNG and GeoTIFF)
- NDVI maps (PNG and GeoTIFF)
- Elevation maps (PNG and GeoTIFF)
- Land cover maps (PNG and GeoTIFF)
- Population density maps (PNG and GeoTIFF)
- Land cover statistics (CSV)
- Interactive map (HTML)
- Future projections and visualizations

## Working with Earth Engine Tasks
GeoTIFF exports are initiated as Earth Engine tasks, which run in the background. These tasks will export files to your Google Drive. You can check the status of these tasks in the Earth Engine Code Editor (https://code.earthengine.google.com/).

## Advanced Usage

### Custom Time Series Analysis
```python
# Download historical imagery for time series analysis
project.download_satellite_imagery(
    start_date="2015-01-01",
    end_date="2015-12-31"
)

# Compare with current imagery to detect changes
project.download_satellite_imagery(
    start_date="2023-01-01",
    end_date="2023-12-31"
)
```

### Integration with Local GIS Software
All GeoTIFF outputs are compatible with common GIS software like QGIS and ArcGIS. The interactive map can be viewed in any web browser.

## Limitations and Considerations
- Earth Engine API has usage quotas that may limit large-scale analysis
- Export tasks for large areas may take significant time to complete
- Complex operations on very large datasets may require cloud computing resources
- Some datasets may have licensing restrictions for commercial use

## Contributing
Contributions to improve this project are welcome. Please feel free to submit a pull request or open an issue on the project's GitHub page.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments
- Google Earth Engine for providing access to satellite data
- ESA WorldCover for land cover data
- WorldPop for population data
- USGS for SRTM elevation data
