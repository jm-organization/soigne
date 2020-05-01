# Hangman
###### Python application framework

Build your first elegant python app!

### Installation
To install the executioner you only need to register the command indicated below. Then you can start writing your application by connecting the modules of this framework.
```shell script
>>> pip install hangman
```

### Your first hangman app
After installing the framework, you need to create the file `` __main __.py`` in the folder of your project and place the code from the example below in it.
```python
from os.path import dirname

from hangman.container import App
from hangman.components.configs import Configs
from hangman.components.l10n import Translation

from myapplication import MyApplication


def register_configs(app, configs, *args):
    """ Configs register method.
    """
    
    return configs(app.path('configs/')).read()


def register_translator(a, translator, *args):
    """ Translator register method.
    """
    
    return translator(app.path('resources/lang/'), app.get('config').l10n['default_language'])


def application_build(app, event):
    """ Application build event handler.
    """

    pass


app = App(dirname(__file__))  # Init our app and set base constants
app.NAME = 'application_name'
app.DESCRIPTION = 'Application description'
app.URL = ''
app.VERSION = '0.1.0.dev1'

# Register some application components
app.register('config', Configs, registerer=register_configs)
app.register('translator', Translation, registerer=register_translator)
app.register('component', 'my_application', MyApplication)

# Register some event handlers
app.dispatch('application_build', application_build)

# Build our app. 
# As a parameter of the build method, you need to specify the name of the component that will process the logic of your application.
my_application: MyApplication = app.build('my_application')
# Now you can call the methods of your application to process it, if necessary. 
my_application.start()
```

### Dependencies
Hangman is obviously strongly dependent on pygame-2.0 and Python-3.8.

### License
This framework is distributed under GNU General Public License v3.0. More in [LICENSE](https://github.com/jm-organization/hangman/blob/master/LICENSE) file
