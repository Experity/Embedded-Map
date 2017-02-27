# Clockwise.MD Website Map

## A Quick Note

This is a patient facing map that is meant to be added to your clinic or hospital's public
facing website. It does not in any way affect functionality of the application.

---

## Demonstration

[Click here to see the widget in action](http://lightshedhealth.github.io/Website-Map-API/)

---

## Beginner's Guide

This first snippet of code loads the dependencies for the maps and styles. It should go inside the
`<head>` tag of your web page. You want to change __REPLACEME__ with your group's id number where noted.

```html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="//s3-us-west-1.amazonaws.com/clockwisepublic/mustache.js"></script>
<script src="//cdn.pubnub.com/pubnub.min.js" type="text/javascript"></script>
<script src="//maps.googleapis.com/maps/api/js?v=3&amp;amp;sensor=false" type="text/javascript"></script>
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

### Example: Changing the number of patients waiting

The current wait is currently set to use `{{{current_queue_length}}}`, which will display the shortest
length currently at your clinic. If you wish to use a different representation, your options are as follows:

- `{{{current_queue_length}}}` - Number of patients in the shortest line
- `{{{current_queue_total}}}` - Total number of patients in all lines
- `{{{current_wait}}}` - Shortest wait time in minutes from now
- `{{{current_wait_hhmm}}}` - Shortest wait time represented as an actual time
- `{{{current_next_available}}}` - The next available time if one were to enter the queue right now

For instance, if you want to display the wait time instead of the number of patients in line, find:

```html
  <script id="map_wait_window" type="text/template">
    <div class="map-window-wait" id="hospital-window-{{id}}">
      <h5 class="opensans"><strong>{{{hospital_name_link}}}</strong></h5>
      <h5 class="opensans">{{{drive_time}}}</h5>
      <h5 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;in line.</h5>
    </div>
  </script>
```

And change `{{{current_queue_length}}}` to `{{{current_wait}}}` and make it look like this:

```html
  <script id="map_wait_window" type="text/template">
    <div class="map-window-wait" id="hospital-window-{{id}}">
      <h5 class="opensans"><strong>{{{hospital_name_link}}}</strong></h5>
      <h5 class="opensans">{{{drive_time}}}</h5>
      <h5 class="opensans"><strong class="current_wait_placeholder">{{{current_wait}}}</strong>&nbsp;min wait.</h5>
    </div>
  </script>
```

### Example: Remove elements on page

Or maybe you want to remove the buttons of the bottom of the page listed under each hospital location.

Take the following snippet:

```html
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
```

And remove `{{{schedule_button}}}` on the line:

```html
      <h4 class="opensans">{{{phone_number}}}</h4>{{{schedule_button}}}
```

to this:

```html
      <h4 class="opensans">{{{phone_number}}}</h4>
```

### Example: Remove the links

Another example is if you don't want the hospital names to be links, change:

```html
        <a class="map-tooltip" onclick="focusMap({{id}})" target="_blank" title="">
          <img src="{{icon_url}}" />&nbsp;
        </a><strong>{{{hospital_name_link}}}</strong>
```

to

```html
        <a class="map-tooltip" onclick="focusMap({{id}})" target="_blank" title="">
          <img src="{{icon_url}}" />&nbsp;
        </a><strong>{{{hospital_name}}}</strong>
```

### Example: Use a different scheduling page

If you want to direct patients to the Clockwise primary care scheduling page instead of the same-day online scheduling page, replace all instances of `{{{hospital_name_link}}}` and `{{{schedule_button}}}` with links to `https://www.clockwisemd.com/hospitals/{{{hospital_id}}}/appointments/schedule_visit`, optionally using `{{{hospital_name}}}` to show the hospital name as the link text.  The result of doing so for all three Mustache templates would be

```html
  <script id="map_full_hospital" type="text/template">
    <div class="map-window-full" id="hospital-window-{{id}}">
      <h5 class="opensans"><strong>
        <a href="https://www.clockwisemd.com/hospitals/{{{hospital_id}}}/appointments/schedule_visit">
          {{{hospital_name}}}
        </a>
      </strong></h5>
      <h5 class="opensans">{{{drive_time}}}</h5>
      <h5 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;in line.</h5>
      <h5 class="opensans">{{{address_1}}}</h5>
      <h5 class="opensans">{{{address_2}}}</h5>
      <h5 class="opensans">{{{city}}}, {{{state}}} {{{zip}}}</h5>
      <h5 class="opensans">{{{phone_number}}}</h5>
      <a href="https://www.clockwisemd.com/hospitals/{{{hospital_id}}}/appointments/schedule_visit">
        <div class='btn btn-primary margin-bottom-10'>Get In Line Now</div>
      </a>
    </div>
  </script>
  <script id="map_wait_window" type="text/template">
    <div class="map-window-wait" id="hospital-window-{{id}}">
      <h5 class="opensans"><strong>
        <a href="https://www.clockwisemd.com/hospitals/{{{hospital_id}}}/appointments/schedule_visit">
          {{{hospital_name}}}
        </a>
      </strong></h5>
      <h5 class="opensans">{{{drive_time}}}</h5>
      <h5 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;in line.</h5>
    </div>
  </script>
  <script id="list_full_hospital" type="text/template">
    <div class="span4 margin-group margin-top text-center" id="list-hospital-{{id}}" style="height:300px">
      <h4 class="opensans">
        <a class="map-tooltip" onclick="focusMap({{id}})" target="_blank" title="">
          <img src="{{icon_url}}" />&nbsp;
        </a>
        <strong><a href="https://www.clockwisemd.com/hospitals/{{{hospital_id}}}/appointments/schedule_visit">
          {{{hospital_name}}}
        </a></strong>
      </h4>
      <h4 class="opensans drive_time_header">{{{drive_time}}}</h4>
      <h4 class="opensans"><strong class="current_wait_placeholder">{{{current_queue_length}}}</strong>&nbsp;in line.</h4><h4 class="opensans">{{{address_1}}}</h4>
      <h4 class="opensans">{{{address_2}}}</h4>
      <h4 class="opensans">{{{city}}}, {{{state}}} {{{zip}}}</h4>
      <h4 class="opensans">{{{phone_number}}}</h4>
      <a href="https://www.clockwisemd.com/hospitals/{{{hospital_id}}}/appointments/schedule_visit">
        <div class='btn btn-primary margin-bottom-10'>Get In Line Now</div>
      </a>
    </div>
  </script>
```

---

## Advanced Topics

If you would like to do custom styling, the maps API provides all necessary information so as to
populate your groups page. Include the same libraries as before, except now in your own
JavaScript you'll want to look at the `hsp_info` object.

```html
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script src="//s3-us-west-1.amazonaws.com/clockwisepublic/mustache.js"></script>
<script src="//cdn.pubnub.com/pubnub.min.js" type="text/javascript"></script>
<script src="//maps.googleapis.com/maps/api/js?v=3&amp;amp;sensor=false" type="text/javascript"></script>
<script src="//s3-us-west-1.amazonaws.com/clockwisepublic/geoposition.js"></script>
<script src="//s3-us-west-1.amazonaws.com/clockwisepublic/infobox.js"></script>
<script src="//www.clockwisemd.com/groups/REPLACEME.js" type="text/javascript"></script>

<script>
  console.log(hsp_info);
</script>
```

The above snippet will print the hospital's in _REPLACEME_ on the console. Through the `hsp_info`
variable you'll have access to the hospital's name, address, hours of operation, as well as
longitude and latitude coordinates so that you can use that data to populate a custom map.

---

## Building your own map

The information on locations and wait_times for a group can be found at:

```
https://www.clockwisemd.com/groups/REPLACEME.json
```
