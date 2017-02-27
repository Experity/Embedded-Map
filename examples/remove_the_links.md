### Example: Remove the links

Scenario: you don't want the hospital names to be links. Change:

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
