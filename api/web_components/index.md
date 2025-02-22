---
layout: default
title: Web Components
parent: API
nav_order: 20
has_children: true
published: false
---
# Data Commons Web Components

Embed [Data Commons](https://datacommons.org)
[statistical variable](https://datacommons.org/tools/statvar) observation
visualizations in your web application.

<img
  src="/assets/images/web_components/all.png"
  style="width: 100%; max-width: 1024px;"
/>

## Usage

Include `datacommons.js` in your html's
`<head>...</head>` tag. Then use Data Commons
[web component](https://developer.mozilla.org/en-US/docs/Web/API/Web_components)
tags (e.g. `datacommons-line`) to add embedded data visualizations.

For example, to embed a line chart:

```html
<html>
  <head>
    <script src="https://datacommons.org/datacommons.js"></script>
  </head>
  <body>
    <datacommons-line
      header="US Population Over Time"
      place="country/USA"
      variables="Count_Person"
    ></datacommons-line>
  </body>
</html>
```

See a live version of this example you can play around with in
[Playground](https://lit.dev/playground/#gist=c0c88276739f4f6061807cc943937a14)
([source](/assets/examples/web-components/line-chart.html)).

## Components

- [datacommons-bar](/api/web_components/bar)
- [datacommons-highlight](/api/web_components/highlight)
- [datacommons-gauge](/api/web_components/gauge)
- [datacommons-line](/api/web_components/line)
- [datacommons-map](/api/web_components/map)
- [datacommons-pie](/api/web_components/pie)
- [datacommons-ranking](/api/web_components/ranking)
- [datacommons-scatter](/api/web_components/scatter)
- [datacommons-slider](/api/web_components/slider)

## Code Playground Examples

- [Static page with all chart types playground](https://lit.dev/playground/#gist=822ce6018bb41113c866d703760c1def)
  ([source](/assets/examples/web-components/all-charts.html))
- [Dynamically updating charts playground](https://lit.dev/playground/#gist=9e3ac88e162248f849dd276ff5895ad0)
  ([source](/assets/examples/web-components/dynamic-map.html))

## Variables and places

Data Commons web components visualize statistical variables about one or more
places. Variables and places are identified by
[Data Commons Identifiers](/glossary.html#dcid), or
[DCID](/glossary.html#dcid)s.

To find the [DCID](/glossary.html#dcid) of a place or variable:

1. Browse all variables with the
   [Data Commons Statistical Variable Explorer](https://datacommons.org/tools/statvar).

2. Search for places and variables with the
   [Data Commons Search](https://datacommons.org/search) page.

3. Use the [Data Commons Graph Browser](https://datacommons.org/browser) to
   understand the relationship between entities.

### Finding DCIDs Examples

#### Example #1: Finding places available for a variable

Inspecting
[Health / Health Insurance (Household) / No Health Insurance / Households Without Health Insurance](https://datacommons.org/tools/statvar#sv=Count_Household_NoHealthInsurance)
shows us that the statistical variable `Count_Household_NoHealthInsurance` is
available in the `United States` ([DCID](/glossary.html#dcid): `country/USA`) at
`State`, `County`, and `City` levels.

<img src="/assets/images/web_components/stat-var-explorer.png" width="600"/>

#### Example #2: Finding place DCIDs

The graph browser [country/USA](https://datacommons.org/browser/country/USA)
page shows the [DCID](/glossary.html#dcid)s for all US states and territories.

<img src="/assets/images/web_components/graph-explorer.png" width="600"/>

## Styling

Custom styles are supported through
[CSS shadow parts](https://developer.mozilla.org/en-US/docs/Web/CSS/::part).

<div markdown="span" class="alert alert-danger" role="alert">
  <span class="material-icons exclamation-icon">priority_high</span>
  <b>IMPORTANT:</b><br />
  Escape forward slashes in `::part()` names, like in DCIDs.
</div>

| CSS `::part`                          | Description                                                                                                 | Components                 |
| ------------------------------------- | ----------------------------------------------------------------------------------------------------------- | -------------------------- |
| `container`                           | Chart container element                                                                                     | All                        |
| `legend`                              | Chart legend                                                                                                | `bar`, `line`, `map`,`pie` |
| `place-path`                          | Geo boundary                                                                                                | `map`                      |
| `place-path-<dcid>`                   | Geo boundary for a particular place. Example: `place-path-geoId\/12` \*                                     | `map`                      |
| `series`                              | Series data (line, bar, lollipop, etc)                                                                      | `bar`, `line`. `pie`       |
| `series-place-<dcid>`                 | Series data for a particular place. Example: `series-place-geoId\/12` \*                                    | `bar`, `line`. `pie`       |
| `series-place-<dcid>-variable-<dcid>` | Series data for a particular place and variable. Example: `series-place-geoId\/12-variable-Count_Person` \* | `bar`, `line`              |
| `series-variable-<dcid>`              | Series data for a variable. Example: `series-place-variable-Count_Person`                                   | `bar`, `line`. `pie`       |
| `header`                              | Chart title                                                                                                 | All                        |
| `subheader`                           | Chart subtitle (if provided in `slot="subheader"`)                                                          | All                        |
| `footer`                              | Chart footer (if provided in `slot="footer"`)                                                               | All                        |
| `x-axis`                              | X-axis line                                                                                                 | `bar`, `line`              |
| `x-axis-text`                         | X-axis label text                                                                                           | `bar`, `line`              |
| `x-axis-tick`                         | X-axis tick mark                                                                                            | `bar`, `line`              |
| `y-axis-text`                         | Y-Axis label text                                                                                           | `bar`, `line`              |
| `y-axis-tick`                         | Y-Axis tick mark                                                                                            | `bar`, `line`              |

Additionally, the following css variables are supported:

| CSS variable                | Description                                                | Default            |
| --------------------------- | ---------------------------------------------------------- | ------------------ |
| `--dc-headings-font-family` | Font family for web component headings (`h1` through `h6`) | `Google Sans`      |
| `--dc-font-family`          | Font family for web component body text                    | `Google Sans Text` |

### Styling Example

See a live version of this example you can play around with in
[Playground](https://lit.dev/playground/#gist=719f5d71c2823ac3e58f504cb6ceccd3)
([source](/assets/examples/web-components/map-styles.html)).

```html
<html>
  <head>
    <style>
      #styled-map {
        --dc-headings-font-family: monospace;
      }
      #styled-map::part(container) {
        border-radius: 10px;
        border: 1px solid #f5f5f5;
        box-shadow: 1px 2px 6px rgba(3, 7, 18, 0.04),
          5px 8px 25px rgba(3, 7, 18, 0.08);
      }
      #styled-map::part(legend) {
        border: 1px solid #e1e1e1;
        padding: 5px 8px;
        border-radius: 10px;
      }
      #styled-map::part(title) {
        font-weight: 200;
        font-size: 16px;
        margin-bottom: 16px;
        color: #111a1b;
      }
      #styled-map::part(place-path) {
        fill: #e9e9e9;
      }
      #styled-map::part(place-path-geoId\/12),
      #styled-map::part(place-path-geoId\/13),
      #styled-map::part(place-path-geoId\/06) {
        fill-opacity: 1;
        fill: #e76f51;
        stroke: #b72a53;
        stroke-width: 2px;
      }
    </style>
  </head>
  <body>
    <datacommons-map
      id="styled-map"
      header="Three most populous US states"
      parentPlace="country/USA"
      childPlaceType="State"
      variable="Count_Person"
    ></datacommons-map>
  </body>
</head>
```

## License

[Apache 2.0](https://github.com/datacommonsorg/website/blob/master/packages/web-components/LICENSE)

## Support

For general questions or issues, please open an issue on our
[issues](https://github.com/datacommonsorg/website/issues) page. For all other
questions, please send an email to `support@datacommons.org`.
