# Async Code with Redux

The problem here is that if we want to use data from an external source, placing it inside the reducer file won't work.
The reason is that this process takes longer than the reducer's task, which will therefor update the central state without our external data.

The solution relies on installing `Thunk`, a middleware and place it's process between the moment we dispatch the action and we receive that action in the reducer method.
It will perform an asynchronous task inside the action creator.

Thunk will hold the dispatch, perform the async request and resume the dispatch.