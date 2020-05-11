# Virtual DOM

We have the App.js that contains:

* Ninjas.js
* AddNinjas.js

To add ninjas we do it through Ninjas.js with addNinjas.
When props updates, it rerenders the template, via the UI Ninja.js

To handle Props, container, to handle UI, UI Component.Ninja.js is constantly updating.
Every time we have an update, React makes a JS representation of the template.

The new virtual DOM created is compared to the current virtual DOM.
When there are changes, differences are updated - only the differences are updated.

Then new Current DOM becomes the current one.
