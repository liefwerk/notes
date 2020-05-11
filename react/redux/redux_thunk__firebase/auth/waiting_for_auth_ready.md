# Waiting for Auth Ready

All this application is loaded to the DOM before firebase has time to load the correct data.
That creates a few display bugs. We want a way to prevent the app to load to the DOM

A simple way is to put `{ auth.isLoaded && Links }` inside navBar.js
