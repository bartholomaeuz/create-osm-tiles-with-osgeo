#Tutorial: How to create your own OSM Tiles with OSGEO
The version used in the tuorial was OsGeo 9.0 (Sep. 2015)
##Style (OpenStreetMap-Carto)

<p>In the tutorial we use: 
<a href="https://github.com/gravitystorm/openstreetmap-carto">OpenStreetMap-Carto</a>.</p>

Read through the Readme File on the Project page



##Requirements

<code>sudo apt-get install node-carto mapnik-input-plugin-postgis</code>

##Preparation

###Create Database

<code>psql -h localhost -U user</code>

####PSQL Shell

<code>create database gis</code>

<code>\c gis</code>

<code>create extension postgis</code>



###Add username,password and host to the project file

<code>sed -i 's/"dbname": "gis"/"dbname": "gis", "host":"localhost", "user": "user", "password":"user"/g' project.mml
</code>

###Convert Project to mapnik File

<code>carto project.mml > map.xml</code>

###Start Simple Tile Server

<code>/usr/local/bin/liteserv.py map.xml</code> 
    
