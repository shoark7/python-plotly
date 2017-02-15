## Sepal width and Sepal length comparsion

#### type : scatter
#### date : 2017/02/15


```python
"""
Our mission today is to compare sepal length and sepal width between species.
Graph will be scatter graph, x is sepal width, and y is sepal length. Cool.

And also average poing of each specie will be drawn too. Points of them would be bigger than others.

Now I can use basic numpy and pandas
"""

import numpy as np
import pandas as pd
import plotly.plotly as py
import plotly.graph_objs as go

dataset = pd.read_csv('/very/famouse/iris.csv')
dataset.head()

# sepal_length and sepal width comparison between species

df1 = dataset.copy()

mean_sepal_length = df1.groupby('Name')['SepalLength'].mean()
mean_sepal_width = df1.groupby('Name')['SepalWidth'].mean()
species = df1.Name.unique()

fig = {
    'data': [
        {
            'x': df1['SepalWidth'][df1['Name'] == specie], 'y': df1['SepalLength'][df1['Name'] == specie],
            'mode': 'markers', 'text': specie,
            'name': specie,
            'marker': {
                'size': 8,
                'symbol': 'square',
            },
            'opacity': 0.5,
            
        } for specie in species],
    
    'layout': {
        'title': 'Sepal length and Sepal Width comparison between species',
        'xaxis': {
            'title': 'Sepal Width',
        },
        'yaxis': {
            'title': 'Sepal Length',
        },
        'paper_bgcolor': 'rgba(10, 123, 100, 0.1)'
    }
}

mean_data = {
    'x': mean_sepal_width, 'y': mean_sepal_length,
    'name': species,
    'mode': 'markers', 
    'text': ['mean of ' + specie for specie in species],
    'marker': {
        'color': ['blue', 'orange', 'green'],
        'size': 15,
    },
    'showlegend': False,
}

fig['data'].append(mean_data)
url = py.plot(fig, filename='specie-comparison-scatter1')
```

![graph](https://github.com/shoark7/python-plotly/blob/master/images/specie-comparison-scatter1.png)