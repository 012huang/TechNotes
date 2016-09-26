# exec

官网对 exec 的解释:

```
This statement supports dynamic execution of Python code.
```


```py
python_source = """
SEVENTEEN = 17

def three():
    return 3
"""
global_namespace = {}
exec(python_source, global_namespace)

global_namespace['SEVENTEEN'] ==> 17
global_namespace['three'] ==> three(function)
```

```
python_source = """
one = 1

def get_name():
    name = person.get('name', '')
    return name
"""

namespace = {'person': {'name': 'peter'}}
exec(python_source, namespace)

In: namespace['person']
Out: {'name': 'peter'}

In: namespace['get_name']
Out: <function get_name>

In: getname = namespace['get_name']
In: getname()
Out: 'peter'

In: namespace.keys()
Out: ['__builtins__', 'person', 'get_name', 'one']
```


