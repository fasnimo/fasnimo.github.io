---
layout: post
title:      "MapDispatchToProps"
date:       2020-10-13 21:07:20 +0000
permalink:  mapdispatchtoprops
---

Redux allows the developer to store data, a developer uses this feature to make components less reliant of passing data as props, the local state to separate concerns. The separation of concerns is what React is best at, the class or functional components import and export to each other and will have data passed between them. When the user interacts with the UI then actions will be invoked. When an action is invoked in a component code as to written inside a component dispatch is called to pass an action to a reducer `dispatch=>({type: "ADD_SOMETHING"})`. 

Dispatch enables this and also passes the object `dispatch=>({type: "ADD_SOMETHING", actionObj})` . The second argument added is the object passed to the reducer, this will go inside of a switch() case condition until the "ADD_SOMETHING" condition is met and the state is updated. MapDispatchToProps enable with use of dispatch in a component as props, so a parent component can pass dispatch down to its child component as props. This helps as mentioned separation of concerns. To refactor use an action folder to hold a file that contains many actions.
Actions without fetch() e.g.
```
export const addBook = book => {
  return {
    type: 'ADD_BOOK',
    book
  };
};

export const removeBook = id => {
  return {
    type: 'REMOVE_BOOK',
    id
  };
};
```

When an action file like this one has many actions it will look like above, these actions accept arguments to send data to a reducer.
Reducer e.g.
```
export const  booksReducer = (state = [], action) => {
  let idx;
  switch(action.type){
    case "ADD_BOOK":
      return [...state, action.book]
    case "REMOVE_BOOK":
      idx = state.findIndex(book => book.id === action.id)
      return [...state.slice(0, idx), ...state.slice(idx + 1)]
    default:
        return state
  }
}
```

Previous examples of mapDispatchToProps will look like below.

```
 const mapDispatchToProps = dispatch => ({
  addBand: name => dispatch({ type: "ADD_BAND", name }),
  deleteBand: id => dispatch({type: 'DELETE_BAND', id})
})

```

The dispatch handle type and action payload to the reducer. Thanks to Thunk asynchronous action is made simpler and the action that is called will process the dispatch to fetch and receive the response and dispatch the function. Thunk is imported into index.js and used applyMiddleware(thunk), this will apply to the store inside of `<Provider store={store}>`. The actions are easier to write without writing mapDispatch toProps. Once imported as `import { addSomething } from "../actions/somethingActions"`, regardless of how your folder is arranged the `{ curly braces }` will destructure the action you wish to acquire from the file. When we export a component use `export default connect(null, {addSomething})(ComponentName)`. When you use null as the first argument it is because you are not using the global state, but instead using actions as props e.g. `this.props.addSomethign(this.state)`. As seen previously each action accepted an argument, this argument is the `this.state`. 
Fetch actions e.g.

```
export const fetchReview = () => {
    return (dispatch) => {
        fetch("http://localhost:3000/reviews")
        .then(res => res.json())
        .then(review => dispatch({type: "FETCH_REVIEW", payload: review}))
    } 
}

export const addReview = (data) => {
    return (dispatch) => {
        fetch("http://localhost:3000/reviews",{
            method: "POST",
            headers: {
                "Content-Type": "application/json",
                "Accept": "application/json"
            },
            body: JSON.stringify({subject: data.subject, mention: data.review})
        })
        .then(res => res.json())
        .then(review => dispatch({type: "ADD_REVIEW", payload: review}))
        window.location.href = "http://localhost:3001/reviews"
    }
}
```

The actions above both use fetch and as seen dispatch handles the return, this is better for performance, and more than one action can be dispatched. Working with Redux can be used in many cases. Creating a folder for actions and reducers will be time-consuming but then you can use the usefulness of props and all of their benefits.

