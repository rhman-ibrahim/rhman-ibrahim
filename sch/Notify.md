[![Tools](https://skillicons.dev/icons?i=js,vite,react,redux)](https://skillicons.dev)

# Notify

A JavaScript, React (Vite) components library which provides notification management.

----

01. State
    01. [Notify Slice](#notify-slice)
02. Components
    01. [Alerts](#alerts)
    02. [Notifications](#notifications)
03. Hooks
    01. [useNotify](#the-notify-hook)


# State

In Blocks the state is managed with **Redux** and **Redux Tool Kit**, because of their excellence in management state in React applications due to their predictable state management, which simplifies debugging and testing.

|Dependency|Role|
|---|---|
|Redux|Provides a centralized store for all application state, ensuring consistency across components.|
|Redux Tool Kit|Enhances Redux by reducing boilerplate code, offering built-in best practices, and integrating tools like `createSlice` and `createAsyncThunk` for easier reducer and asynchronous logic creation, making state management more efficient and developer-friendly.|

## Notify Slice

This slice manages all of notify components states as **Alerts** and **Notifications** components use `notifications` and `counter` properties.

### Properties

|Property|Usage|
|--|--|
|`notifications`|An array that includes all of current state notifications.|
|`counter`|A number that reflects the number of current state notifications.|

### Reducers

|Reducer|Usage|
|--|--|
|`addNotification`|Adds a new notification into the state and increments the `counter` by `1`, a notification is an object of `read`, `id`, `message`, `flag` properties. use the [useNotify](#the-notify-hook) in order to add a new notification by providing the message only.|
|`markNotificationRead`|By passing the `id` this action toggles the `read` property to `true`; by default it is set to `false`.|
|`removeNotification`|By passing the `id` this actions removes the notification from the state and decrement the `counter` by `1`.|
|`clearNotifications`|Clears all of the notifications and resets the counter to `0`.|

---

# Components
> These components are desgined to work with [Blocks](https://github.com/rhman-ibrahim/blocks), this does not prevent it from being used independently but it has not been tried yet. 

## Alerts
01. An alert is self disappearing element, it disappears after 4 seconds. It shows the very first characters of the notification message (shows `90px` of its width) preceded by the notifications counter and colored with the notification's flag colors.

02. As an animated positioned element it aims to trigger the user to check the Notifications, Alerts appear on the middle top of the screen, its animation takes `1s` (1 second) to finish.

03. Place **\<Alerts />** at the end of the displayed component as it is a positioned element.

## Notifications
01. A list of styled HTML ***div*** elements representing notifications, It's better to place the **Notifications** component inside a positioned element and display it when needed on a click; *For example: using [NotificationsAside](https://github.com/rhman-ibrahim/blocks?tab=readme-ov-file#special-asides)*.

02. Each notifcation displays its message with 2 buttons; each button of a single functionality: `removeNotification` and `markNotificationRead` and this can't be undone.

03. When a notification is marked read using `markNotificationRead`, its `opacity` decreases from `1` to `0.5` and moves to the end of the displayed notifications.

04. When a notification is removed using `removeNotification`, it disappears from display compeletly and this can't be undone.

05. Place **\<Notifications />** at the end of the displayed component as it is a positioned element.

---

# Hooks

Custom hooks in React are a way to encapsulate and reuse stateful logic across multiple components. They allow you to extract component logic into reusable functions. A custom hook is essentially a JavaScript function whose name starts with "use" and that can call other hooks.

## The Notify Hook

`useNotify` utilizes the `dispatch` function and `addNotification` action from the slice reducers to add notifications with using 4 functions `nDanger`, `nWarning`, `nInfo`, `nSuccess` this naming convention *nFlag* states the each method adds a different flag to the notification: `danger`, `warning`, `info` and `success` respectively.


```
    import {useNotify} from 'notify';

    const message = `Hello World!`;
    const { nInfo } = useNotify();

    nInfo(message);
```