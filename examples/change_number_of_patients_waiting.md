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
