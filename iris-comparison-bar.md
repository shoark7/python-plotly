## Iris comparison graph

#### type: bar
#### date: 2017/02/09

```python
"""Day 3"""
import numpy as np
import plotly.offline as py
import plotly.graph_objs as go

# Data trim part

fp = open('/home/sunghwanpark/dataset/plotly-datasets/iris.csv')
original_text = fp.read()
splited_text_by_row = original_text.split('\n')
columns = splited_text_by_row[0].split(',')      # ['SepalLength', 'SepalWidth', 'PetalLength', 'PetalWidth', 'Name']

trimmed_text_by_row = [row.split(',') for row in splited_text_by_row]
trimmed_text_by_row = trimmed_text_by_row[1:-1]  # Remove a column name row and a redundant row.

data = np.array(trimmed_text_by_row)            # (150, 5) shape. 50 samples for each specie.
species = sorted(list(set(data[..., -1])))           # ['Iris-setosa', 'Iris-versicolor', 'Iris-virginica']. Sort specy in alphabetical order.
species_count = [original_text.count(specie) for specie in species]

sl = [0, 0, 0,]      # Sepal Length
sw = [0, 0, 0,]     # Sepal Width
pl = [0, 0, 0,]      # Petal Length
pw = [0, 0, 0,]     # Petal Width

for row in data:
    index = species.index(row[-1])   # Last element of each row is its specie
    sl[index] += float(row[0])
    sw[index] += float(row[1])
    pl[index] += float(row[2])
    pw[index] += float(row[3])

sl = [round(number / species_count[i], 2) for i, number in enumerate(sl)]
sw = [round(number / species_count[i], 2) for i, number in enumerate(sw)]
pl = [round(number / species_count[i], 2) for i, number in enumerate(pl)]
pw = [round(number / species_count[i], 2) for i, number in enumerate(pw)]

x_cord = [0, 1, 2,
         ]
# graph part
trace1 = go.Bar(
    x=species, y=sl,
    name='Sepal Length',
    marker={
        'color': 'red'
    },
    opacity=0.8,
)

trace2 = go.Bar(
    x=species, y=sw,
    name='Sepal Width',
    marker={
        'color': 'crimson',
    },
    opacity=0.8,
)

trace3 = go.Bar(
    x=species, y=pl,
    name='Petal Length',
    marker={
        'color': 'blue'
    },
    opacity=0.8
)

trace4 = go.Bar(
    x=species, y=pw,
    name='Petal Width',
    marker={
        'color': 'violet',
    },
    opacity=0.8,
)

data = [trace1, trace2, trace3, trace4]
layout = go.Layout(
    barmode='group',
    paper_bgcolor='ivory',
)

annotations = []

annotations1 = [dict(
            x=xi-0.3,
            y=yi,
            text=str(yi),
            xanchor='auto',
            yanchor='bottom',
            showarrow=False,
        ) for xi, yi in zip(x_cord, sl)]

annotations2 = [dict(
            x=xi-0.1,
            y=yi,
            text=str(yi),
            xanchor='auto',
            yanchor='bottom',
            showarrow=False,
        ) for xi, yi in zip(x_cord, sw)]

annotations3 = [dict(
            x=xi+0.1,
            y=yi,
            text=str(yi),
            xanchor='auto',
            yanchor='bottom',
            showarrow=False,
        ) for xi, yi in zip(x_cord, pl)]

annotations4 = [dict(
            x=xi+0.3,
            y=yi,
            text=str(yi),
            xanchor='auto',
            yanchor='bottom',
            showarrow=False,
        ) for xi, yi in zip(x_cord, pw)]

annotations = annotations1 + annotations2 + annotations3 + annotations4
layout['annotations'] = annotations

fig = go.Figure(data=data, layout=layout)
py.plot(fig, filename='specie-comparison')
```
![graph](https://github.com/shoark7/python-plotly/blob/master/images/iris-comparison-bar2.png)
