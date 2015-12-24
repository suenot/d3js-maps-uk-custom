http://www.nytimes.com/interactive/2013/04/08/business/global/asia-map.html
http://bl.ocks.org/mbostock/99049112373e12709381
http://bl.ocks.org/mbostock/99049112373e12709381
http://bl.ocks.org/mbostock/99049112373e12709381
http://bl.ocks.org/mbostock/99049112373e12709381
http://bl.ocks.org/mbostock/1d127e44b53a3cbebe7b
http://bl.ocks.org/mbostock/20789c8df83e04e49684
http://mbostock.github.io/protovis/ex/
http://mbostock.github.io/protovis/ex/
http://mbostock.github.io/protovis/ex/
http://mbostock.github.io/protovis/ex/dymax.html
https://www.jasondavies.com/maps/countries-by-area
https://www.jasondavies.com/maps/countries-by-area
http://bl.ocks.org/SLR436/5693283
http://bl.ocks.org/quantviews/raw/ed7a710a4e81cf7a910e/
http://bl.ocks.org/mbostock/899711
http://bost.ocks.org/mike/example/

# Create topojsons
ogr2ogr \
  -f GeoJSON \
  -where "ADM0_A3 IN ('GBR', 'IRL')" \
  map.json \
  ne_10m_admin_0_map_units.shp
ogr2ogr \
  -f GeoJSON \
  -where "ADM0_A3  IN  ('GBR') AND scalerank = 8" \
  states.json \
  ne_10m_admin_1_states_provinces_lines.shp
ogr2ogr \
  -f GeoJSON \
  -where "ADM0_A3  IN  ('GBR') AND scalerank < 8" \
  places.json \
  ne_10m_populated_places.shp

# Merge topojsons in one
topojson \
  -o uk.json \
  --id-property SU_A3 \
  --properties name=NAME \
  -- \
  map.json \
  states.json \
  places.json
