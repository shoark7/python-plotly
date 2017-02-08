## Binomial Distribution graph

#### type : bar
#### date : 2017/02/08

Flipping a coin 100 times..

```python
"""Binomial distribution"""
# 이항분포

p = 0.5
n = 100

def factorial(n):
    start = 1
    result = 1
    while start <= n:
        result *= start
        start += 1
        
    return result

def combination_count(n, k):
    return factorial(n) // factorial(k) // factorial(n - k)

# combination(10, 3)

def B(n, p, x):
    return combination_count(n, x) * (p ** x) * ((1-p) ** (n - x))

x = np.arange(101)
y = [B(n, p, j) for j in x]


data =[go.Bar(
    x=x, y=y,
    marker={
        'color': 'blue',
        'line': {
            'color': 'blue',
            'width': 1.5,
        }
    },
    opacity=0.4
)]

layout = go.Layout(
    title='Binomial Distribution',
    xaxis= {
        'title': 'Number of heads from flipping a coin 100 times',
    },
    yaxis= {
        'title': 'Possibility',
    },
)

fig = go.Figure(data=data, layout=layout)

py.plot(fig, filename='Binomial-distribution-bar')

```
![graph](https://github.com/shoark7/python-plotly/blob/master/images/binomial-bar.png)
