# Command Line Interface using python-fire

Fire provides a truly simple way to get started with command line
applications. It is python friendly and can expose any python object
as a command line interface

To get started
`pip install fire`

Docs: [read the docs](https://github.com/google/python-fire/blob/master/docs/guide.md)

### Simple Use Case 1

Expose a function in your module as CLI

```python
   1   │ import fire
   2   │
   3   │ def human_population(year=2021):
   4   │   if year == 2021:
   5   │     return 8000000000
   6   │
   7   │   return "unknown"
   8   │
   9   │ if __name__ == "__main__":
  10   │   fire.Fire(human_population)
```

### Output
```bash
python module-example.py
8000000000
```

## Simple Use Case 2

Expore your class as CLI

```python
   1   │ import fire
   2   │
   3   │ database = {
   4   │   "United States": {
   5   │      "GDP": "20 Trillion",
   6   │      "pop": 330000000
   7   │    },
   8   │   "India": {
   9   │      "GDP": "5 Trillion",
  10   │      "pop": 1500000000
  11   │    },
  12   │
  13   │ }
  14   │
  15   │
  16   │ class Census:
  17   │   """This class handles the census for the UN"""
  18   │
  19   │   def __init__(self):
  20   │     self.countries = database
  21   │
  22   │   def info(self, country, attribute):
  23   │     res = self.countries[country.title()].get(attribute)
  24   │     return res
  25   │
  26   │
  27   │ if __name__ == "__main__":
  28   │   """
  29   │   use this as key based interface to the dict
  30   │   outputs
  31   │   $python component-example.py India
  32   │   GDP: 5 Trillion
  33   │   pop: 1500000000
  34   │   """
  35   │   # fire.Fire(database)
  36   │
  37   │   """
  38   │   Expose the class as an Interface
  39   │   """
  40   │   fire.Fire(Census)
```

### Output
```bash
python component-example.py info "united states" GDP
20 Trillion
```