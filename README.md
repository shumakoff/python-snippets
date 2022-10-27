## How to merge list of dictionaries into a single dictionary, putting values of keys into a list, i.e. turn
```
foo = [
    {'a': 'x', 'b': 'y', 'c': 'z'},
    {'a': 'j', 'c': 'z'}
]
```
into 
```
bar = {
    'a': ['x', 'j'],
    'b': ['y', None],
    'c': ['z', 'z']
}
```

```
bar = {
    k: [d.get(k) for d in foo]
    for k in set().union(*foo)
}
```
