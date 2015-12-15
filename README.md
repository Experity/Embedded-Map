# Clockwise.MD Website Map
### A Quick Note
This is a patient facing map that is meant to be added to your clinic or hospital's public
facing website.  It does not in any way affect functionality of the application.

---
### Demonstration
[Click here to see the widget in action](http://lightshedhealth.github.io/Website-Map-API/)

---
### Beginner's Guide
This first snippet of code loads the dependencies for the maps and styles.  It should go inside the
`<head>` tag of your web page.  You want to replace __[GROUP_ID]__ with your group's id number
(exclude the brackets) where noted.

```javascript

<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="https://s3-us-west-1.amazonaws.com/clockwisepublic/mustache.js"></script>
<script src="http://cdn.pubnub.com/pubnub.min.js" type="text/javascript"></script>
<script src="http://maps.googleapis.com/maps/api/js?v=3&amp;amp;sensor=false" type="text/javascript"></script>
<script src="https://s3-us-west-1.amazonaws.com/clockwisepublic/geoposition.js"></script>
<script src="https://s3-us-west-1.amazonaws.com/clockwisepublic/infobox.js"></script>
<script src="https:/clockwisemd.com/groups/[GROUP_ID].js" type="text/javascript"></script>
<link href="http://fonts.googleapis.com/css?family=Open+Sans:300italic,400italic,600italic,300,400,600" media="screen" rel="stylesheet" />
<link href="https://s3-us-west-1.amazonaws.com/clockwisepublic/clockwise_map.css" media="all" rel="stylesheet" />

<style>
  .row-fluid_maps{ height:300px; }
</style>

```

---
This next snippet of code will render a map on your webpage with a search bar for patients to enter their location.  This can be placed anywhere within the
`<body>` tag on your web page.

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
  <script id="map_full_hospital" type="text/template"><div class="map-window-full" id="hospital-window-{{id}}"><h5 class="opensans"><strong>{{{hospital_name_link}}}</strong></h5><h5 class="opensans">{{{drive_time}}}</h5><h5 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;patient in line.</h5><h5 class="opensans">{{{address_1}}}</h5><h5 class="opensans">{{{address_2}}}</h5><h5 class="opensans">{{{city}}}, {{{state}}} {{{zip}}}</h5><h5 class="opensans">{{{phone_number}}}</h5>{{{schedule_button}}}</div></script>
  <script id="map_wait_window" type="text/template"><div class="map-window-wait" id="hospital-window-{{id}}"><h5 class="opensans"><strong>{{{hospital_name_link}}}</strong></h5><h5 class="opensans">{{{drive_time}}}</h5><h5 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;patient in line.</h5></div></script>
  <script id="list_full_hospital" type="text/template"><div class="span4 margin-group margin-top text-center" id="list-hospital-{{id}}" style="height:300px"><h4 class="opensans"><a class="map-tooltip" onclick="focusMap({{id}})" target="_blank" title=""><img src="{{icon_url}}" />&nbsp;</a><strong>{{{hospital_name_link}}}</strong></h4><h4 class="opensans drive_time_header">{{{drive_time}}}</h4><h4 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;patient in line.</h4><h4 class="opensans">{{{address_1}}}</h4><h4 class="opensans">{{{address_2}}}</h4><h4 class="opensans">{{{city}}}, {{{state}}} {{{zip}}}</h4><h4 class="opensans">{{{phone_number}}}</h4>{{{schedule_button}}}</div></script>
  <!-- This is the end of the mustache.js template -->
</div>

```
