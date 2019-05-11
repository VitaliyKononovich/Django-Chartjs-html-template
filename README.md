# Django-Chartjs-html-template
This is my Chartjs html-template for generation different types of Chartjs charts in your Django application

## Getting Started
1. Copy the whole chartjs directory into your Django  project

2. Add it to your **INSTALLED_APPS** in settings.py:
```python
   INSTALLED_APPS = (
        '...',
        'chartjs',
    )
```

## Using it
A simple Bar Chart example

1. Add chart configuration options (as dictionary) to your view and past it into your web page template as parameter
```python
    from chartjs import Colors

    def index(request):
    colors = Colors()

    my_chart_config = { 'id': 'chart_performance', 'src_add': True, 'labels_plugin_rotation': -90,
               'labels_plugin_add': True, 'yAxies_label': 'Performance'}

    my_chart_config['data'] = {'labels': ["15-21.Jan", "22-28.Jan", "29-04.Feb", "05-11.Feb", "12-18.Feb", "19-25.Feb",
                                  "26-04.Mar", "05-11.Mar", "12-18.Mar", "19-25.Mar", "26-01.Apr", "02-08.Apr"],
                       'datasets': [
                           {'label': 'Anna', 'backgroundColor': colors.lightskyblue,
                            'data': [46, 49, 70, 63, 61, 55, 48, 47, 65, 95, 70, 97]},
                           {'label': 'Jane', 'backgroundColor': colors.slategray,
                            'data': [2, 1, 1, 1, 1, 3, 3, 0, 5, 0, 2, 0]},
                           {'label': 'Tom',
                            'backgroundColor': colors.hotpink,
                            'data': [0, 0, 0, 2, 2, 1, 0, 0, 0, 1, 0, 0]},
                           {'label': 'Dean',
                            'backgroundColor': colors.mediumslateblue,
                            'data': [9, 9, 11, 8, 14, 12, 16, 9, 11, 11, 17, 6]},
                           {'label': 'George',
                            'backgroundColor': colors.sandybrown,
                            'data': [0, 1, 1, 4, 2, 5, 0, 0, 1, 4, 8, 3]},
                           {'label': 'Jim',
                            'backgroundColor': colors.springgreen,
                            'data': [2, 5, 3, 3, 6, 3, 6, 2, 3, 9, 0, 1]}]}

    return render(request, 'index.html', {'my_chart_config': my_chart_config})
```
2. Add following line into content of your web page template in place you want to see the chart
```html
{% include "chartjs/chartjs.html" with chartjs=my_chart_config only  %}
```

** Chartjs configuration options
Chartjs dictionary object contains all parameters for configuration and styling chart. It may consist of
following KEY: VALUE attributes:
 * id (string) MANDATORY - chart id postfix which will be used for manipulation with chart (id='chart_'+id)
 * type (string) - type of chart. Default value is 'bar'
 * data (dict) - The dictionary object which represent chart data (labels and datasets)
 * stacked (bool) - Set True if you need stacked chart. Default value is False
 * height (int) - chart height. Default value is 120
 * width (int) - chart width
 * style (string) - style attributes which will be added into CANVAS tag
 * src_add (bool) - Set True if you need to add SCRIPT tag with src to Chart.bundle.min.js
 * src_alt (string) - Alternative path to Chart.bundle.min.js if needed. Applicable only  if src_add is True
 * legend_display (bool) - Set False if you need hide the chart legent. Default value is True
 * legend_position (string) - Position of the legend. Default value 'bottom'
 * legend_alt (dict) - Chart legend alternative configuration options. Replace everything in block legend
 * title_text (string) - Text displayed on the title of chart
 * title_alt (dict) - Chart title alternative configuration options. Replace everything in block title
 * yAxies_label (string) - The label which will be displayed on yAxies in the chart
 * yAxies_alt (list[dict]) - Chart yAxies alternative configuration options. Replace everything in block yAxies
 * xAxies_alt (list[dict]) - Chart xAxies alternative configuration options. Replace everything in block xAxies
 * tooltips_display (bool) - Set False if you need hide the chart tooltips. Default value is True
 * tooltips_alt (dict) - Chart tooltips alternative configuration options. Replace everything in block tooltips
 * labels_plugin_add (bool) - True if you need to add javascript file for data labels on the chart
 * labels_plugin_display (bool) - True if you need to add data labels on the chart
 * labels_plugin_color (string) - Set data labels color. Default value is '#000000'
 * labels_plugin_anchor (string) - Defines the position of the data label: start, center, end. Default value is 'end'
 * labels_plugin_rotation (int) - Rotation angle (in degrees) of the data label. Default value is 0 (no rotation)
 * labels_plugin_alt (dict) - Data Labels alternative configuration options. Replace everything in block datalabels

For more detailed information for configuration options please visit https://www.chartjs.org/docs/latest/
