# Watercrawl Plugin

[![PyPI version](https://badge.fury.io/py/watercrawl-plugin.svg)](https://badge.fury.io/py/watercrawl-plugin)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Description

WaterCrawl plugin is a Python package that provides a base for creating plugins for the WaterCrawl web crawling
framework. It offers abstract classes and interfaces to standardize plugin development with support for input validation,
pipeline processing, and middleware integration.

## Features

- Abstract base classes for plugin development
- JSON Schema-based input validation
- Pipeline processing support
- Spider and Downloader middleware integration
- Cached property utilities
- Type hints and comprehensive documentation

## Installation

You can install the WaterCrawl plugin package using pip:

```bash
pip install watercrawl-plugin
```

## Usage

Here's a comprehensive guide on how to create a WaterCrawl plugin:

### 1. Import Required Classes

```python
from watercrawl_plugin import AbstractInputValidator, AbstractPlugin, BasePipeline
```

### 2. Create Input Validator

Define your plugin's configuration schema using JSON Schema:

```python
class MyInputValidator(AbstractInputValidator):
    @classmethod
    def get_json_schema(cls):
        return {
            "title": "My Plugin",
            "description": "Plugin description",
            "type": "object",
            "properties": {
                "model_name": {
                    "title": "Model Name",
                    "type": "string",
                    "default": "default-model",
                    "enum": ["model-1", "model-2"],
                    "ui": {
                        "widget": "select",
                        "options": [
                            {"label": "Model 1", "value": "model-1"},
                            {"label": "Model 2", "value": "model-2"},
                        ]
                    },
                },
                "config": {
                    "title": "Configuration",
                    "type": "object",
                    "ui": {
                        "widget": "json-editor"
                    }
                }
            }
        }

    def get_model(self):
        return self.data.get('model_name', 'default-model')

    def get_config(self):
        return self.data.get('config', {})
```

### 3. Create Pipeline Class

Implement the processing logic:

```python
class MyPipeline(BasePipeline):
    def get_validator(self, spider):
        return spider.plugin_validators[MyPlugin.plugin_key()]

    def process_item(self, item, spider):
        validator = self.get_validator(spider)
        if not validator or not validator.data:
            return item

        try:
            # Process the item using validator configuration
            processed_data = self.process_data(
                item,
                model=validator.get_model(),
                config=validator.get_config()
            )
            item['processed_data'] = processed_data
        except Exception as e:
            raise RuntimeError(f"Error processing item: {e}")

        return item
```

### 4. Create Plugin Class

Define your main plugin class:

```python
class MyPlugin(AbstractPlugin):
    @classmethod
    def plugin_key(cls) -> str:
        return "my_plugin"

    @classmethod
    def get_pipeline_classes(cls) -> dict:
        return {
            'my_package.MyPipeline': 500,  # Priority 500
        }

    @classmethod
    def get_input_validator(cls) -> Type[MyInputValidator]:
        return MyInputValidator

    @classmethod
    def extended_fields(cls):
        return ["processed_data"]

    @classmethod
    def get_spider_middleware_classes(cls) -> dict:
        return {}

    @classmethod
    def get_downloader_middleware_classes(cls) -> dict:
        return {}

    @classmethod
    def get_author(cls) -> str:
        return "Your Name"

    @classmethod
    def get_version(cls) -> str:
        return "1.0.0"

    @classmethod
    def get_name(cls) -> str:
        return "MyPlugin"

    @classmethod
    def get_description(cls) -> str:
        return "Plugin description"
```

## API Reference

### AbstractPlugin

Base class for plugins with required methods:

- `plugin_key()`: Unique identifier for the plugin
- `get_pipeline_classes()`: Dictionary of pipeline classes with priorities
- `get_input_validator()`: Returns the input validator class
- `extended_fields()`: List of fields added by the plugin
- `get_spider_middleware_classes()`: Spider middleware classes
- `get_downloader_middleware_classes()`: Downloader middleware classes
- `get_author()`, `get_version()`, `get_name()`, `get_description()`: Plugin metadata

### AbstractInputValidator

Base class for input validation:

- `get_json_schema()`: Returns JSON Schema for configuration
- Custom getter methods for configuration values
- Access to validation data through `self.data`

### BasePipeline

Base class for item processing:

- `process_item(item, spider)`: Main processing method
- `get_validator(spider)`: Get plugin validator instance
- Support for cached properties and error handling

## Contributing

We welcome contributions! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
