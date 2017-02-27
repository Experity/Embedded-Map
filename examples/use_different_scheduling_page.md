### Example: Use a different scheduling page

Scenario: you want to direct patients to the Clockwise primary care scheduling page instead of the same-day online scheduling page, replace all instances of `{{{hospital_name_link}}}` and `{{{schedule_button}}}` with links to `https://www.clockwisemd.com/hospitals/{{{hospital_id}}}/appointments/schedule_visit`, optionally using `{{{hospital_name}}}` to show the hospital name as the link text.  The result of doing so for all three Mustache templates would be

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

