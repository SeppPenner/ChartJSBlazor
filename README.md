# ChartJs interop with Blazor

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/Joelius300/ChartJSBlazor/blob/master/LICENSE.md)
[![GitHub issues](https://img.shields.io/github/issues/Joelius300/ChartJSBlazor.svg)](https://github.com/Joelius300/ChartJSBlazor/issues)
[![GitHub forks](https://img.shields.io/github/forks/Joelius300/ChartJSBlazor.svg)](https://github.com/Joelius300/ChartJSBlazor/network)
[![GitHub stars](https://img.shields.io/github/stars/Joelius300/ChartJSBlazor.svg)](https://github.com/Joelius300/ChartJSBlazor/stargazers)
[![Join the chat at https://gitter.im/ChartJSBlazor/community](https://badges.gitter.im/ChartJSBlazor/community.svg)](https://gitter.im/ChartJSBlazor/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![NuGet Downloads](https://img.shields.io/nuget/dt/ChartJs.Blazor.Fork.svg)](https://www.nuget.org/packages/ChartJs.Blazor.Fork/)

This is a Blazor Component that wraps [ChartJS](https://github.com/chartjs/Chart.js).
You can use the library in both client- and server-side projects.

# Status Update (end of life)

This repository has reached its end of life. All future development will be done in the [original repo](https://github.com/mariusmuntean/ChartJs.Blazor). You can find more information in [this pinned issue (#97)](https://github.com/Joelius300/ChartJSBlazor/issues/97).

## Introduction

This library is a modification of [this awesome library](https://github.com/mariusmuntean/ChartJs.Blazor) by [Marius Muntean](https://github.com/mariusmuntean/). 

Since it has now become apparent that the old repo is not maintained anymore, this project is continued and extended here. Since this is a project I'm working on in my free time, don't expect this to grow rapidly. There will often be differences between the docs and the actual code so I really advise you to go look at the [WebCore-project](https://github.com/Joelius300/ChartJSBlazor/tree/master/WebCore) which contains several examples that are up-to-date.

## Changelog

### Latest changes
**0.10.3:**

* Remove unnecessary highlight.js
* Lots of XML-documentation improvements
* Lots of bug-fixes
* Make the canvas-id read-only
* Rename classes to comply with the consistent naming conventions. From XXChartYY to XXYY.
* Lots of general improvements (refactoring, remove redundancies, etc)
* Implement [indexable options](https://www.chartjs.org/docs/latest/general/options.html#indexable-options)
* Update to preview9
* Rework Pie-Chart
* Remove Doughnut-Chart
* Rework Polar-Area-Chart

The detailed changelog can be found [here](https://github.com/Joelius300/ChartJSBlazor/blob/master/CHANGELOG.md).

#### How to update (breaking changes):
* Remove any assignment of the charts `CanvasId`. It will be handled automatically for you using a GUID string.
* Use pie-chart-classes anywhere you used dougnut chart and either manually set the `CutoutPercentage` to 50 or pass in `true` for the `PieOptions` constructor. It will yield the exact same results unless you have made manual changes to the chart.js-defaults using your own js.
* Many classes and properties have been removed, added, moved, renamed and more. You might have to add new using-directives and use the new class names. This is especially the case for the charts we've reworked (Pie (& Doughnut), Polar-Area, Line). Also a typo was fixed from `TimeTupel` to `TimeTuple`. The properties should all comply with the ones from chart.js written in PascalCase ([chart.js documentation](https://www.chartjs.org/docs/latest/)).  
For more details take a look at the detailed changelog, the chart.js-docs and our samples.
* **If you aren't referencing the js-interop-file dynamically using `_content`, you need to copy the new file manually from [here](https://github.com/Joelius300/ChartJSBlazor/blob/master/ChartJs.Blazor/wwwroot/ChartJsInterop.js) (there were two bug fixes).**

## Please keep in mind that this is still a preview. Expect breaking changes during the next releases. We're reworking all the charts because most of them contain errors and inconsistencies.

## Prerequisites

Don't know what Blazor is? Read [here](https://dotnet.microsoft.com/apps/aspnet/web-apps/client).

The prerequisites are:

1. [Visual Studio 2019 16.3](https://visualstudio.microsoft.com/downloads/)
2. [.NET Core 3](https://dotnet.microsoft.com/download/dotnet-core/3.0)


## Installation

There's a NuGet package available: [ChartJs.Blazor.Fork](https://www.nuget.org/packages/ChartJs.Blazor.Fork/)

Install from the command line:

```bash
dotnet add package ChartJs.Blazor.Fork
```

## Usage

For detailed instructions read the [Chart.Js](https://www.chartjs.org/docs/latest/charts/) documentation to understand how each chart works in detail or go to the [Wiki](https://github.com/Joelius300/ChartJSBlazor/wiki) to check the examples provided there. Since the example here and those in the wiki might be outdated very fast because of the many breaking changes, I would also advise you to go look at the [WebCore-project](https://github.com/Joelius300/ChartJSBlazor/tree/master/WebCore) in this repos where you can find some examples.  

Before you can start creating a chart with a config etc, you have to include some static assets to your project.

In your `_Host.cshtml` (server-side) or in your `index.html` (client-side) -file add this code to have `moment.js` with the locales:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.24.0/moment-with-locales.min.js"
        integrity="sha256-AdQN98MVZs44Eq2yTwtoKufhnU+uZ7v2kXnD5vqzZVo="
        crossorigin="anonymous">
</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.8.0/Chart.min.js"></script>
```

or this code if you want the bundled version of `Chart.Js`, but without the locales of `moment.js` (`moment.js` itself is then included in the bundle):

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.8.0/Chart.bundle.min.js"></script> <!--Contains moment.js for time axis-->
```

Furthermore, you need to include the js-interop and the css-file which enables responsiveness.  
Since those are static assets in the library, you should be able to reference them via your `_Host.cshtml`/`index.html`-file directly, without copying the files. You can do that using `_content` as seen below:

```html
<script src="_content/ChartJs.Blazor.Fork/ChartJsInterop.js" type="text/javascript" language="javascript"></script>
<link rel="stylesheet" href="_content/ChartJs.Blazor.Fork/ChartJsBlazor.css" />
```

**Disclaimer:**
Make sure to include the Blazor `_framework`-script before including the library-script. Otherwise, you will face the error: [Uncaught reference error: "Blazor is not defined at ChartJsInterop.js:5"](https://github.com/Joelius300/ChartJSBlazor/issues/94).
This issue is also documented in the [known issues page](https://github.com/Joelius300/ChartJSBlazor/wiki/Known-issues#uncaught-reference-error-blazor-is-not-defined-at-chartjsinteropjs5).

Now to creating the chart. Below is a simple example for a line-chart. Examples of the other chart types can be found in the [Wiki](https://github.com/Joelius300/ChartJSBlazor/wiki/Chart-types). You can find the examples also [here](https://github.com/Joelius300/ChartJSBlazor/blob/master/WebCore/Pages/) (the examples are probably more up to date in case the below code doesn't work).

The example covers a few static options, how to use a simple point-dataset and how to dynamically initialize and update the data displayed on the chart.

```csharp
@page "/SimpleLineLinearExample"
@using WebCore.Data
@using ChartJs.Blazor.Charts
@using ChartJs.Blazor.ChartJS.Common
@using ChartJs.Blazor.ChartJS.Common.Properties
@using ChartJs.Blazor.ChartJS.Common.Enums
@using ChartJs.Blazor.ChartJS.Common.Legends
@using ChartJs.Blazor.ChartJS.LineChart
@using ChartJs.Blazor.ChartJS.LineChart.Axes
@using ChartJs.Blazor.ChartJS.LineChart.Axes.Ticks
@using ChartJs.Blazor.Util.Color

<h2>Line Linear Chart</h2>
<ChartJsLineChart @ref="lineChartJs" Config="@lineConfig" Width="600" Height="300" />
<Button @onclick="UpdateChart">Add random point</Button>

@code
{
    LineConfig lineConfig;
    ChartJsLineChart lineChartJs;

    private LineDataset<Point> pointDataset;

    private Random rnd = new Random();

    protected override void OnInit()
    {
        lineConfig = new LineConfig
        {
            Options = new LineOptions
            {
                Responsive = true,
                Title = new OptionsTitle
                {
                    Display = true,
                    Text = "Simple Line Chart"
                },
                Legend = new Legend
                {
                    Position = Positions.Right,
                    Labels = new LegendLabelConfiguration
                    {
                        UsePointStyle = true
                    }
                },
                Tooltips = new Tooltips
                {
                    Mode = InteractionMode.Nearest,
                    Intersect = false
                },
                Scales = new Scales
                {
                    xAxes = new List<CartesianAxis>
                    {
                        new LinearCartesianAxis
                        {
                            ScaleLabel = new ScaleLabel
                            {
                                LabelString = "X-value"
                            }
                        }
                    },
                    yAxes = new List<CartesianAxis>()
                    {
                        new LinearCartesianAxis
                        {
                            ScaleLabel = new ScaleLabel
                            {
                                LabelString = "Random value"
                            }
                        }
                    }
                }
            }
        };


        pointDataset = new LineDataset<Point>()
        {
            BackgroundColor = ColorUtil.ColorString(0, 255, 0, 1.0),
            BorderColor = ColorUtil.ColorString(0, 0, 255, 1.0),
            Label = "Some values",
            Fill = false,
            PointBackgroundColor = ColorUtil.RandomColorString(),
            BorderWidth = 1,
            PointRadius = 3,
            PointBorderWidth = 1
        };

        pointDataset.AddRange(Enumerable.Range(1, 10).Select(i => new Point(i, rnd.Next(30))));

        lineConfig.Data.Datasets.Add(pointDataset);
    }

    private void UpdateChart()
    {
        pointDataset.Add(new Point(pointDataset.Data.Last().X +1, rnd.Next(rnd.Next(50))));
        lineChartJs.Update();
    }
}
```

For running on client-side Blazor there is currently a bug with JSON.NET tracked by this [issue](https://github.com/JamesNK/Newtonsoft.Json/issues/2020).
The known workaround is to include the following line in the parent component:

```csharp
private ReferenceConverter ReferenceConverter = new ReferenceConverter(typeof(PROBLEMATIC_COMPONENT));
```

where `PROBLEMATIC_COMPONENT` is a placeholder for the chart-component you're using inside this component (e.g. `ChartJsBarChart`, `ChartJsPieChart`, `ChartJsLineChart`, ..).

This issue is also documented in the [known issues page](https://github.com/Joelius300/ChartJSBlazor/wiki/Known-issues#missingmethodexception-when-using-client-side-blazor).

# Contributors
* [Joelius300](https://github.com/Joelius300)
* [SeppPenner](https://github.com/SeppPenner)
* [MindSwipe](https://github.com/MindSwipe)

# Contributing
We really like people helping us with the project. Nevertheless, take your time to read our contributing guidelines [here](https://github.com/Joelius300/ChartJSBlazor/blob/master/CONTRIBUTING.md).
