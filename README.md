#Tutorial: How to create your own OSM Tiles with OSGEO
The version used in the tuorial was OsGeo 9.0 (Sep. 2015)
##Style (OpenStreetMap-Carto)

<p>In the tutorial we use: 
<a href="https://github.com/gravitystorm/openstreetmap-carto">OpenStreetMap-Carto</a>.</p>

Read through the Readme File on the Project page

##Clone Project and change to the project directory

##Requirements

<code>sudo apt-get install node-carto mapnik-input-plugin-postgis</code>

##Preparation

###Create Database

<code>psql -h localhost -U user</code>

####PSQL Shell

<code>create database gis</code>

<code>\c gis</code>

<code>create extension postgis</code>


###Download OSM Data
<code>wget http://download.geofabrik.de/europe/croatia-latest.osm.pbf</code>

###Import OSM Data
<code>osm2pgsql -H localhost -d gis  -U user croatia-latest.osm.pbf --style openstreetmap-carto.style</code>


###Add username,password and host to the project file

<code>sed -i 's/"dbname": "gis"/"dbname": "gis", "host":"localhost", "user": "user", "password":"user"/g' project.mml
</code>

###Convert Project to mapnik File

<code>carto project.mml > map.xml</code>

###Start Simple Tile Server

<code>/usr/local/bin/liteserv.py map.xml</code> 

Check debug output on server

###Leaflet Map

<code>var map = L.map('map').setView([45.1, 15.2], 10);</code>

<code>L.tileLayer('http://localhost:8000/{z}/{x}/{y}.png', { maxZoom: 18 }).addTo(map);</code>


    
