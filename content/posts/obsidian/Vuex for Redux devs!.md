
---
title: Vuex for Redux devs
date: 2021-01-23 00:00:00
---
---

# Vuex for Redux devs!

Vuex as redux is a state manager, with the pattern of having the whole state separate from the UI. 

This way, rendering is a pure function of the state DOM = render(vuex_state). Also you create specific functions (actions) you can call from the UI to modify the state

![](<../images/VuexForRedux.png>)

So far, is the same with Redux, and for everything else is just the same, with names changed everywhere.


- `mapState` -> is the `mapstatetoprops` of react-redux, it maps the values of the state to fields/props of the component. In vue components, you map them to `computed`
-  `getters` -> is a "view" of the state, and it becomes into antother part of the state (TODO, explain this better :P), you use `mapGetters` to map them to the compoenent
- `mutations` -> are the reducers in redux. they get an "action" with a possible payload, and change the state. as in redux they need to be pure functions. in redux you `dispatch` actions, in vuex you `commit` mutations.
- `mapMutations` -> is the function to map the mutations to the component
- `actions` -> is like redux-thunk middleware but is already inside the code, allows you to write functions that commit multiple mutations. and they can be async functions.

Reference: https://vuex.vuejs.org/#what-is-a-state-management-pattern

