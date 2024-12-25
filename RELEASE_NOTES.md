# Release Notes - Watercrawl Plugin v0.0.2

## What's New

- Check API Changes for more information

## Improvements

- First version no bug

## Bug Fixes

- First version no bug

## API Changes

- The [AbstractPlugin](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py) class now includes methods:
  - [get_name()](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py): Returns the name of the plugin (defaults to the class name)
  - [get_description()](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py): Returns the description of the plugin (defaults to the class docstring)
  - [get_version()](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py): Returns the version of the plugin (needs to be implemented by subclasses)
  - [get_author()](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py): Returns the author of the plugin (needs to be implemented by subclasses)

- The [AbstractInputValidator](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py) class now includes:
  - A [validate()](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py) method that subclasses should implement to define input validation logic
  - An [is_valid()](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py) method to check if the input is valid
  - An [add_error()](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py) method to add validation errors

- The [AbstractPipelinePlugin](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/base.py) class now includes:
  - A [process_item()](https://github.com/watercrawl/watercrawl-plugin/blob/0.0.2/src/watercrawl_plugin/pipeline.py) method that subclasses should implement to define item processing logic

# Release Notes - Watercrawl Plugin v0.1.0

## What's New

- Major version update with improved plugin architecture
- Added new utility functions for enhanced plugin development
- Removed deprecated pipeline module

## Improvements

- Enhanced plugin base class with better abstractions
- Added utility functions for common plugin operations
- Improved code organization and structure

## Bug Fixes

- Fixed various minor issues in the base plugin implementation

## API Changes

- Removed deprecated pipeline module
- Enhanced AbstractPlugin class with improved functionality
- Added new utility functions for plugin development
