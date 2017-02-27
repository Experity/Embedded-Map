### Example: Remove elements on page

Scenario: you want to remove the buttons on the bottom of the page listed under each hospital location.

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
