---
layout: spec
title: Axes
permalink: /docs/axes/index.html
---

**Axes** visualize spatial [scale](../scales) mappings using ticks, grid lines and labels. Vega currently supports axes for Cartesian (rectangular) coordinates. Similar to scales, axes can be defined either at the top-level of the specification, or as part of a [group mark](../marks/group).

## Axis Properties

Properties for specifying a coordinate axis.

| Property      | Type                           | Description    |
| :------------ | :----------------------------: | :------------- |
| scale         | {% include type t="String" %}  | {% include required %} The name of the scale backing the axis component.|
| orient        | {% include type t="String" %}  | {% include required %} The orientation of the axis. See the [axis orientation reference](#orientation).|
| bandPosition  | {% include type t="Number" %}  | An interpolation fraction indicating where, for `band` scales, axis ticks should be positioned. A value of `0` places ticks at the left edge of their bands. A value of `0.5` places ticks in the middle of their bands. |
| domain        | {% include type t="Boolean" %} | A boolean flag indicating if the domain (the axis baseline) should be included as part of the axis (default `true`).|
| domainColor   | {% include type t="Color" %}   | Color of axis domain line. |
| domainWidth   | {% include type t="Number" %}  | Stroke width of axis domain line. |
| encode        | {% include type t="Object" %}  | Optional mark encodings for custom axis styling. Supports encoding blocks for `axis`, `ticks`, `grid`, `labels`, `title`, and `domain`. See [custom axis encodings](#custom).|
| format        | {% include type t="String" %}  | The format specifier pattern for axis labels. For numerical values, must be a legal [d3-format](https://github.com/d3/d3-format#locale_format) specifier. For date-time values, must be a legal [d3-time-format](https://github.com/d3/d3-time-format#locale_format) specifier.|
| grid          | {% include type t="Boolean" %} | A boolean flag indicating if grid lines should be included as part of the axis (default `false`).|
| gridColor     | {% include type t="Color" %}   | Color of axis grid lines. |
| gridDash      | {% include type t="Number[]" %} | Stroke dash of axis grid lines (or `[]` for solid lines). |
| gridOpacity   | {% include type t="Number" %}  | Opacity of axis grid lines. |
| gridScale     | {% include type t="String" %}  | The name of the scale to use for including grid lines. By default grid lines are driven by the same scale as the ticks and labels.|
| gridWidth     | {% include type t="Number" %}  | Stroke width of axis grid lines. |
| labels        | {% include type t="Boolean" %} | A boolean flag indicating if labels should be included as part of the axis (default `true`).|
| labelAlign    | {% include type t="String" %}  | Horizontal text alignment of axis tick labels, overriding the default setting for the current axis orientation. |
| labelAngle    | {% include type t="Number" %}  | Angle in degrees of axis tick labels. |
| labelBaseline   | {% include type t="String" %}  | Vertical text baseline of axis tick labels, overriding the default setting for the current axis orientation. |
| labelBound    | {% include type t="Boolean|Number" %} | Indicates if labels should be hidden if they exceed the axis range. If `false` (the default) no bounds overlap analysis is performed. If `true`, labels will be hidden if they exceed the axis range by more than 1 pixel. If this property is a number, it specifies the pixel tolerance: the maximum amount by which a label bounding box may exceed the axis range.|
| labelColor    | {% include type t="Color" %}   | Text color of axis tick labels. |
| labelFlush    | {% include type t="Boolean|Number" %} | Indicates if labels at the beginning or end of the axis should be aligned flush with the scale range. If a number, indicates a pixel distance threshold: labels with anchor coordinates within the threshold distance for an axis end-point will be flush-adjusted. If `true`, a default threshold of 1 pixel is used. Flush alignment for a horizontal axis will left-align labels near the beginning of the axis and right-align labels near the end. For vertical axes, bottom and top text baselines will be applied instead.|
| labelFlushOffset | {% include type t="Number" %} | Indicates the number of pixels by which to offset flush-adjusted labels (default `0`). For example, a value of `2` will push flush-adjusted labels 2 pixels outward from the center of the axis. Offsets can help the labels better visually group with corresponding axis ticks.|
| labelFont     | {% include type t="String" %}  | Font name for axis tick labels. |
| labelFontSize | {% include type t="Number" %}  | Font size of axis tick labels. |
| labelFontWeight | {% include type t="String|Number" %} | Font weight of axis tick labels. |
| labelLimit    | {% include type t="Number" %}  | The maximum allowed length in pixels of axis tick labels. |
| labelOverlap  | {% include type t="Boolean|String" %} | The strategy to use for resolving overlap of axis labels. If `false` (the default), no overlap reduction is attempted. If set to `true` or `"parity"`, a strategy of removing every other label is used (this works well for standard linear axes). If set to `"greedy"`, a linear scan of the labels is performed, removing any label that overlaps with the last visible label (this often works better for log-scaled axes).|
| labelPadding  | {% include type t="Number" %}  | The padding in pixels between labels and ticks.|
| minExtent     | {% include type t="Number|Value" %} | The minimum extent in pixels that axis ticks and labels should use. This determines a minimum offset value for axis titles.|
| maxExtent     | {% include type t="Number|Value" %} | The maximum extent in pixels that axis ticks and labels should use. This determines a maximum offset value for axis titles.|
| offset        | {% include type t="Number|Value" %} | The orthogonal offset in pixels by which to displace the axis from its position along the edge of the chart.|
| position      | {% include type t="Number|Value" %} | The anchor position of the axis in pixels (default `0`). For x-axes with top or bottom orientation, this sets the axis group `x` coordinate. For y-axes with left or right orientation, this sets the axis group `y` coordinate.|
| ticks         | {% include type t="Boolean" %} | A boolean flag indicating if ticks should be included as part of the axis (default `true`).|
| tickColor     | {% include type t="Color" %}   | Color of axis ticks. |
| tickCount     | {% include type t="Number|String|Object" %}  | A desired number of ticks, for axes visualizing quantitative scales. The resulting number may be different so that values are "nice" (multiples of 2, 5, 10) and lie within the underlying scale's range. For scales of type `time` or `utc`, the tick count can instead be a time interval specifier. Legal string values are `"millisecond"`, `"second"`, `"minute"`, `"hour"`, `"day"`, `"week"`, `"month"`, and `"year"`. Alternatively, an object-valued interval specifier of the form `{"interval": "month", "step": 3}` includes a desired number of interval steps. Here, ticks are generated for each quarter (Jan, Apr, Jul, Oct) boundary.|
| tickExtra     | {% include type t="Boolean" %} | Boolean flag indicating if an extra axis tick should be added for the initial position of the axis. This flag is useful for styling axes for `band` scales such that ticks are placed on band boundaries rather in the middle of a band. Use in conjunction with `"bandPostion": 1` and an axis `"padding"` value of `0`. |
| tickOffset    | {% include type t="Number" %}  | Position offset in pixels to apply to ticks, labels, and gridlines. |
| tickRound     | {% include type t="Boolean" %} | Boolean flag indicating if pixel position values should be rounded to the nearest integer. |
| tickSize      | {% include type t="Number" %}  | The length in pixels of axis ticks.|
| tickWidth     | {% include type t="Number" %}  | Width in pixels of axis ticks. |
| title         | {% include type t="String" %}  | A title for the axis (none by default).|
| titleAlign    | {% include type t="String" %}  | Horizontal text alignment of axis titles. |
| titleAngle    | {% include type t="Number" %}  | Angle in degrees of axis titles. |
| titleBaseline | {% include type t="String" %}  | Vertical text baseline for axis titles. |
| titleColor    | {% include type t="Color" %}   | Text color of axis titles. |
| titleFont     | {% include type t="String" %}  | Font name for axis titles. |
| titleFontSize | {% include type t="Number" %}  | Font size of axis titles. |
| titleFontWeight | {% include type t="String|Number" %} | Font weight of axis titles. |
| titleLimit    | {% include type t="Number" %}  | The maximum allowed length in pixels of axis titles. |
| titlePadding  | {% include type t="Number|Value" %} | The padding in pixels between the axis labels and axis title.|
| titleX        | {% include type t="Number" %}  | Custom X position of the axis title relative to the axis group, overriding the standard layout. |
| titleY        | {% include type t="Number" %}  | Custom Y position of the axis title relative to the axis group, overriding the standard layout. |
| values        | {% include type t="Array" %}   | Explicitly set the visible axis tick and label values.|
| zindex        | {% include type t="Number" %}  | The integer z-index indicating the layering of the axis group relative to other axis, mark and legend groups. The default value is `0` and axes and grid lines are drawn _behind_ any marks defined in the same specification level. Higher values (`1`) will cause axes and grid lines to be drawn on top of marks.|

To create themes, new default values for many axis properties can be set using a [config](../config) object.


## <a name="orientation"></a>Axis Orientation Reference

Valid settings for the axis _orient_ parameter.

| Value          | Description |
| :------------- | :---------- |
| `left`         | Place a y-axis along the left edge of the chart.|
| `right`        | Place a y-axis along the right edge of the chart.|
| `top`          | Place an x-axis along the top edge of the chart.|
| `bottom`       | Place an x-axis along the bottom edge of the chart.|


## <a name="custom"></a>Custom Axis Encodings

Custom mark properties can be set for all axis elements using the _encode_ parameter. The addressable elements are:

- `axis` for the axis [group](../marks/group) mark,
- `ticks` for tick [rule](../marks/rule) marks,
- `grid` for gridline [rule](../marks/rule) marks,
- `labels` for label [text](../marks/text) marks,
- `title` for the title [text](../marks/text) mark, and
- `domain` for the axis domain [rule](../marks/rule) mark.

Each element accepts a set of visual encoding directives grouped into `enter`, `update`, `exit`, _etc._ objects as described in the [Marks](../marks) documentation. Mark properties can be styled using standard [value references](../types/#Value).

In addition, each encode block may include a string-valued `name` property to assign a unique name to the mark set, a boolean-valued `interactive` property to enable input event handling, and a string-valued (or array-valued) `style` property to apply default property values. Unless otherwise specified, title elements use a default style of `"guide-title"` and labels elements use a default style of `"guide-label"`.

Each axis tick, grid line, and label instance is backed by a data object with the following fields, which may be accessed as part of a custom visual encoding rule.

- `label` - the string label
- `value` - the data value

The following example shows how to set custom colors, thickness, text angle, and fonts. The `labels` encoding block also make legend labels responsive to input events, and changes the text color on mouse hover.

{: .suppress-error}
```json
"axes": [
  {
    "orient": "bottom",
    "scale": "x",
    "title": "X-Axis",
    "encode": {
      "ticks": {
        "update": {
          "stroke": {"value": "steelblue"}
        }
      },
      "labels": {
        "interactive": true,
        "update": {
          "text": {"signal": "format(datum.value, '+,')"},
          "fill": {"value": "steelblue"},
          "angle": {"value": 50},
          "fontSize": {"value": 14},
          "align": {"value": "left"},
          "baseline": {"value": "middle"},
          "dx": {"value": 3}
        },
        "hover": {
          "fill": {"value": "firebrick"}
        }
      },
      "title": {
        "update": {
          "fontSize": {"value": 16}
        }
      },
      "domain": {
        "update": {
          "stroke": {"value": "#333"},
          "strokeWidth": {"value": 1.5}
        }
      }
    }
  }
]
```

Custom text can be defined using the `"text"` property for `labels`. For example, one could define an ordinal scale that serves as a lookup table from axis values to axis label text.
