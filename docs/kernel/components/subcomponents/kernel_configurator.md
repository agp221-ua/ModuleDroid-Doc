---
icon: material/wrench-cog
---

# Kernel Configurator

The `KernelConfigurator` is the subcomponent responsible for configuring the microkernel and its components within the 
application. All configuration tasks are handled by this subcomponent, which prepares the configuration presets for each
component, registers all plugins, initializes them, and applies the appropriate settings. As the first component to be 
initialized, it enables certain actions to be performed before and after the initialization of the microkernel.

## Custom `Application`

The `KernelConfigurator` requires access to the `Application` instance to configure the microkernel and its components. 
This is why it utilizes a class that extends from `Application`, which has access to methods like `onCreate`, allowing 
actions to be taken during the application’s creation. These actions include initializing the various microkernel 
subcomponents and registering plugins.

For this reason, it is crucial that the `Application` instance is either an instance of or extends from 
`ModuleDroidApplication`. To achieve this, simply add or replace the `Application` class in the `AndroidManifest.xml` 
file with `ModuleDroidApplication`.

```xml
<application 
        android:name="software.galaniberico.moduledroid.subcomponents.kernelconfigurator.ModuleDroidApplication"
        ...
        > 
        <!-- ... -->
</application>
```

By doing so, the `Application` instance will be of type `ModuleDroidApplication`, and the `KernelConfigurator` will 
automatically have access to it.

## Plugin Registration

As mentioned earlier, the `KernelConfigurator` is responsible for registering plugins within the microkernel. To simplify
this process for developers and prevent them from having to manually register or configure plugins in their code, an 
auto-registration system has been implemented. This system allows plugins to be automatically registered and configured 
simply by adding the dependency to the application’s `AndroidManifest.xml` using metadata:

The plugin developer only needs to specify, in the plugin's documentation, the configurator class to be added to the list
of plugins.

```xml
<application 
        android:name="software.galaniberico.moduledroid.subcomponents.kernelconfigurator.ModuleDroidApplication"
        ...
        > 
        <!-- ... -->
        <meta-data
            android:name="moduledroid_plugins"
            android:value="software.galaniberico.myplugin.MyPluginConfigurator" 
            />
</application>
```

???+ tip
    Plugins can be listed using commas (`,`) and the list can contain line breaks and whitespace for improved readability. For instance:
    ```xml
    <meta-data
        android:name="moduledroid_plugins"
        android:value="software.galaniberico.myplugin.MyPlugin1Configurator,
                       software.galaniberico.myplugin2.MyPlugin2Configurator,
                       software.galaniberico.myplugin3.MyPlugin3Configurator"  
    />
    ```

???+ info
    The provided class must extend the `PluginConfigurator` interface and have a parameterless constructor.


