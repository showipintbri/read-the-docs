# Dictionaries

Dictionaries are a data structure made up of '**keys**' and '**values**' created with the use of curly-braces '`{}`' in Python.

**Rules:**  

- Keys must be unique.
- If a Key needs more than 1 Value, you must use a list, nested dictionary, tuple or other iterable.

## Create a Dictionary

Before you can replace, update or delete any keys or values you must instantiate the dictionary.

### Empty dictionary:  

```python
my_dict = {}
```

### Or instantiate with keys and values:  

```python
my_dict = {'key1': 'value1'}
or
my_dict['key1'] = 'value1'
```

You can call the object directly or print the dictionary:

```python
>>> my_dict = {'key1': 'value1'}

>>> my_dict
{'key1': 'value1'}
```

Using `print()`:

```python
>>> my_dict = {'key1': 'value1'}

>>> print(my_dict)
{'key1': 'value1'}
```

## Add Key & Value to Existing Dictionary

- Key must be unique
- If Key is not unique Value will be overwritten.

### Start with a dictionary

```python
>>> my_dict = {'key1': 'value1'}
>>> my_dict
{'key1': 'value1'}
```

### Create a new Key with Value

```python
>>> my_dict['key2'] = 'value0'
>>> my_dict
{'key1': 'value1', 'key2': 'value0'}
```

### Update the Value for existing Key (overwrite)

```python
>>> my_dict['key2'] = 'value1'
>>> my_dict
{'key1': 'value1', 'key2': 'value1'}
```

## Add multiple Values to Key

Because a Value is a single object, I commonly use list's when I need a Key to contain multiple Values.

Convert your Key with a single value to a Key with a list object as a Value:

```python
>>> my_dict['key1'] = [my_dict['key1']]
>>> my_dict
{'key1': ['value1']}
```
