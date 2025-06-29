# Smart-Survey-Drawing-Tool
Smart Survey Drawing Tool

Project Context

In many land surveying projects, engineers face challenges in drawing and analyzing large areas accurately, especially when using heavy software like AutoCAD. This tool was created to solve these issues and save significant time and effort by automating the drawing process using AI and DXF file generation.

Key Strengths of the Tool

Operates independently of AutoCAD, compatible with any environment.

Automatically generates structured DXF files with organized layers.

Comprehensive analysis of map elements (buildings, roads, green areas) within a polygon.

Supports export to Excel and GIS-ready formats.

Accepts real GPS data from surveying devices.

Intuitive and flexible graphical user interface.

Supports internal holes in buildings and green areas.

High-speed analysis and export functionality.

Introduction

Traditional Surveying Challenges:

Manual Labor: Manually collecting points and drawing in AutoCAD is time-consuming and error-prone.

Complex Area Handling: Difficult to analyze and draw complex sites (courtyards, mixed-use zones, greenery).

Redundant Work: Any update or re-survey requires manual rework.

Hole Representation: Drawing buildings with internal holes (e.g., courtyards) in AutoCAD requires advanced tools and experience.

Data Exporting: Converting data from GPS or OSM sources to DXF/Excel is often indirect and complex.

How the Tool Solves These Problems

User-Friendly Interface: Allows users to define elements (buildings, roads, greenery) and input points manually or via map.

OSM Integration: Automatically fetches data from OpenStreetMap (buildings, roads, green areas).

Direct DXF Export: Elements are drawn and exported as DXF files instantly.

Automatic Area Calculation: Each feature's area is calculated and displayed.

Hole Support: Accurately draws inner holes as separate polylines in distinct layers.

Excel Export: All data is saved in organized Excel files.

AI Assistance (Optional): Classifies points and assists in mapping tasks.

Main Components

1. smart_survey_gui.py

Manages user interaction and graphical interface.

Allows element selection, point input, DXF file creation, and operation logs.

2. dxf_generator.py

Generates DXF files for all elements.

Draws closed polylines for outer and inner boundaries.

Adds area text labels in appropriate positions.

3. full_area_analyzer.py

Analyzes a full polygon area.

Pulls OSM data for buildings, roads, greenery.

Calculates exact surface areas.

4. autocad_controller.py

(Legacy) Uses AutoCAD COM to draw directly into AutoCAD.

Supports region creation with holes.

No longer used by default (DXF method preferred).

5. smart_map_module.py

Manages map view with PyQt/Leaflet.

Accepts user-defined or OSM-derived coordinates.

Handles coordinate system conversions.

6. smart_street_analyzer.py

Extracts road data from OSM.

Analyzes road centerlines and classifications.

7. excel_exporter.py

Exports all data to well-structured Excel files.

Automatically calculates and records areas.

8. ai_point_classifier.py

AI-powered classifier to detect and categorize survey points.

9. AI Assistant Module

Provides a chatbot interface integrated with Google Gemini.

Users can ask surveying questions and receive accurate educational responses.

Supports Arabic, includes a detailed chat log UI.

Requires API key and google-generativeai package.

Built-In AI Logic

Uses OSMNX to fetch map data and filters elements by type (building, road, green area). Each feature is converted to a polygon and exported to DXF with proper layer assignment and styling.

What is COM?

COM (Component Object Model): A Microsoft technology allowing external software like Python to control applications like AutoCAD.

Initially used in this tool, but replaced with DXF export due to instability.

What is OSM?

OSM (OpenStreetMap): An open-source mapping project providing free geographic data.

This tool uses OSM to retrieve geographic features based on selected regions.

Core Files Overview

smart_survey_gui.py: Main interface and logic controller.

dxf_generator.py: DXF creation and export.

full_area_analyzer.py: Full area processing and OSM integration.

autocad_controller.py: AutoCAD COM operations (legacy).

smart_map_module.py: Map interface and coordination.

smart_street_analyzer.py: Road data extraction.

excel_exporter.py: Excel data generation.

ai_point_classifier.py: AI-based classification.

neon_tech_fusion_ui.py: Additional UI module.

smart_fence_analyzer.py: Wall detection and analysis.

Usage Guide

Run smart_survey_gui.py.

Select element type (building, road, green area, etc.).

Enter points manually or fetch from OSM.

Choose or create DXF file.

Click confirm to export to DXF and Excel.

Open the DXF in AutoCAD to review and print.

Real Use Cases

Analyzing entire Nasr City in under 3 minutes.

Mapping zones from Tanta to Cairo to Sohag in less than 5 minutes.

Converting raw GPS files from Total Station devices into ready-to-draw formats.

Design Philosophy

The tool moved away from COM-based AutoCAD integration due to its complexity and reliance on local installations. Instead, it adopted direct DXF generation using ezdxf, making the tool faster, more portable, and universally compatible.

Requirements

Python 3.8+

Required packages: ezdxf, osmnx, geopandas, shapely, pyproj, pandas, openpyxl, etc. (see requirements_full.txt)

AutoCAD (optional, for viewing DXF files only)

Technical Notes & DXF Limitations

DXF standard does not directly support holes inside polylines; holes must be represented as separate closed polylines.

For true holes in AutoCAD, convert closed polylines to REGIONS and subtract.

This tool visually distinguishes holes using color and layer separation.

General Notes

Codebase is modular and scalable.

Each module is documented and easily extendable.

Supports both manual and automated workflows.

Can be integrated with additional geospatial data sources.

New Features & Updates (2025)

Date: 26/06/2025

1. DXF to GIS (GeoJSON/Shapefile) Conversion

New feature to convert DXF files to standard GIS formats.

Supports both combined and layer-specific export.

User can choose projection system:

UTM Zone 36N (EPSG:32636) for local precision

Latitude/Longitude (EPSG:4326) for web visualization

2. Auto Layer Detection

Automatically detects and processes common layer names:

SMART_BUILDING, SMART_ROAD, SMART_GREEN, SMART_WALL, BUILDING_HOLES

Alternate names like Smart_Street, Green_Area_Layer, Fence_Layer

3. Modern UI for Conversion

New UI for GIS export.

Success/failure messages included for user clarity.

4. Code Architecture Retained

No original structure was modified.

New features added without disrupting old workflows.

5. Additional Dependencies

GIS conversion requires: ezdxf, geopandas, shapely, fiona

Geographic Area Selection Tips

When using AI/OSM tools for analysis:

Choose reasonably sized areas (districts or neighborhoods).

Larger areas = more features = slower processing and higher memory usage.

Real Example:

Area similar to New York City (6-point polygon):

~199,759 buildings

~179,198 roads

~11,226 green spaces

Processing took minutes and required high memory

Warning:

Avoid extremely large areas (multi-city/province): may cause memory issues.

Start small, test performance, then scale up.

Pro Tip

If memory usage is high, reduce area size or process in smaller batches.

The tool supports any size, but performance depends on map complexity.
