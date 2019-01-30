---
layout: post
title:      "Setting Up Middleware and Redux Dev Tools in React"
date:       2019-01-30 19:42:20 +0000
permalink:  setting_up_middleware_and_redux_dev_tools_in_react
---


Here's a quick post that will especially be useful (hopefully...) to Learn.co students who are learning the ins-and-outs of Redux. As we learned, setting up async fetch requests in this environment requires a bit of forethought. This is because, without any change to the standard React and Redux set ups,  we would create errors when loading React components with data coming from a fetch request because of the fact that those components will try to load before that data has been retrieved. How to set action creators and reducers for this purpose is outside of the scope of this post, but the main takeaway is that we need some middleware that can allow us to return functions in our action creators. This allows our action creators to dispatch different actions to our reducer when we are loading and when the fetch request has completed.  We learned how to use React Thunk for that purpose, and ultimately, you should end up with something like this on your root index.js file:

```
import React from 'react';
import ReactDOM from 'react-dom'
import App from './App'
import { Provider } from 'react-redux';
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

const store = createStore(rootReducer, applyMiddleware(thunk));

ReactDOM.render(
    <Provider store={store()} >
        <App />
    </Provider>,
    document.getElementById('root')
);
```

The unanswered question I had at this point was how to connect the Redux Dev Tools chrome extension that I use for debugging anything having to do with Redux in my browser. Adding the code snippet to the `store` variable didn't work and caused errors:

`const store = createStore(rootReducer, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__(), applyMiddleware(thunk));` 

or

`const store = createStore(rootReducer, applyMiddleware(thunk), window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__();`

A bit of googling found a suitable answer in the form of the `compose()` function that is included in the redux library. Essentially, adding middleware and the devtools connection are known as "enhancements" to the Redux store. All that `compose()` does is allow you to nest those enhancements, which come in the form of functions. So, this was my final setup:

```
import React from 'react';
import ReactDOM from 'react-dom'
import App from './App'
import { Provider } from 'react-redux';
import { createStore, applyMiddleware, compose } from 'redux';
import thunk from 'redux-thunk';
import rootReducer from './reducers';

export default function store(initialState) {
    const store = createStore(
      rootReducer,
      initialState,
      compose(
        applyMiddleware(thunk),
        window.__REDUX_DEVTOOLS_EXTENSION__ ? window.__REDUX_DEVTOOLS_EXTENSION__() : f => f
      )
    );
    return store;
}

ReactDOM.render(
    <Provider store={store()} >
        <App />
    </Provider>,
    document.getElementById('root')
);
```

Note that you must add `compose` to the functions that are imported from Redux. I will be honest, some of this code still is a bit of a mystery (in particular, why `f => f` is the false option in the DevTools arguement in the compose function), but seeing as I just got finished with this final lab and it worked perfectly, I thought I would share. Any additonal insights would be great!
