<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [keplerGlReducer](#keplerglreducer)
    -   [keplerGlReducer.initialState](#keplerglreducerinitialstate)
    -   [keplerGlReducer.plugin](#keplerglreducerplugin)

## keplerGlReducer

Kepler.gl reducer to be mounted to your store. You can mount `keplerGlReducer` at property `keplerGl`, if you choose
to mount it at another address e.g. `foo` you will need to specify it when you mount `KeplerGl` component in your app with `getState: state => state.foo`

**Examples**

```javascript
import keplerGlReducer from 'kepler.gl/reducers';
import {createStore, combineReducers, applyMiddleware, compose} from 'redux';
import {taskMiddleware} from 'react-palm/tasks';

const initialState = {};
const reducers = combineReducers({
  // <-- mount kepler.gl reducer in your app
  keplerGl: keplerGlReducer,

  // Your other reducers here
  app: appReducer
});

// using createStore
export default createStore(reducer, initialState, applyMiddleware(taskMiddleware));
```

### keplerGlReducer.initialState

Return a reducer that initiated with custom initial state.
The parameter should be an object mapping from `subreducer` name to custom subreducer state,
which will be shallow **merged** with default initial state.

Default subreducer state:

-   [`visState`][9]
-   [`mapState`][10]
-   [`mapStyle`][11]
-   [`uiState`][12]

**Parameters**

-   `iniSt` **[Object][13]** custom state to be merged with default initial state

**Examples**

```javascript
const myKeplerGlReducer = keplerGlReducer
 .initialState({
   uiState: {readOnly: true}
 });
```

### keplerGlReducer.plugin

Returns a kepler.gl reducer that will also pass each action through additional reducers spiecified.
The parameter should be either a reducer map or a reducer function.
The state passed into the additional action handler is the instance state.
It will include all the subreducers `visState`, `uiState`, `mapState` and `mapStyle`.
`.plugin` is only meant to be called once when mounting the keplerGlReducer to the store.
**Note** This is an advanced option to give you more freedom to modify the internal state of the kepler.gl instance.
You should only use this to adding additional actions instead of replacing default actions.

**Parameters**

-   `customReducer` **([Object][13] \| [Function][14])** A reducer map or a reducer

**Examples**

```javascript
const myKeplerGlReducer = keplerGlReducer
 .plugin({
   // 1. as reducer map
   HIDE_AND_SHOW_SIDE_PANEL: (state, action) => ({
     ...state,
     uiState: {
       ...state.uiState,
       readOnly: !state.uiState.readOnly
     }
   })
 })
.plugin(handleActions({
  // 2. as reducer
  'HIDE_MAP_CONTROLS': (state, action) => ({
    ...state,
    uiState: {
      ...state.uiState,
      mapControls: hiddenMapControl
    }
  })
}, {}));
```

[1]: #keplerglreducer

[2]: #examples

[3]: #keplerglreducerinitialstate

[4]: #parameters

[5]: #examples-1

[6]: #keplerglreducerplugin

[7]: #parameters-1

[8]: #examples-2

[9]: ./vis-state.md#INITIAL_VIS_STATE

[10]: ./map-state.md#INITIAL_MAP_STATE

[11]: ./map-style.md#INITIAL_MAP_STYLE

[12]: ./ui-state.md#INITIAL_UI_STATE

[13]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[14]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function