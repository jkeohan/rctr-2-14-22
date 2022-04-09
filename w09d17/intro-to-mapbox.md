[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# React Mapbox

## Learning Objectives

- Learn to implement a basic map using the **react-map-gl** library


## Mapping Libraries

There are several popular JavaScript mapping libraries to choose from including:

- [Leaflet](https://leafletjs.com/)
- [Google Maps](https://cloud.google.com/maps-platform)
- [OpenLayers](https://openlayers.org/)
- [Mapbox](https://www.mapbox.com/)


### React Versions

All of these libraries have been ported over to React with each one having several different React libraries to choose from.  Let's take **Mapbox** which includes the following separate NPM libraries:

- [react-map-gl](https://github.com/visgl/react-map-gl)
- [react-mapbox-gl](https://github.com/alex3165/react-mapbox-gl)

When making the decision on which library to choose it's always best to do some research and see which one is trending on [npmtrends](https://www.npmtrends.com/mapbox-gl-vs-react-map-gl-vs-react-mapbox-gl).

For this lesson we will be working with **react-map-gl**


## Starter Code

Here is the [Starter CodeSandbox](https://codesandbox.io/s/rctr-mapbox-starter-2hden?file=/src/App.js) we will be using for this lecture.

**react-map-gl** library

If we examine the code we will see that it is a bare bones React app, however it also includes the **react-map-gl** dependency to help get us started.  

<img src="https://i.imgur.com/Yj0Cozl.png">

<br>
<br>

**mapbox-gl.css** 

Another import required is the **mapbox-gl.css** file which has also been imported via a a link tag. 

```html
 <link href='https://api.tiles.mapbox.com/mapbox-gl-js/v1.12.0/mapbox-gl.css'>
```

<hr>

#### <g-emoji class="g-emoji" alias="alarm_clock" fallback-src="https://github.githubassets.com/images/icons/emoji/unicode/23f0.png">⏰</g-emoji> Activity - 2min - Mapbox Access Token

Working with Mapbox requires that we sign up at Mapbox to create an access token.  

<img src="https://i.imgur.com/tgJQybC.png">

Take a few minutes to sign up and create an access token. 

<hr>

## Creating A Mapbox 

Now that we have an API token, let’s begin coding. To build a map, we will take advantage of the **ReactMapGl** component provided by **react-map-gl**. 

It takes in a number of props, including:

- **API token**: required to use the library
- **viewport**: Dimensions of your map, the center point, and the zoom constant.
- **mapStyle**: Various styles are available on Mapbox (with different combinations of color scheme, street-view, labels, etc.), or even create your own here.
- **onViewportChange**: Function that controls viewport transition (i.e. updating the viewport when a user drags the map).

### The ReactMapGl Component

Let's first import **ReactMapGl** into the **Map** component.


```js
import ReactMapGL from 'react-map-gl';
```

And then render it. 

```js
const Map = () => {
  return (
    <>
      <div>Map Goes Here</div>
      <ReactMapGL />
    </>
  );
};
```

Nothing will appear to happen but if we example **React Dev Tools** we should see the following: 

<img src="https://i.imgur.com/Br2T7qC.png">

#### Viewport Settings

The **viewport** settings define the Dimension of our map, the center point, and the zoom constant. Let's create a **viewport** variable to include those key:value pairs.

```js
const viewport = {
    width: 400,
    height: 400,
    latitude: 37.7577,
    longitude: -122.4376,
    zoom: 8
}
```

And then update **ReactMapGL** to include them. 

```js
<ReactMapGL {...viewport} />
```

At this point we should the following which means our map is working to some extent but yet something is missing. 

<img src="https://i.imgur.com/4hh5m9g.png">

### Mapbox Token

The missing piece is the **Access Token**. Let's include that as well. 

```js
const mapboxToken = "add your token here"

<ReactMapGL 
    mapboxApiAccessToken={mapboxToken}
{...viewport} 
/>
```

And with that we should now see the map. 

<img src="https://i.imgur.com/2GmixR0.png">

## Adding Mapbox Styles 

Mapbox comes with several additional styles that we can use of such as **light**, **dark**, **satelite** and several others. 

Let's take a look at the official [Mapbox Documentation](https://docs.mapbox.com/api/maps/styles/) and see which others are available. 

Implementing one of these styles is done by adding a **mapStyle** prop and setting it's value to one of the styles. 

```
<ReactMapGL 
     mapboxApiAccessToken={mapboxToken}
    {...viewport} 
    mapStyle='mapbox://styles/mapbox/satellite-v9'
/>
```

[Solution](https://codesandbox.io/s/rctr-mapbox-starter-8-2-21-0kfn5?file=/src/Map/index.js)


## Additional Resources
