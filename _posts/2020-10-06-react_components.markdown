---
layout: post
title:      "React Components"
date:       2020-10-06 23:23:20 +0000
permalink:  react_components
---


React Components work together to give each other component its own responsibility. A container components mount child components and can send props, and manage state, along with other tasks. When managing state with Redux you can use `import {connect} from "react-redux"` to use `mapStateToProps` which will retrieve the state changes and pass them into `<Components as={props} />`. These child components can also have a local state as a class component or they can be functional components without state using only the props passed down to them. Components that have the job of only rendering are Presentational components. 

Components that have props sent to them and render them can also be called presentational components. Presentational components will render with little to no logic or lifecycle hooks implemented. When creating a component for input functionality a local state would be used and other methods such as `onChange` and `onSubmit`. These changes would be updated in the local state and passed into a Redux action. The action would traditionally send an action.type and payload of the state to a reducer to update the state, but with the inclusion of `redux-thunk` we can use fetch to an API database. When including fetch the return is via dispatch function and the reducer will listen to the action.type `"ADD_SOMETHING"`  to a `switch` `case` conditional. 

The benefit of the `switch case` conditional is that it's less complex to read unlike a `if else` and the function will read each case of that reducer until it finds one it can return. 
e.g.
```
    export const reviewReducer = (state = [], action) => {
    switch(action.type){
        case "ADD_REVIEW":
            return [...state, action.payload]
        case "FETCH_REVIEW":
            return action.payload
        default: 
            return state
      }
    }
```
The default will return the state if no case is met, this allows one reducer to handle multiple action.types. Unlike reducers, there should be many action function built to handle each fetch separately. When connecting an action to a component use `{ connect }` and use it in ` export default connect(mapStateToProps, { addSomething })(Component)` or `mapDispatchToProps` as it's own function then apply them to  ` export default connect(mapStateToProps, mapDispatchToProps)(Component)`. 

It is good practice to have a top-level component that will mount the other child components, for example, App.js can mount your initial application components. Class components will use `render () {}` for JSX to be used, and functional components will `return ()`. Life cycle hooks can be used in class components and if a functional component is reliant on a lifecycle hook whatever is needed can be passed to if by props. 
e.g.
```
     class ReviewContainer extends React.Component{
    
    componentDidMount(){
        this.props.fetchReview()
    }
    
    render(){
         return (
            <div>
                <ReviewList reviews={this.props.reviews}/>
            </div>
           );
       }
   };

   const mapStateToProps = ( state) => {
       return {
           reviews: state.reviews
      }
  }

    export default connect(mapStateToProps, {fetchReview})(ReviewContainer);
```
The props are passed to a function component that will mount and display the date when ReviewContainer mounts and run the fetchReview action via `componentDidMount`  that will supply `mapStateToProps` with data which is then used as props for ` <ReviewList reviews={this.props.reviews}/>`.  This allows the components to be less reliant on managing state and more developer-friendly. Using JSX allows developers to build HTML representational code to render, this is all made possible by Babel a JavaScript compiler, which will translate the JSX to the browser as backward compatible JavaScript. In an instance when ES6 syntax is not recognizable in a browser then Babel will translate the JSX, and will use code that would be better suited for performance.


