---
layout: page
title: Handle UI Events
---

#### Register Event Handler to UiComponents

To handle events from ui components you can subscribe theses events by register and implement an event handler.

Before an event handler is called all values of every element of your view is transfered back in the backend. Also models are updated if they are connect via CloudUi data binding functions.

#### Example

~~~~

Button button = new Button();
button.addEventHandler("click", event -> {
    Notification notification = new Notification("Button clicked");
    add(notification);
    notification.open();
})
~~~~

#### Limitations

So for there are no event attributes transfered.