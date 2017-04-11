# Clockwise.MD Embedded Map

## A Quick Note

This is a patient facing map that is meant to be added to your clinic or hospital's public
facing website. It does not in any way affect functionality of the application.

---

## Demonstration

[Click here to see the widget in action](http://lightshedhealth.github.io/Embedded-Map-API/)

---

## Beginner's Guide

This first snippet of code loads the dependencies for the maps and styles. It should go inside the
`<head>` tag of your web page. You want to change __REPLACEME__ with your group's id number where noted.

```html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="//s3-us-west-1.amazonaws.com/clockwisepublic/mustache.js"></script>
<script src="//cdn.pubnub.com/pubnub.min.js" type="text/javascript"></script>
<script src="//maps.googleapis.com/maps/api/js" type="text/javascript"></script>
<script src="//s3-us-west-1.amazonaws.com/clockwisepublic/geoposition.js"></script>
<script src="//s3-us-west-1.amazonaws.com/clockwisepublic/infobox.js"></script>
<script src="//www.clockwisemd.com/groups/REPLACEME.js" type="text/javascript"></script>
<link href="//fonts.googleapis.com/css?family=Open+Sans:300italic,400italic,600italic,300,400,600" media="screen" rel="stylesheet" />
<link href="//s3-us-west-1.amazonaws.com/clockwisepublic/clockwise_map.css" media="all" rel="stylesheet" />

<style>
  .row-fluid_maps { height:300px; }
  #group-hospital-list .margin-group { margin-left: 0; }
</style>
```

---

This next snippet of code will render a map on your webpage with a search bar for patients to enter
their location. This can be placed anywhere within the `<body>` tag on your web page.

```html
<div class="groups-map" id="map-panel">
  <div class="address-box" id="panel">
    <div class="row-fluid" style="display:flex;flex-direction:row;">
      <input style="flex-grow:10;height:5%;" id="address" placeholder="Current Address" type="text" value="" />
      <input style="flex-grow:1;" class="btn btn-primary" id="address-search-btn" onclick="codeAddress()" type="button" value="Search Nearby" />
      &nbsp;
      <input style="flex-grow:1;" class="btn btn-primary" id="current-location-btn" onclick="findPosition()" style="display:none;" type="button" value="Use My Location" />
      &nbsp;
      <input class="btn btn-danger" id="clear-address-btn" onclick="reDrawMap()" style="display:none;flex-grow:1;" type="button" value="Clear Search" />
    </div>
  </div>
  <div class="row-fluid row-fluid_maps">
    <div id="map-canvas">
    </div>
    <div class="directions-panel" id="directionsPanel" style="float:right;height:65%;display:none">
    </div>
    <div class="directions-clinic-info" id="clinicInfo" style="float:right;height:35%;display:none">
    </div>
  </div>
</div>
<div class="row-fluid row-fluid_maps" id="group-hospital-list">
</div>
<div style="display:none;">
  <!-- This is a clockwise mustache.js template. For more info goto https://mustache.github.io/ -->
  <script id="map_full_hospital" type="text/template">
    <div class="map-window-full" id="hospital-window-{{id}}">
      <h5 class="opensans"><strong>{{{hospital_name_link}}}</strong></h5>
      <h5 class="opensans">{{{drive_time}}}</h5>
      <h5 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;in line.</h5>
      <h5 class="opensans">{{{address_1}}}</h5>
      <h5 class="opensans">{{{address_2}}}</h5>
      <h5 class="opensans">{{{city}}}, {{{state}}} {{{zip}}}</h5>
      <h5 class="opensans">{{{phone_number}}}</h5>{{{schedule_button}}}
    </div>
  </script>
  <script id="map_wait_window" type="text/template">
    <div class="map-window-wait" id="hospital-window-{{id}}">
      <h5 class="opensans"><strong>{{{hospital_name_link}}}</strong></h5>
      <h5 class="opensans">{{{drive_time}}}</h5>
      <h5 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;in line.</h5>
    </div>
  </script>
  <script id="list_full_hospital" type="text/template">
    <div class="span4 margin-group margin-top text-center" id="list-hospital-{{id}}" style="height:300px">
      <h4 class="opensans">
        <a class="map-tooltip" onclick="focusMap({{id}})" target="_blank" title="">
          <img src="{{icon_url}}" />&nbsp;
        </a><strong>{{{hospital_name_link}}}</strong>
      </h4>
      <h4 class="opensans drive_time_header">{{{drive_time}}}</h4>
      <h4 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;in line.</h4><h4 class="opensans">{{{address_1}}}</h4>
      <h4 class="opensans">{{{address_2}}}</h4>
      <h4 class="opensans">{{{city}}}, {{{state}}} {{{zip}}}</h4>
      <h4 class="opensans">{{{phone_number}}}</h4>{{{schedule_button}}}
    </div>
  </script>
  <!-- This is the end of the mustache.js template -->
</div>
```

---

## Google Maps API key

Google requires the use of a key to identify your site. The script tag in your header will need to change from:

```
<script src="//maps.googleapis.com/maps/api/js" type="text/javascript"></script>
```

to:

```
<script src="//maps.googleapis.com/maps/api/js?key=YOUR_API_KEY" type="text/javascript"></script>
```

Google's documentation on [obtaining an API key](https://developers.google.com/maps/documentation/javascript/get-api-key)
will guide you through the process.

---

## Customizing output

Each of the mustache templates copied into your page allows for customization. There are three
templates that are used to customize information being shown on the page. Each template can
be identified with:

```html
<script id="name_of_the_template" type="text/template">
```

- `#map_full_hospital` - When clicking on a map pin, this template controls what's in the popup.
- `#map_wait_window` - Each pin by default has a little description above the pin, this controls the contents there.
- `#list_full_hospital` - All locations are listed below the map, this controls the information displayed there.

### Examples
- [Changing the number of patients waiting](examples/change_number_of_patients_waiting.md)
- [Remove elements on page](examples/remove_elements_on_page.md)
- [Remove the links](examples/remove_the_links.md)
- [Use a different scheduling page](examples/use_different_scheduling_page.md)
- [Custom styling](examples/custom_styling.md)

---

## Building your own map

The information on locations and wait_times for a group can be found at:

```
https://www.clockwisemd.com/groups/REPLACEME.json
```
