## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/Albertzmh/albert-leaflet.github.io/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Albertzmh/albert-leaflet.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Leaflet Tutorial</title>
<!-- .css in head -->
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css" />

    <style>

        body{
            margin: 0;
            padding: 0;
        }
        #map {
            width: 100%;
            height: 100vh;
        }
    </style>
</head>
<body>
   <div id= "map"></div>
</body>
</html>
<!-- .js in script -->
<script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"></script>

<script>
  //map initialization
  var map = L.map('map').setView([16.8409,  96.1735], 8);
//osm layer
  var osm=L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
});
osm.addTo(map);

//water colour
var watercolor = L.tileLayer('https://stamen-tiles-{s}.a.ssl.fastly.net/watercolor/{z}/{x}/{y}.{ext}', {
	attribution: 'Map tiles by <a href="http://stamen.com">Stamen Design</a>, <a href="http://creativecommons.org/licenses/by/3.0">CC BY 3.0</a> &mdash; Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
	subdomains: 'abcd',
	minZoom: 1,
	maxZoom: 16,
	ext: 'jpg'
});
watercolor.addTo(map)
//google maps
var gMap = L.tileLayer('http://{s}.google.com/vt/lyrs=m&x={x}&y={y}&z={z}',{
     maxZoom: 20, subdomains:['mt0','mt1','mt2','mt3']
 }); 
gMap.addTo(map);

//Marker
var myIcon= L.icon({
    iconUrl: 'img/ROCATION LOGO_2.png',
    iconSize: [60,60],
});
var singleMarker = L.marker([16.8409,  96.1735], { icon: myIcon, draggable: true });
var popup = singleMarker.bindPopup('This is Yangon ' + singleMarker.getLatLng()).openPopup()
popup.addTo(map);

console.log(singleMarker.toGeoJSON())
//Layer Controller
var baseMaps = {
    "OSM": osm,
    "Water Colour": watercolor,
    "Google Map": gMap
};

var overlayMaps = {
    "marker": singleMarker
};
L.control.layers(baseMaps, overlayMaps, {collasped: false}).addTo(map);
</script>
