


Complex Network Analysis
=============================
Many aspects of a chart's appearance can be configured at the top level using


<br>

Altair Themes
-------------

The themes registry consists of functions which define a specification dictionary
that will be added to every created chart.
For example, the default theme configures the default size of a single chart:

    >>> import altair as alt
    >>> default = alt.themes.get()
    >>> default()
    {'config': {'view': {'continuousWidth': 400, 'continuousHeight': 300}}}

<br>

Changing the Theme
~~~~~~~~~~~~~~~~~~
If you would like to enable any other theme for the length of your Python session,
you can call ``alt.themes.enable(theme_name)``.
For example, Altair includes a theme in which the chart background is opaque
rather than transparent:

<br>

Defining a Custom Theme
~~~~~~~~~~~~~~~~~~~~~~~
The theme registry also allows defining and registering custom themes.
A theme is simply a function that returns a dictionary of default values
to be added to the chart specification at rendering time, which is then
registered and activated.

For example, here we define a theme in which all marks are drawn with black
fill unless otherwise specified:

::

    import altair as alt
    from vega_datasets import data

    # define the theme by returning the dictionary of configurations
    def black_marks():
        return {
            'config': {
                'view': {
                    'height': 300,
                    'width': 400,
                },
                'mark': {
                    'color': 'black',
                    'fill': 'black'
                }
            }
        }

    # register the custom theme under a chosen name
    alt.themes.register('black_marks', black_marks)

    # enable the newly registered theme
    alt.themes.enable('black_marks')

    # draw the chart
    cars = data.cars.url
    alt.Chart(cars).mark_point().encode(
        x='Horsepower:Q',
        y='Miles_per_Gallon:Q'
    )

<br>

If you want to restore the default theme, use::

   alt.themes.enable('default')


For more ideas on themes, see the `Vega Themes`_ repository.


.. _Vega Themes: https://github.com/vega/vega-themes/