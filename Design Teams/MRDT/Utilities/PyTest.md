# PyTest
## How to invoke pytest
When pytest is invoked it will execute all test files whose names follow the form `test_*.py` or `\*_test.py`

```Shell
pytest test_mod.py
pytest testing/
```

## Writing Tests
```python
def f():
	return 3

def test_function():
	assert f() == 4
```