# leaflet-elevation.js

[![NPM version](https://img.shields.io/npm/v/@raruto/leaflet-elevation.svg?color=red)](https://www.npmjs.com/package/@raruto/leaflet-elevation)
[![License](https://img.shields.io/badge/license-GPL%203-blue.svg?style=flat)](LICENSE)

A Leaflet plugin that allows to add elevation profiles using d3js

<p align="center">
    <a href="https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_hoverable-tracks.html"><img src="https://raruto.github.io/img/leaflet-elevation.png" alt="Leaflet elevation viewer" /></a>
</p>

---

_For a working example see one of the following demos:_

- [loading .gpx file](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation.html)
- [loading .geojson file](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_geojson-data.html)
- [loading .kml file](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_kml-data.html)
- [loading .tcx file](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_tcx-data.html)
- [loading a local .gpx file](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_upload-gpx.html)
- [loading data from a textarea](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_string-data.html)
- [loading individual .geojson tracks](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_geojson-group.html)
- [loading individual .gpx tracks](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_toggable-tracks.html)
- [loading multiple .gpx tracks (hover to toggle)](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_hoverable-tracks.html)
- [loading multiple .gpx tracks (click to toggle)](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_toggable-charts.html)
- [translating plugin labels](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_i18n-strings.html)
- [using custom colors](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_custom-theme.html)
- [using .gpx extensions (cadence + heart)](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_extended-ui.html)
- [using .gpx waypoint icons](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_gpx-waypoints.html)
- [using .geojson waypoint icons](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_geojson-waypoints.html)


<br/>

- [autohide map](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_hidden-map.html)
- [autohide chart](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_hidden-chart.html)
- [collapsible button](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_close-button.html)
- [custom summary](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_custom-summary.html)
- [follow marker](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_follow-marker.html)
- [layer almostover](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_almost-over.html)
- [slope chart](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_slope-chart.html)
- [speed chart](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_speed-chart.html)
- [walking marker](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_dynamic-runner.html)

---

<blockquote>
    <p align="center">
        <em>Initially based on the <a href="http://mrmufflon.github.io/Leaflet.Elevation/">work</a> of <strong>Felix “MrMufflon” Bache</strong></em>
    </p>
</blockquote>

---

## How to use

1. **include CSS & JavaScript**
    ```html
    <head>
    ...
    <style> html, body, #map, #elevation-div { height: 100%; width: 100%; padding: 0; margin: 0; } #map { height: 75%; } #elevation-div {	height: 25%; font: 12px/1.5 "Helvetica Neue", Arial, Helvetica, sans-serif; } </style>

    <!-- leaflet-ui -->
    <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"></script>
    <script src="https://unpkg.com/leaflet-ui@0.5.4/dist/leaflet-ui.js"></script>

    <!-- leaflet-elevation -->
    <link rel="stylesheet" href="https://unpkg.com/@raruto/leaflet-elevation/dist/leaflet-elevation.css" />
    <script src="https://unpkg.com/@raruto/leaflet-elevation/dist/leaflet-elevation.js"></script>
    ...
    </head>
    ```
2. **choose the div container used for the slippy map**
    ```html
    <body>
    ...
    <div id="map"></div>
    ...
    </body>
    ```
3. **create your first simple “leaflet-elevation” slippy map**
    ```html
    <script>
      // Full list options at "leaflet-elevation.js"
      var elevation_options = {

        // Default chart colors: theme lime-theme, magenta-theme, ...
        theme: "lightblue-theme",

        // Chart container outside/inside map container
        detached: true,

        // if (detached), the elevation chart container
        elevationDiv: "#elevation-div",

        // if (!detached) autohide chart profile on chart mouseleave
        autohide: false,

        // if (!detached) initial state of chart profile control
        collapsed: false,

        // if (!detached) control position on one of map corners
        position: "topright",

        // Autoupdate map center on chart mouseover.
        followMarker: true,

        // Autoupdate map bounds on chart update.
        autofitBounds: true,

        // Chart distance/elevation units.
        imperial: false,

        // [Lat, Long] vs [Long, Lat] points. (leaflet default: [Lat, Long])
        reverseCoords: false,

        // Acceleration chart profile: true || "summary" || "disabled" || false
        acceleration: false,

        // Slope chart profile: true || "summary" || "disabled" || false
        slope: false,

        // Speed chart profile: true || "summary" || "disabled" || false
        speed: false,

        // Display time info: true || "summary" || false
        time: false,

        // Display distance info: true || "summary"
        distance: true,

        // Display altitude info: true || "summary"
        altitude: true,

        // Summary track info style: "inline" || "multiline" || false
        summary: 'multiline',

        // Download link: "link" || false || "modal"
        downloadLink: 'link',

        // Toggle chart ruler filter
        ruler: true,

        // Toggle chart legend filter
        legend: true,

        // Toggle "leaflet-almostover" integration
        almostOver: true,

        // Toggle "leaflet-distance-markers" integration
        distanceMarkers: false,

        // Display track datetimes: true || false
        timestamps: false,

        // Display track waypoints: true || "markers" || "dots" || false
        waypoints: true,

        // Toggle custom waypoint icons: true || { associative array of <sym> tags } || false
        wptIcons: {
          '': L.divIcon({
            className: 'elevation-waypoint-marker',
            html: '<i class="elevation-waypoint-icon"></i>',
            iconSize: [30, 30],
            iconAnchor: [8, 30],
          }),
        },

        // Toggle waypoint labels: true || "markers" || "dots" || false
        wptLabels: true,

        // Render chart profiles as Canvas or SVG Paths
        preferCanvas: true,

      };

      // Instantiate map (leaflet-ui).
      var map = L.map('map', { mapTypeId: 'terrain', center: [41.4583, 12.7059], zoom: 5 });

      // Instantiate elevation control.
      var controlElevation = L.control.elevation(elevation_options).addTo(map);

      // Load track from url (allowed data types: "*.geojson", "*.gpx", "*.tcx")
      controlElevation.load("https://raruto.github.io/leaflet-elevation/examples/via-emilia.gpx");

    </script>
    ```

### Build Guide

For those wishing to try cloning this repository into a local development folder (eg. /var/www):

```shell
git clone git@github.com:Raruto/leaflet-elevation.git
cd ./leaflet-elevation

npm i         # install dependencies
npm run dev   # auto-generate "dist" files
```

After that you can start developing inside the `src` and `test` folders (eg. open "http://localhost/leaflet-elevation/test" in your browser to preview changes). Check also [CONTRIBUTING.md](.github/CONTRIBUTING.md) file for some information about it.

### FAQ

<details>
  <summary>1. How can I change the color of the elevation plot?</summary><br>

There are multiple options to achieve this:

* You could either use some default presets (see: theme: "lightblue-theme" option in readme file and the following file `leaflet-elevation.css` for some other default "*-theme" names).
* check out [this example](https://raruto.github.io/leaflet-elevation/examples/leaflet-elevation_custom-theme.html)
* Or add the following lines for custom colors.
```css
.elevation-control .area {
    fill: red;
}
.elevation-control .background {
    background-color: white;
```
</details>

<details>
  <summary>2. How to enable/disable the leaflet user interface customizations?</summary><br>

These customizations are actually part of the [leaflet-ui](https://github.com/Raruto/leaflet-ui) and can be toggled on/off using e.g. the following options:
```js
var map = L.map('map', {
    center: [41.4583, 12.7059],  // needs value to initialize
    zoom: 5,                     // needs value to initialize
    mapTypeId: 'topo',
    mapTypeIds: ['osm', 'terrain', 'satellite', 'topo'],
    gestureHandling: false,     // zoom with Cmd + Scroll
    zoomControl: true,          // plus minus buttons
    pegmanControl: false,
    locateControl: false,
    fullscreenControl: true,
    layersControl: true,
    minimapControl: false,
    editInOSMControl: false,
    loadingControl: false,
    searchControl: false,
    disableDefaultUI: false,
    printControl: false,
});
```
</details>

<details>
  <summary>3. Some real world projects based on this plugin?</summary><br>

- https://parcours.scasb.org/
- https://velocat.ru/velo/phpBB3/map.php
- https://plugins.qgis.org/plugins/track_profile_2_web/
- https://wordpress.org/plugins/os-datahub-maps/
- https://wordpress.org/plugins/extensions-leaflet-map/
- https://github.com/der-stefan/OpenTopoMap
- https://gpx.n-peloton.fr/
- https://walkaholic.me/map

</details>

_Related: [Leaflet-UI presets](https://github.com/raruto/leaflet-ui), [QGIS Integration](https://github.com/faunalia/trackprofile2web)_

### Changelog

All notable changes to this project are documented in the [releases](https://github.com/Raruto/leaflet-elevation/releases) page.

---

**Compatibile with:**
[![Leaflet 1.x compatible!](https://img.shields.io/badge/Leaflet-1.7.0-1EB300.svg?style=flat)](http://leafletjs.com/reference.html)
[![d3.js v6 compatibile!](https://img.shields.io/badge/d3.js-6.5-1EB300.svg?style=flat)](https://www.npmjs.com/package/d3)
[![@tmcw/togeojson v4.6.0 compatibile!](https://img.shields.io/badge/@tmcw/togeojson-4.6-1EB300.svg?style=flat)](https://www.npmjs.com/package/@tmcw/togeojson)


---

**Contributors:** [MrMufflon](https://github.com/MrMufflon/Leaflet.Elevation), [HostedDinner](https://github.com/HostedDinner/Leaflet.Elevation), [ADoroszlai](http://ADoroszlai.github.io/joebed/), [Raruto](https://github.com/Raruto/leaflet-elevation)

---

**License:** GPL-3.0+
