## First time series graph


#### type : line graph
#### date : 2017/02/14

```python
import numpy as np
import pandas as pd
import plotly.plotly as py
import plotly.graph_objs as go

dataset = pd.read_csv('/home/location/of/image.csv', parse_dates=['Date'], index_col='Date')

x = dataset.index # date

alphabet_range = [chr(ord('A') + i) for i in range(7)]
expression = ['trace_{} = dataset["{}"]'.format(c.lower(), c) for c in alphabet_range]
for ex in expression:
    exec(ex)

trace1 = go.Scatter(
    x=x, y=trace_a,
    mode='lines',
    name='A'
)

trace2 = go.Scatter(
    x=x, y=trace_b,
    mode='lines',
    name='B',
)

trace3 = go.Scatter(
    x=x, y=trace_c,
    mode='lines',
    name='C'
)

trace4 = go.Scatter(
    x=x, y=trace_d,
    mode='lines',
    name='D'
)

trace5 = go.Scatter(
    x=x, y=trace_e,
    mode='lines',
    name='E'
)

trace6 = go.Scatter(
    x=x, y=trace_f,
    mode='lines',
    name='F'
)

trace7 = go.Scatter(
    x=x, y=trace_g,
    mode='lines',
    name='G'
)

data = [trace1, trace2, trace3, trace4, trace5, trace6, trace7]

layout = go.Layout(
    title='timeseries graph of 7 data',
    xaxis={
        'title': 'time',
        'tickformat': '%Y-%m-%d',
        'fixedrange': True,
        'tickangle': 45
    },
    yaxis={
        'title': 'value',
        'fixedrange': True
    },
    paper_bgcolor= 'rgba(0, 0, 0, 0.2)',
    
)

fig = go.Figure(data=data, layout=layout)
py.plot(fig, filename='timeseries-graph')
```
![graph](https://github.com/shoark7/python-plotly/blob/master/images/timeseries-graph.png)