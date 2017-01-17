#Tutorial: How to create your own OSM Tiles with OSGEO
The version used in the tuorial was OsGeo 9.0 (Sep. 2015)
##Style (OpenStreetMap-Carto)

<p>In the tutorial we use: 
<a href="https://github.com/gravitystorm/openstreetmap-carto">OpenStreetMap-Carto</a>.</p>

Read through the Readme File on the Project page

##Download OSM render project


<code>wget https://github.com/gravitystorm/openstreetmap-carto/archive/v2.45.1.zip</code>

<code>unzip v2.45.1.zip</code>

<code>cd openstreetmap-carto-2.45.1</code>

<code>./get-shapefiles.sh </code>



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

##Tile Server
<code>git clone https://github.com/springmeyer/tilelite.git</code>
<code>cd tilelite/</code>
<code>sudo python setup.py install</code>

###Start Simple Tile Server

<code>/usr/local/bin/liteserv.py map.xml</code> 

Check debug output on server

####Store generated tiles on Server (Optional)

<code>mkdir ~/cache</code>

<code>/usr/local/bin/liteserv.py -c --cache-path=~/cache map.xml</code> 



##Leaflet Map

http://leafletjs.com/examples/quick-start-example.html

###Adopt Leaflet Example

<code>var map = L.map('map').setView([45.1, 15.2], 10);</code>

<code>L.tileLayer('http://localhost:8000/{z}/{x}/{y}.png', { maxZoom: 18 }).addTo(map);</code>


    
