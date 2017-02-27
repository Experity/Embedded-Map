### Example: Use custom styling

Scenario: If you would like to do custom styling, the maps API provides all necessary information so as to
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
