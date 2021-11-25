# Python
This is one location for all things python that I've had to look up, or forgotten or had a bookmark for in my browser. This is **NOT** intended to be the worlds single reference python resource, instead it serves me directly. If you'd like to submit a correction or contribute, PR's are welcomed. I tried to be original and unique in most of my examples and code, this was not to rip-off anyone elses examples or work. There are countless sites over the years I've used for reference and python script text files on my desktop of code I'll never remember where it all came from.

Thank you to everyone who puts code and examples out there on the internet. Here's my little place to aggregate what I use and give back. 

## Dictionaries
Dictionaries are a data structure made up of 'keys' and 'values' created with the use of curly-braces '`{}`' in Python.

**Rules:**
- Keys must be unique.
- If a Key needs more than 1 Value, you must use a list, nested dictionary, tuple or other iterable.

### Create a Dictionary
Before you can replace, update or delete any keys or values you must instantiate the dictionary.

- Empty dictionary:  
  ```
  my_dict = {}
  ```
- Or instantiate with keys and values:  
  ```
  my_dict = {'key1': 'value1'}
  or
  my_dict['key1'] = 'value1'
  ```

You can call the object directly or print the dictionary:
```
>>> my_dict = {'key1': 'value1'}

>>> my_dict
{'key1': 'value1'}
```
Using `print()`:
```
>>> my_dict = {'key1': 'value1'}

>>> print(my_dict)
{'key1': 'value1'}
```

### Add Key & Value to Existing Dictionary
- Key must be unique
- If Key is not unique Value will be overwritten.

```
# Start with a dictionary
>>> my_dict = {'key1': 'value1'}
>>> my_dict
{'key1': 'value1'}

# Create a new Key with Value
>>> my_dict['key2'] = 'value0'
>>> my_dict
{'key1': 'value1', 'key2': 'value0'}

# Update the Value for existing Key (overwrite)
>>> my_dict['key2'] = 'value1'
>>> my_dict
{'key1': 'value1', 'key2': 'value1'}
```

### Add multiple Values to Key
I commonly use list's when I need a Key to contain multiple Values.

Convert your Key with a single value to a Key with a list object as a Value:
```
>>> my_dict['key1'] = [my_dict['key1']]
>>> my_dict
{'key1': ['value1']}
```

