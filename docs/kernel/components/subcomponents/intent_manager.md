---
icon: fontawesome/solid/diagram-predecessor
---

# Intent Manager

The `Intent Manager` subcomponent is responsible for the part of the kernel that intercepts events related to the 
application's intents to execute the corresponding actions. Its main goal is to simplify intent management for the 
client by centralizing the handling of application intents.

???+ note
    Currently, `Intent Manager` only supports `Intents` for launching Activities within the same application.

## Launching Activities

Two primary methods are provided for launching activities within the application:

| Method                       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **_startActivity_**          | Launches an activity within the application. It requires the destination activity's class as a mandatory parameter. Optionally, you can assign an ID to the destination activity and execute a pre-launch action through a lambda function, which provides parameters such as the intent used or the assigned ID (e.g., for cases where an ID is not specified). Additionally, the parent activity instance can be passed if you want to explicitly indicate the context from which it is created.           |
| **_startActivityForResult_** | Launches an activity within the application and awaits a result. It requires the destination activity's class as a mandatory parameter. Optionally, you can assign an ID to the destination activity and execute a pre-launch action via a lambda function, which provides parameters such as the intent, the assigned ID (e.g., for cases where an ID is not specified), or a requestCode (if not provided, a generic one will be created). The parent activity can also be explicitly specified if needed. |

???+ example
    For instance, let’s say we want to launch an activity of class `OtherActivity`.
    ```kotlin
    Facade.startActivity(OtherActivity::class.java)
    ```
    Alternatively, if we want to launch the activity with a specific ID, we can do so as follows:
    ```kotlin
    Facade.startActivity(OtherActivity::class.java, "id")
    ```
    Furthermore, if we want to perform a pre-launch action and specify the source activity, we can do it like this:
    ```kotlin
    // Assuming we are within an activity
    Facade.startActivity(this, OtherActivity::class.java) { intent, id, internalId ->
        intent.putExtra("key", "example")
    }
    ```

## Activity Identifiers

To facilitate the identification of activities, `Intent Manager` assigns a unique identifier to each activity initiated 
through its defined methods. This may result in activities without an identifier, so several methods are available to 
provide an identifier to an activity if it lacks one, or to retrieve the identifier if it already has one:

| Method                  | Description                                                                                                                                                               |
|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **_getId_**             | Retrieves the identifier of the activity passed as a parameter.                                                                                                           |
| **_provideId_**         | Assigns an identifier to the activity passed as a parameter if it lacks one, and returns it. Note that if the activity already has an identifier, it will be overwritten. |
| **_getIdOrProvideOne_** | Retrieves the identifier of the activity passed as a parameter if it already has one, or assigns one if it lacks one, returning it in either case.                        |

???+ example
    For instance, let’s say we want to obtain the identifier of an activity:
    ```kotlin
    val activity: Activity = ...
    val id = Facade.getId(activity)
    ```
    Alternatively, if we want to assign an identifier to an activity that does not yet have one:
    ```kotlin
    val id = Facade.provideId(activity)
    ```
    On the other hand, if we want to retrieve the identifier of an activity if it already has one, or assign one if it 
    does not:
    ```kotlin
    val id = Facade.getIdOrProvideOne(OtherActivity::class.java)
    ```

???+ tip
    Among these methods, `getIdOrProvideOne` is the most recommended as it avoids constant checks and reduces the risk 
    of errors related to activity identification.

## Internal Identifiers

With the above method, potential issues arise, such as assigning duplicate identifiers to different activities. To avoid
this, a unique internal identifier is maintained, allowing users to have activities with the same identifier while 
internally assigning a unique identifier to each. This internal identifier can be retrieved through the `getInternalId` 
method and cannot be assigned manually, as it is automatically assigned whenever an identifier is either manually or 
automatically assigned.

???+ example
    For instance, let’s say we want to retrieve the internal identifier of an activity:
    ```kotlin
    val activity: Activity = ...
    val internalId = Facade.getInternalId(activity)
    ```

???+ warning
    Each time an activity’s identifier is overwritten, the internal identifier will also be updated.
