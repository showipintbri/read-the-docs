# JSON in Python
JSON is made up of "Key-Value Pairs". JSON supports a few data-types.

## Data Types

### String
```json
{"key": "value"}
```

### Number
```json
{"number": 1234}
```

### Boolean
```json
{"boolean": True}
```

### JSON Object
```json
{"json_object": {"key": "value", "number": 1234, "boolean": False}}
```

### Array
```json
{"array": ["item1", "item2", "item3"]}
```

### Null
```json
{"key": null}
```

## JSON Library (Python)
```python
import json

# some JSON:
x =  '{ "name":"John", "age":30, "city":"New York"}'

# parse x:
y = json.loads(x)

# the result is a Python dictionary:
print(y["age"]) 
```
