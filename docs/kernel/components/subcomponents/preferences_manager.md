---
icon: material/card-bulleted
---

# Preferences Manager

The `Preferences Manager` subcomponent is responsible for managing the application's preferences. It handles the
initialization, configuration, and retrieval of the application's preferences. Its aim is to centralize the management
of preferences and provide a unified interface for accessing them without unnecessary code repetition.

## Retrieving and Setting Preferences

To retrieve or set the application's preferences, the following methods are available:

| Method      | Description                                                                                                                                                                                                                         |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **_get_**   | Retrieves the value of a preference. It takes as parameters the preference key and the default value if the preference does not exist. Supports the types `String`, `Int`, `Float`, `Double`, `Boolean`, `Long`, and `Set<String>`. |
| **_set_**   | Sets the value of a preference. It takes as parameters the preference key and the value to be set. Supports the types `String`, `Int`, `Float`, `Double`, `Boolean`, `Long`, and `Set<String>`.                                     |
| **_clear_** | Clears all stored preferences. This is designed for testing and isolated cases.                                                                                                                                                     |

???+ example
    To set a preference with the key "**_my-key_**" and the value "**_my value_**":
    
    ```kotlin
    Facade.set("my-key", "my value")
    ```
    
    To retrieve the value of the preference:
    
    ```kotlin
    val value = Facade.get("my-key", "default value")
    // If it exists, it will be "my value", otherwise it will be "default value"
    ```

## Subscription to Changes

The `Preferences Manager` subcomponent allows subscription to changes in the application's preferences, so that whenever
a preference changes, the specified callbacks are executed. The following methods are available for this purpose:

| Method                   | Description                                                                                                           |
|--------------------------|-----------------------------------------------------------------------------------------------------------------------|
| **_addSubscription_**    | Adds a subscription to a preference. Takes the callback to be executed as a parameter in case any preference changes. |
| **_removeSubscription_** | Removes a subscription to a preference. Takes the callback to be removed as a parameter.                              |

???+ example
    To add a subscription to the preference "**_my-key_**":
    ```kotlin
    Facade.addSubscription { _, key ->
        if (key == "my-key") {
            //...
        }
    }
    ```
    
    To remove the subscription:
    
    ```kotlin
    Facade.removeSubscription() {
        if (key == "my-key") {
            //...
        }
    }
    ```
