---
icon: material/sync
---

# Activity Lifecycle

The `Activity Lifecycle` subcomponent is a part of the kernel responsible for intercepting the lifecycle events of the
application's activities to execute corresponding actions. Its purpose is to allow other subcomponents and application
plugins to react to these activity lifecycle events to perform various actions.

???+ example
    For instance, consider a plugin that manages navigation between screens in the application. This plugin needs to know
    when a new activity is created to pass relevant data to the new screen. To achieve this, it could subscribe to the
    `onCreate` event in the activity lifecycle and execute the necessary actions when this event occurs.

???+ info
    Currently, the `Activity Lifecycle` subcomponent does not officially support intercepting fragment lifecycle events.

## Retrieving Activities

???+ warning
    The reference to these Activities can change at any time, so it is recommended not to store the reference but to call
    the method when needed. Another option is to create a computed property where the getter calls the desired method.

To retrieve Activities, the Facade provides different options depending on the situation:

| Method             | Description                                                                                                                                                                                           |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Current Activity   | Returns the activity that is currently resumed.                                                                                                                                                       |
| Resuming Activity  | Returns the activity that is currently resuming.                                                                                                                                                      |
| Starting Activity  | Returns the activity that is currently starting.                                                                                                                                                      |
| Creating Activity  | Returns the activity that is currently being created.                                                                                                                                                 |
| Preferred Activity | Returns the activity in the order `resuming` > `starting` > `creating` > `current`. This is offered as a simplified solution to access the activity during uncertain times when the state is unknown. |

Alternatively, there are two methods to retrieve the desired activity: one that returns a nullable value (Activity?) and
another that returns a non-nullable value (Activity), which will throw an `IllegalStateException` if the desired
activity is not found.

???+ example
    For example, let's assume we want to obtain the current activity of the application from a code where
    direct access to the activity is not available.

    ```kotlin
    // Optional way
    val currentActivity = Facade.getCurrentActivity() ?: // Handle case where no activity is found

    // Exception way
    try {
        val currentActivity = Facade.getCurrentActivityOrFail()
    } catch (e: IllegalStateException) {
        // Handle case where no activity is found
    }

    // Property way
    val currentActivity: Activity?
        get() {
            return Facade.getCurrentActivity()
        }
    //...
    this.currentActivity // Access the current activity
    ```

## Event Subscription

As mentioned earlier, the `Activity Lifecycle` subcomponent uses a subscription system for activity lifecycle events.
The `Activity Lifecycle` provides a set of methods that allow subscribing to these events.

To achieve this, the `Activity Lifecycle` subcomponent intercepts lifecycle events. When an activity lifecycle event
occurs, before the corresponding activity method is executed, all subscriptions to that event that meet the relevant
conditions are executed.

The available events for subscription are: `onPreCreate`, `onCreate`, `onPostCreate`, `onPreStart`, `onStart`,
`onPostStart`, `onPreResume`, `onResume`, `onPostResume`, `onPrePause`, `onPause`, `onPostPause`, `onPreStop`, `onStop`,
`onPostStop`, `onPreDestroy`, `onDestroy`, `onPostDestroy`, `onRestart`, `onSaveInstanceState`.

Additionally, all of these events offer different subscription method versions, adapting to the specific case as needed
based on certain conditions:

| Method call parameters                    | Description                                                                                                                               |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| `subscription`                            | This call simply adds the subscription, which will be executed when the event is captured.                                                |
| `id`<br>`subscription`                    | This call only executes the subscription when the id of the current activity matches `id`.                                                |
| `activityClass`<br>`subscription`         | This call only executes the subscription when the class of the current activity matches `activityClass`.                                  |
| `id`<br>`activityClass`<br>`subscription` | This call only executes the subscription when both the id and class of the current activity match `id` and `activityClass`, respectively. |

???+ example
    Suppose we want to subscribe to the `onCreate` event of a specific activity. We could use the following call:

    ```kotlin
    Facade.addOnCreateSubscription { activity, bundle ->
        // Execute actions when MyActivity is created
    }
    ```

    Now, imagine we want to subscribe to the `onStart` event of the activity with id `myActivityId`:

    ```kotlin
    Facade.addOnStartSubscription(myActivityId) { activity ->
        // Execute actions when MyActivity is started
    }
    ```
