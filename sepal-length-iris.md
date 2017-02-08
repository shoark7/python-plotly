## Sepal length comparison between iris species

#### type : bar chart
#### date : 2017/02/08

```python
import plotly.offline as py
import plotly.graph_objs as go
import numpy as np

# open iris file
fp = open('/home/sunghwanpark/dataset/plotly-datasets/iris.csv')
original_text = fp.read()
original_data = original_text.split('\n')
col_name = original_data[0].split(',')
data = [i.split(',') for i in original_data[1:]]
data = np.array(data[:-1]) # numpy used!!
x = list(set(data[..., -1]))  # ['Iris-setosa', 'Iris-virginica', 'Iris-versicolor']
count_x = [original_text.count(a) for a in x]
y = np.zeros([3])

for row in data:
    if row[-1] == x[0]:
        y[0] += float(row[0]) # row[0] = 값, y[0]
    elif row[-1] == x[1]:
        y[1] += float(row[0])
    else:
        y[2] += float(row[0])


y = [n / count_x[i] for i, n in enumerate(y)] # 이제 각 종 간의 Sepal length 값을 알게 되었다.


data = [go.Bar(
        x=x, y=y,
        marker= {
            'color': 'red',
            'line': {
                'color': 'black',
                'width': 2
            }
        },
        opacity=0.7
            )]

layout = go.Layout(
    title='Sepal length of each iris species',
    xaxis={
        'title': 'Specis of iris'
    },
    yaxis={
        'title': 'Length of sepal'
    },
    paper_bgcolor='rgba(245, 246, 249, 1)',
    annotations=[{
        'x':xi, 'y':yi,
        'text':str(yi),
        'xanchor':'center',
        'yanchor':'bottom',
        'showarrow': False
    } for xi , yi in zip(x, y)]
)

fig = go.Figure(data=data, layout=layout)
py.plot(fig, filename='sepal-length-comparison')
```
오늘 numpy를 처음 배워서 아직 잘 활용은 못한다. 하지만 더 익숙해질듯

![graph](../images/sepal-length-comparsion.png  "graph")