
{{ target: component-globe }}

# globe(Object)

Earth components. Providing assembly drawing of the earth and the corresponding coordinates, developers can display a three-dimensional scattergram, bubble chart, histogram, line graph flying above.

## show(boolean) = true

Whether Earth components.

## globeRadius (number) = 100
Radius of the Earth. With respect to the unit three-dimensional space, with [viewControl.distance] (~ globe.viewControl.distance) correlation.

{{ use: partial-environment(
    componentType="globe",
    componentName="地球"
) }}

## baseTexture(string|HTMLImageElement|HTMLCanvasElement|EChartsInstance)

The texture of the earth. Support picture path string, Canvas pictures or objects.

Also supports direct use as an example echarts texture, echarts examples of mouse action at this time on Earth will be used with the textures have linkage.

Example:
```js
// use the Earth texture image
baseTexture: 'asset/earth.jpg'


// Example echarts drawing the world map as a texture
var canvas = document.createElement('canvas');
var Mapchart = echarts.init (canvas, null, {
    width: 4096, height: 2048
});
mapChart.setOption({
    series : [
        {
            type: 'map',
            map: 'world',
            // Draw full size echarts examples
            top: 0, left: 0,
            right: 0, bottom: 0,
            boundingCoords: [[-180, 90], [180, -90]]
        }
    ]
});
...
BaseTexture: mapChart

```

## heightTexture(string|HTMLImageElement|HTMLCanvasElement)

Highly textured earth. Highly textured may be used [bump mapping] (https://zh.wikipedia.org/wiki/%E5%87%B9%E5%87%B8%E8%B4%B4%E5%9B%BE) represents the earth surface the light and dark detail. FIG following two are used and the effect of the difference between `heightTexture`` heightTexuture` unused.

![400xauto](~heightmap-enable.png)

![400xauto](~heightmap-disable.png)

## displacementTexture(string|HTMLImageElement|HTMLCanvasElement)

Earth displacement vertex texture, with the default [heightTexture] (~ globe.heightTexture).

Compared to bump mapping, displacement of vertices is vertex displacement made directly from the texture. Effective greater than 0 [displaymentScale] (~ globe.displaymentScale).

## displacementScale(number) = 0

Earth displacement vertex size. The default is 0, i.e. no displacement, are provided below two FIG different effects `displacementScale`

<div class="twentytwenty-container" style="width: 700px;">
    <img src="documents/asset/gl/img/displacement-disable.png" width="100%" title="Scale: 0">
    <img src="documents/asset/gl/img/displacement-enable.png" width="100%" title="Scale: 0.1">
</div>

## displacementQuality(string) = 'medium'

Quality vertex displacement of the Earth. Support provided ` 'low'`,`' medium'`, ` 'high'`,`' ultra'`. Higher quality surface height can show more detail. The following are the effects of different theme of `displacementQuality`

<div class="twentytwenty-container" style="width: 700px;">
    <img src="documents/asset/gl/img/displacement-low.png" width="100%" title="Low">
    <img src="documents/asset/gl/img/displacement-ultra.png" width="100%" title="Ultra">
</div>


{{ use: partial-shading-globe(
    componentType="globe",
    componentName="地球"
) }}

{{ use: partial-light-globe(
    componentType="globe",
    componentName="地球"
) }}

{{ use: partial-post-effect(
    componentType="globe",
    componentName="地球"
) }}

{{ use: partial-temporal-super-sampling(
    componentType="globe",
    componentName="地球"
) }}

{{ use: partial-view-control(
    componentType="globe",
    componentName="地球",
    defaultPanSensitivity=0
) }}

### targetCoord(Array)

Positioning latitude and longitude coordinates of the target. After setting ignored [alpha] (~ globe.viewControl.alpha) and [beta] (~ globe.viewControl.beta).


```js
viewControl: {
    // navigate to Beijing
    targetCoord: [116.46, 39.92]
}
```


## layers(Array)

Configuring the Earth's surface layer, you can use the added configuration item clouds, or on [baseTexture] (~ globe.baseTexture) supplemented drawn contour countries like.

### show(boolean) = true

Whether the layer.

### type(string) = 'overlay'

Type layer, optionally:

+ `'overlay'`

A cover layer on the surface, and the like can be used to display clouds.

+ `'blend'`

With [baseTexture] (~ globe.baseTexture) mixing.

### name(string)

Name layer, set layer properties can be used when using setOption name to identify the layer needs to be updated.

```js
chart.setOption({
    globe: {
        layer: [{
            // Update name is 'cloud' of the texture layer
            name: 'cloud',
            texture: 'cloud.png'
        }]
    }
});
```

### blendTo(string) = 'albedo'

In the [type] (~ globe.layers.type) to ` 'is blend'` valid.

Optional:
+ `Albedo` mixed albedo, affected by illumination.

+ `Emission` mixed self-luminous, light is not affected.

### intensity(number) = 1

Mixing intensity.

### shading(string) = 'lambert'

Coloring effect covering layer, with [globe.shading] (~ globe.shading), supports the ` 'color'`,`' lambert'`, ` 'realistic'`

In the [type] (globe.layers.type) to ` 'is overlay'` valid.

### distance(number) = null

Distance from the cover layer of the Earth's surface.

In the [type] (~ globe.layers.type) to ` 'is overlay'` valid.


### texture(string|HTMLImageElement|HTMLCanvasElement|EChartsInstance)

Texture layer, to support the image path string, Canvas pictures or objects.

Also supports direct use as an example echarts texture, echarts examples of mouse action at this time on Earth will be used with the textures have linkage.

{{ use: partial-zlevel }}

{{ use: partial-viewport }}


{{ target: partial-shading-globe(master=partial-shading) }}

{{ block: shading-compare }}
Here is the difference between different colored effect

![250xauto](~globe-shading-color.png)
![250xauto](~globe-shading-lambert.png)
![250xauto](~globe-shading-realistic.png)
{{ /block }}


{{ target: partial-light-globe(master=partial-light) }}

{{ block: light-extend }}
###${prefix|default("#")} time(Date)

Sunshine time, the system defaults to the current time.

{{ /block }}

