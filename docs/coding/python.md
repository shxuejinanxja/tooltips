# Notes for python

## useful function

### zip

zip() function accept iterables as input and generate list of tuples.
for loop can unpack the list of tuples.
if two iterables are don't have same length, the length of the result list is min(iterables)

```python

l1=[1,2,3,4]
l2=["a","b","c"]
x1=zip(l1,l2)
print(min(len(l1),len(l2)))
print(type(x1))
print(list(x1))
for x,y in zip(l1,l2):
    print(x)
    print(y)

```

## concept

### metapromgramming

#### What is meta

Let make a table of employees as example

| name | wage |
| ---- | ---- |
| Jack | 1000 |

That table is data, this is metadata

| column | datatype | size |
| ------ | -------- | ---- |
| name   | String   | 64   |
| wage   | Int64    | 8    |

Metadata is the data of how the data is stored in the first table.

> the issue with instructions , though, is that once you write them, it's like they've been carved into stone, and so they are non-malleable. It would be more enabling if we could treat instructions as data and generate new instructions using code.
