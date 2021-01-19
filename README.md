# pylogplus
A simple yet powerful logging library for Python.

## Getting started

### Downloading the library
There are two main ways to get the library, either by compressing from source or downloading from the [Releases page](https://github.com/coredoescode/pylogplus/releases). If you download from releases, you will have the most stable build. Compressing from source will give you the latest features that have not been released yet. It is recommended to download from releases.

#### Compressing from source
Commands are shown for windows. Use the commands for your platform.
```bash
git clone https://github.com/coredoescode/pylogplus
cd pylogplus
mkdir build
copy build-config-example.py build/build-config.py
python build.py build/build-config.py
```
Once the build completes, the library will be placed in build/pylogplus. Copy the ENTIRE pylogplus directory to your project directory. A fresh configuration file will be placed in build/pylogplus.

### Using the library
#### Initializing the library
First off, import the library. Use this import statement:
```python
from pylogplus.pylogplus import PyLogPlus
```
The PyLogPlus class is known as a *registry class*. Registry classes always have to be initialized. Initialize the library as follows:
```python
pylogplus = PyLogPlus()
pylogplus.init(print)
```
The `pylogplus.init()` method takes one input, and it is the method that should be used to output logs. Here we use the 'print' method. The library expects a function that takes in one string as an argument.
While the library is initializing, some messages will appear in the console.
```python
PyLogPlus initializing
PyLogPlus is ready
```
These messages can be disabled in the [Configuration File.](https://github.com/coredoescode/pylogplus/wiki/Configuration-File)
#### Creating a logger
An essential part of PyLogPlus are *loggers*. This system allows different parts of your program to log things independently, with different prefixes, and even different configurations, by using a custom logger class. Let's create a logger.
```python
from pylogplus.pylogplus import PyLogPlus, Logger
pylogplus = PyLogPlus()
pylogplus.init(print)

example_logger = pylogplus.getLogger()
```
Loggers can be created in two ways. You can either directly create an object (logger = Logger()), or use the pylogplus.getLogger() method. It is recommended that you use the getLogger method because that will ensure the logger is ready. Here is an example where you do NOT use the getLogger method:
```python
from pylogplus.pylogplus import PyLogPlus, Logger
pylogplus = PyLogPlus()
pylogplus.init(print)

example_logger = Logger()
example_logger.register(pylogplus.getRegistryData())
```
Not using the getLogger method allows you to register the logger on a custom pylogplus framework class, which allows you to program custom logging functionality. A PyLogPlus Logger can be registered on any framework class that supports the PLP Registry 
#### Sending a message
Now that you have created a logger, you are ready to send a message. The initial pylogplus initialization only has to be completed once.
There are five levels of messages. The display names of these can be changed in the config file, but the method names and amount of them can only be changed with a custom logger class. The five levels are as follows, in order from lowest to highest: debug, info, warning, error, fatal
Let's send one.
```python
from pylogplus.pylogplus import PyLogPlus, Logger
pylogplus = PyLogPlus()
pylogplus.init(print)

example_logger = pylogplus.getLogger()
example_logger.setName('Example')
example_logger.info('A message!')
example_logger.info('A different message!')
```
Using the default config, this code will output:
```
> python example_5.py
PyLogPlus initializing
PyLogPlus is ready
[15:24:55] [Example/INFO]: A message!
[15:24:55] [Example/INFO]: A different message!
```
Times will reflect the current time. You may have noticed a setName message - this sets the prefix that is used as the name variable in the format.
