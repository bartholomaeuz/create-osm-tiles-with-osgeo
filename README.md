#Tutorial: How to create your own OSM Tiles with OSGEO
The version used in the tuorial was OsGeo 9.0 (Sep. 2015)
##Style






##Requirements

<code>sudo apt-get install node-carto mapnik-input-plugin-postgis</code>

Insert host,user,password in config file
<code>sed -i 's/"dbname": "gis"/"dbname": "gis", "host":"localhost", "user": "user", "password":"user"/g' project.mml
</code>

test1

<code>carto project.mml > map.xml</code>
tess2

<code>/usr/local/bin/liteserv.py map.xml</code> 
    
