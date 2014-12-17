LA Buildings
===========

Los Angeles County building import

Generates an OSM file of buildings with addresses per census block groups,
ready to be used in JOSM for a manual review and upload to OpenStreetMap. This repository is based heavily on the [NYC building import](https://github.com/osmlab/nycbuildings)

This README is about data conversion. See also the [page on the OSM wiki](https://wiki.openstreetmap.org/wiki/Los_angeles,_California/Buildings_Import).


![LA buildings screenshot](la_buildings_screenshot.png?raw=true "LA buildings screenshot from QGIS")

Browse a slippy map of the data [here](https://api.tiles.mapbox.com/v3/stamen.labuildings/page.html#17/33.99024/-118.46586)


## Prerequisites

    Python 2.7.x
    pip
    virtualenv
    libxml2
    libxslt
    spatialindex
    GDAL

### Installing prerequisites on Mac OSX

    # install brew http://brew.sh

    brew install libxml2
    brew install libxslt
    brew install spatialindex
    brew install gdal

### Installing prerequisites on Ubuntu

    apt-get install python-pip
    apt-get install python-virtualenv
    apt-get install gdal-bin
    apt-get install libgdal-dev
    apt-get install libxml2-dev
    apt-get install libxslt-dev
    apt-get install python-lxml
    apt-get install python-dev
    apt-get install libspatialindex-dev
    apt-get install unzip

## Set up Python virtualenv and get dependencies
    # may need to easy_install pip and pip install virtualenv
    virtualenv ~/venvs/labuildings
    source ~/venvs/labuildings/bin/activate
    pip install -r requirements.txt


## Usage

Run all stages:

    # Download all files and process them into a building
    # and an address .osm file per district.
    make

You can run stages separately, like so:

    # Download and expand all files, reproject
    make download

    # Chunk address and building files by census block group
    # (this will take a long time)
    make chunks

    # Generate importable .osm files.
    # This will populate the osm/ directory with one .osm file per
    # census block group.
    make osm

    # Clean up all intermediary files:
    make clean

    # For testing it's useful to convert just a single district.
    # For instance, convert block group 060372735024:
    make chunks # will take a while
    python merge.py 060372735024 # Should be fast
    python convert.py merged/buildings-addresses-060372735024.geojson # Fast


## Features

- Conflates buildings and addresses
- Cleans address names
- Exports one OSM XML building file per LA county block group
- Exports OSM XML address files for addresses that pertain to buildings with
  more than one address
- Handles multipolygons
- Simplifies building shapes

## Attribute mapping

TBD.
