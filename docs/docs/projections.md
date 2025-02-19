---
layout: spec
title: Projections
permalink: /docs/projections/index.html
---

Cartographic **projections** map _(longitude, latitude)_ pairs to projected _(x, y)_ coordinates. Vega uses projections to layout both geographic points (such as locations on a map) for which longitude and latitude coordinates are part of the input data, and geographic regions (such as countries and states) represented using the [GeoJSON](https://en.wikipedia.org/wiki/GeoJSON) format.

{% include embed spec="transforms/geoshape" %}

## Documentation Overview

- [Projection Properties](#properties)
- [Projection Types](#types)
- [Register Additional Projections](#register)

## <a name="properties"></a>Projection Properties

| Property      | Type          | Description    |
| :------------ |:-------------:| :------------- |
| name          | {% include type t="String" %}  | {% include required %} A unique name for the projection. Projections and [scales](../scales) share the same namespace; names must be unique across both.|
| [type](#projection-types) | {% include type t="String" %} | The cartographic projection to use. The default is `"mercator"`. This value is case-insensitive, for example `"albers"` and `"Albers"` indicate the same projection type. |
| [clipAngle](https://github.com/d3/d3-geo#projection_clipAngle) | {% include type t="Number" %} | Sets the projection’s clipping circle radius to the specified angle in degrees. If `null`, switches to [antimeridian](http://bl.ocks.org/mbostock/3788999) cutting rather than small-circle clipping.|
| [clipExtent](https://github.com/d3/d3-geo#projection_clipExtent) | {% include type t="Array" %} | Sets the projection’s viewport clip extent to the specified bounds in pixels. The extent bounds are specified as an array [[x0, y0], [x1, y1]], where x0 is the left-side of the viewport, y0 is the top, x1 is the right and y1 is the bottom. If `null`, no viewport clipping is performed. |
| [scale](https://github.com/d3/d3-geo#projection_scale) | {% include type t="Number" %} | Sets the projection’s scale factor to the specified value. The default scale is projection-specific. The scale factor corresponds linearly to the distance between projected points; however, scale factor values are not equivalent across projections. |
| [translate](https://github.com/d3/d3-geo#projection_translate) | {% include type t="Number[]" %} | Sets the projection’s translation offset to the specified two-element array [tx, ty]. If translate is not specified, returns the current translation offset which defaults to `[480, 250]`. The translation offset determines the pixel coordinates of the projection’s center. The default translation offset places (0&deg;,0&deg;) at the center of a 960&times;500 area.|
| [center](https://github.com/d3/d3-geo#projection_center) | {% include type t="Number[]" %} | Sets the projection’s center to the specified center, a two-element array of longitude and latitude in degrees. The default value is `[0, 0]`.|
| [rotate](https://github.com/d3/d3-geo#projection_rotate) | {% include type t="Number[]" %} | Sets the projection’s three-axis rotation to the specified angles, which must be a two- or three-element array of numbers [_lambda_, _phi_, _gamma_] specifying the rotation angles in degrees about each spherical axis. (These correspond to yaw, pitch and roll.) The default value is `[0, 0, 0]`.|
| [pointRadius](https://github.com/d3/d3-geo#path_pointRadius) | {% include type t="Number" %} | Sets the default radius (in pixels) to use when drawing GeoJSON `Point` and `MultiPoint` geometries. This parameter sets a constant default value, to modify the point radius in response to data, see the corresponding parameter of the [GeoPath](../transforms/GeoPath) and [GeoShape](../transforms/GeoShape) transforms. The default value is 4.5.|
| [precision](https://github.com/d3/d3-geo#projection_precision) | {% include type t="String" %} | Sets the threshold for the projection’s [adaptive resampling](http://bl.ocks.org/mbostock/3795544) to the specified value in pixels. This value corresponds to the [Douglas–Peucker](http://en.wikipedia.org/wiki/Ramer%E2%80%93Douglas%E2%80%93Peucker_algorithm) distance. If precision is not specified, returns the projection’s current resampling precision which defaults to √0.5 ≅ 0.70710...|
| fit | {% include type t="Object|Array" %} | GeoJSON data to which the projection should attempt to automatically fit the _translate_ and _scale_ parameters. If object-valued, this parameter should be a GeoJSON Feature or FeatureCollection. If array-valued, each array member may be a GeoJSON Feature, FeatureCollection, or a sub-array of GeoJSON Features.|
| extent | {% include type t="Array[]" %} | Used in conjunction with _fit_, provides the pixel area to which the projection should be automatically fit. The extent bounds are specified as an array `[[x0, y0], [x1, y1]]`, where x0 is the left side of the extent, y0 is the top, x1 is the right and y1 is the bottom.|
| size | {% include type t="Number[]" %} | Used in conjunction with _fit_, provides the width and height in pixels of the area to which the projection should be automatically fit. This parameter is equivalent to an _extent_ of `[[0,0], size]`. |

In addition to the shared properties above, the following properties are supported for specific projection types in the [d3-geo-projection](https://github.com/d3/d3-geo-projection) library:
[`coefficient`](https://github.com/d3/d3-geo-projection#hammer_coefficient),
[`distance`](https://github.com/d3/d3-geo-projection#satellite_distance),
[`fraction`](https://github.com/d3/d3-geo-projection#bottomley_fraction),
[`lobes`](https://github.com/d3/d3-geo-projection#berghaus_lobes),
[`parallel`](https://github.com/d3/d3-geo-projection#armadillo_parallel),
[`radius`](https://github.com/d3/d3-geo-projection#gingery_radius),
[`ratio`](https://github.com/d3/d3-geo-projection#hill_ratio),
[`spacing`](https://github.com/d3/d3-geo-projection#lagrange_spacing),
[`tilt`](https://github.com/d3/d3-geo-projection#satellite_tilt).

## <a name="types"></a>Projection Types

Vega includes all cartographic projections provided by the [d3-geo](https://github.com/d3/d3-geo#) library.

| Type          | Description   |
| :------------ |:------------- |
| [albers](https://github.com/d3/d3-geo#geoAlbers)          | The Albers’ equal-area conic projection. This is a U.S.-centric configuration of `"conicEqualArea"`. |
| [albersUsa](https://github.com/d3/d3-geo#geoAlbersUsa) | A U.S.-centric composite with projections for the lower 48 states, Hawaii, and Alaska (scaled to 0.35 times the true relative area). |
| [azimuthalEqualArea](https://github.com/d3/d3-geo#geoAzimuthalEqualArea) | The azimuthal equal-area projection. |
| [azimuthalEquidistanct](https://github.com/d3/d3-geo#geoAzimuthalEquidistant) | The azimuthal equidistant projection. |
| [conicConformal](https://github.com/d3/d3-geo#geoConicConformal) | The conic conformal projection. The parallels default to [30&deg;, 30&deg;] resulting in flat top. |
| [conicEqualArea](https://github.com/d3/d3-geo#geoConicEqualArea) | The Albers’ equal-area conic projection. |
| [conicEquidistant](https://github.com/d3/d3-geo#geoConicEquidistant) | The conic equidistant projection. |
| [equirectangular](https://github.com/d3/d3-geo#geoEquirectangular) | The equirectangular (plate carr&eacute;e) projection, akin to using longitude, latitude directly. |
| [gnomonic](https://github.com/d3/d3-geo#geoGnomonic) | The gnomonic projection. |
| [identity](https://github.com/d3/d3-geo#geoIdentity) | The identity transform, which can be used to translate, scale, and clip planar geometry. Also supports additional boolean [`reflectX`](https://github.com/d3/d3-geo#identity_reflectX) and [`reflectY`](https://github.com/d3/d3-geo#identity_reflectY) parameters. |
| [mercator](https://github.com/d3/d3-geo#geoMercator) | The spherical Mercator projection. Uses a default `clipExtent` such that the world is projected to a square, clipped to approximately ±85&deg; latitude. |
| [naturalEarth1](https://github.com/d3/d3-geo#geoNaturalEarth1) | The [Natural Earth projection](http://www.shadedrelief.com/NE_proj/) is a pseudocylindrical projection designed by Tom Patterson. It is neither conformal nor equal-area, but appealing to the eye for small-scale maps of the whole world. |
| [orthographic](https://github.com/d3/d3-geo#geoOrthographic) | The orthographic projection. |
| [stereographic](https://github.com/d3/d3-geo#geoStereographic) | The stereographic projection. |
| [transverseMercator](https://github.com/d3/d3-geo#geoTransverseMercator) | The transverse spherical Mercator projection. Uses a default `clipExtent` such that the world is projected to a square, clipped to approximately ±85&deg; latitude. |

## <a name="register"></a>Register Additional Projections

Vega can be extended with additional projections, such as those found in the [d3-geo-projection](https://github.com/d3/d3-geo-projection) library.

To register all extended projections from d3-geo-projection with Vega, simply import the [vega-projection-extended](https://github.com/vega/vega-projection-extended) library:

```html
<script src="https://cdn.jsdelivr.net/npm/vega-projection-extended@1.0.0"></script>
```

Alternatively, custom projections can be manually registered using the `vega.projection` method:

```js
// Assumes d3-geo-projection is imported under the d3 variable.
// To register with Vega, provide a name and projection function.
vega.projection('winkel3', d3.geoWinkel3);

// Vega parser and runtime now support the 'winkel3' projection
var runtime = vega.parse({
  ...,
  "projections": [
    { "name": "proj", "type": "winkel3" }
  ],
  ...
});
```
