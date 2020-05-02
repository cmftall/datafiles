<h1>Settings</h1>

For libraries that wish to temporarily alter any of the previously described behavior, a handful of settings can be set at the module level. All boolean settings default to `True` unless otherwise noted.

# `HIDE_INITIALIZATION_LOGGING`

By default, logging in the `@datafile()` calls is disabled to avoid prematurely configuring logging for clients.
If this information is needed to debug a complex issue, enable it as follows:

```python
import datafiles

datafiles.settings.HIDE_INITIALIZATION_LOGGING = False
```

# `HIDE_TRACEBACK_IN_HOOKS`

When an exception occurs in patched method, this traceback is hidden by default for `pytest`. If this information is needed to debug a complex issue, enable it as follows:

```python
import datafiles

datafiles.settings.HIDE_TRACEBACK_IN_HOOKS = False
```

# `HOOKS_ENABLED`

When running unit tests for a library using `datafiles`,
it can be helpful to disable automatic loading/saving of models for performance and to avoid writing files to disk:

```python
import datafiles

def pytest_runtest_setup(item):
    """Disable file storage during unit tests."""
    datafiles.settings.HOOKS_ENABLED = False
```

# `INDENT_YAML_BLOCKS`

In `datafiles >= 0.4`, YAML blocks are now indented by default, like so:

```yaml
items:
  - 1
  - 2
  - 3
```

To make it easier to upgrade to this version, a library can disable this functionality:

```python
import datafiles

datafiles.settings.INDENT_YAML_BLOCKS = False
```

to produce YAML like:

```yaml
items:
  - 1
  - 2
  - 3
```

# `YAML_LIBRARY`

This setting controls the underlying YAML library used to read and write files. The following options are available:

- `'ruamel.yaml'` (default)
- `'PyYAML'`
