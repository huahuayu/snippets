[//title]: (use-python-sympy-to-solve-equation)
[//englishtitle]: (use-python-sympy-to-solve-equation)
[//category]: (python,snippet,sympy)
[//tags]: (python,snippet)
[//createtime]: (20210510)
[//updatetime]: (20210510)

```python
import sympy as sym
import time
start = time.time()
# variable symbol
x,y = sym.symbols('x,y')
# constant symbol
A = 107420270715474691
B = 46565854106545866009963
C = 1000000000000000
D = 423977575939714546100
eq1 = sym.Eq((A + 0.997 * x) * (B - y), A * B) # (A + 0.997 * x) * (B - y) = A * B
eq2 = sym.Eq((A + 0.997 * x + C) * (B - y - D), (A + 0.03 * x) * B)
result = sym.solve([eq1,eq2], [x,y])
print(result)
print(type(result)) # list
print(type(result[0])) # tuple
print(result[0][0]) # x1
print(result[1][0]) # x2
print(time.time() - start)
```

## context

everything is good except time consuming, about 0.34s for my test.
