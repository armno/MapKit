# MapKit plugin for iOS and Android

> Forked from @imhotep's great [MapKit](https://github.com/imhotep/MapKit) plugin and customized to fit my own needs (and so, opinionated). I'm primarily focusing on iOS but also expecting the same functionality on Android too.

Uses *Apple Maps* on iOS and *Google Maps v2* on Android

Currently only works/tested on Android and iOS. Requires Cordova 3.0+ (will not work on earlier versions without modifications).

![Cordova Map 1](http://i.imgur.com/Mf6oeXal.png)

![Cordova Map 2](http://i.imgur.com/XaaBGeGl.png)

![Cordova Map 3](http://i.imgur.com/3IoDj0Rl.png)

![Cordova Map 4](http://i.imgur.com/Bfzik6Ml.png)

## Installation

**Android specific** - You need a [Google Maps Android v2 API KEY](https://code.google.com/apis/console/) from google and you need to specify it when you install the plugin.

`API_KEY` is optional for iOS.

install with cordova CLI

```sh
$ cordova -d plugin add https://github.com/imhotep/MapKit.git --variable API_KEY="YOUR_API_KEY_FROM_GOOGLE"
```

## Usage

The plugin exports 1 global `plugin` object with its `mapKit` property. Minimal usage is just to show the map with default `mapOptions`.

```js
plugin.mapKit.showMap(successCallback, errorCallback, mapOptions);
```

```html
<body>
  <script src="cordova.js"></script>
  <script>
    document.addEventListener('deviceready', function() {

      var onSuccess = function() {
        console.log('success');
      };

      var onError = function() {
        console.log('error');
      };

      plugin.mapKit.showMap(onSuccess, onError);
    });
  </script>
</body>
```

## Options

You can override the options by passing a suitable options object as arguments to `showMap()`

```js
var options = {
  height: 460,      // height of the map, in pixel
  width: 200,       // width of the map, in pixel
  lat: 49.281468,   // initial camera position latitude
  lon: -123.104446  // initial camera position latitude
};

mapKit.showMap(success, error, options);

// without overriding any defaults
mapKit.showMap(success, error);
```

| property | type | default value | required | description |
| -------- | ---- | ------- | -------- | ----------- |
| `height` | `number` | 50% of viewport | false | map's height |
| `width`  | `number` | 100% of viewport | false | map's width |
| `top`    | `number` | 0 | false | top offset for the map. do not use with `bottom` |
| `bottom`    | `number` | undefined | false | bottom offset for the map. do not use with `top` property |
| `left`    | `number` | 0 | false | left offset for the map |
| `lat`    | `number` | 49.281468 | false | latitude of map's center |
| `lon`    | `number` | -123.104446 | false | longitude of map's center |

## Constants

map types

```js
plugin.mapKit.mapType = {
  MAP_TYPE_NONE: 0, //No base map tiles.
  MAP_TYPE_NORMAL: 1, //Basic maps.
  MAP_TYPE_SATELLITE: 2, //Satellite maps with no labels.
  MAP_TYPE_TERRAIN: 3, //Terrain maps.
  MAP_TYPE_HYBRID: 4 //Satellite maps with a transparent layer of major streets.
}
```

icon colors

```js
plugin.mapKit.iconColors = {
  HUE_RED: 0.0,
  HUE_ORANGE: 30.0,
  HUE_YELLOW: 60.0,
  HUE_GREEN: 120.0,
  HUE_CYAN: 180.0,
  HUE_AZURE: 210.0,
  HUE_BLUE: 240.0,
  HUE_VIOLET: 270.0,
  HUE_MAGENTA: 300.0,
  HUE_ROSE: 330.0
};
```

## APIs

- `showMap(success, error, options)`
- `addMapPins(pins, success, error)`
- `clearMapPins(success, error)`
- `changeMapType(mapType, success, error)`
- `hideMap(success, error)`

```js
var app = {
  showMap: function() {
    var pins = [
    {
      lat: 49.28115,
      lon: -123.10450,
      title: "A Cool Title",
      snippet: "A Really Cool Snippet",
      icon: plugin.mapKit.iconColors.HUE_ROSE
    },
    {
      lat: 49.27503,
      lon: -123.12138,
      title: "A Cool Title, with no Snippet",
      icon: {
        type: "asset",
        resource: "www/img/logo.png", //an image in the asset directory
        pinColor: plugin.mapKit.iconColors.HUE_VIOLET //iOS only
      }
    },
    {
        lat: 49.28286,
        lon: -123.11891,
        title: "Awesome Title",
        snippet: "Awesome Snippet",
        icon: plugin.mapKit.iconColors.HUE_GREEN
    }];

    var error = function() {
      console.log('error');
    };

    var success = function() {
      plugin.mapKit.addMapPins(pins,
        function() {
          console.log('adMapPins success');
        },
        function() {
          console.log('error');
        }
      );
    };

    plugin.mapKit.showMap(success, error);
  },
  hideMap: function() {
    var success = function() {
      console.log('Map hidden');
    };
    var error = function() {
      console.log('error');
    };
    plugin.mapKit.hideMap(success, error);
  },
  clearMapPins: function() {
    var success = function() {
      console.log('Map Pins cleared!');
    };
    var error = function() {
      console.log('error');
    };
    plugin.mapKit.clearMapPins(success, error);
  },
  changeMapType: function() {
    var success = function() {
      console.log('Map Type Changed');
    };
    var error = function() {
      console.log('error');
    };
    plugin.mapKit.changeMapType(mapKit.mapType.MAP_TYPE_SATELLITE, success, error);
  }
}
```

Sample App
----------

Checkout the sample/ application as a boilerplate!

Missing features
----------------

Info bubbles: Simple info bubbles supported (title, snippet and custom icons for markers). Custom info bubbles not supported (i.e HTML bubbles etc..).

## Wishlist

see [issues](https://github.com/armno/MapKit/issues).

License
-------

Apache
