---
layout: post
title:      "Basic Reaction to React (Also Redux)"
date:       2020-11-07 13:12:13 -0500
permalink:  basic_reaction_to_react_also_redux
---


Often, developers get comfortable with a concept such as a programming language or framework; but then have something else added on top of that which can sometimes throw a wrench in the works.

This happened to me when I moved from Sinatra to Rails. Both use Ruby as the programming language, but the two frameworks have some key differences which can make the transition challenging. Needless to say moving from basic or "vanilla" JavaScript to React *and then* addind Redux on top of that was... let's say difficult at best.

The most important steps for me was understanding the simple basics of React/Redux. Nail down the difference between components and containers, understand what state and props mean, and finally sprinkle that Redux over the top of everything to make one big happy application.

**What is React?**

Released in 2013, React is a JavaScript library that is maintained by Facebook and is meant for developing User Interfaces (UIs)

React code is made up of Componentsm they are essentially block of code that can easily be reused throughout any application that you build. Components are written in JSX, or JavaScript XML, which looks very similar to HTML and therefore familiar to most progrommers.

The basis of a React app looks something like this:

```ReactDOM.render(
    <React.StrictMode>
      <App />
    </React.StrictMode>
  document.getElementById('root')
);```

You'll see that middle line is what renders the App Component. Now inside that App component, you could render more and more components simply by using those self-closing tags.

```<App
         <Component 1 />
				 <Component 2 />
				 <Component 3 />
				/>```
				
	So on and so forth ...
	
	This is what makes React handy and easy to organize, you simply tell the App page to import from the file where your component code is, and then simply render it like the example above. Each Component has a render() function that shows what will display to the DOM when it is rendered.
	
**Props and Sate**
Props are data that gets passed from one Component to another, like 'properties'.  Props are not immutable, meaning they cannot change. Calling ```this.props``` is a good way to call all the props a Component might have.

State is very similar to Props in that it holds information that influences how the Component renders, but the biggest difference is that Props get passed to the component like function parameters, whereas State gets managed within the Component itself. For example, if you built some sort of counter app, you could have a button that maybe increases the state + 1, therefore the state would update and the component re-renders.

This is a * very basic* introduciton to React and there is a lot more to unpack, but understanding the simple basics is key when it comes to learning new programming.

**But what about Redux???**
You though I forgot,* didn't you ?*

We've briefly talked about State, and in any React application there might be a lot of State going on. Think about it, the more Components you have, the more State the application has, and you have to deal with this State and that State. This can make your application clunky and increases the chance of somehting breaking. It is here where we enlist the help of Redux.

Redux is a Javascript library that manages State and is often unsed with React. The basic parts of Redux can be broken up into: Store, Actions, Dispatch, and Reducers.

Actions describe what you are going to do. It is a funciton that returns an object. You can really give it any name you want. Earlier I mentioned a simple counter application, so maybe you have an Action called INCREASE_COUNTER, and another Action called DECREASE_COUNTER. 

For example, it might look something like this:
```const increaseCounter = () => {
    return {
		name: "INCREASE_COUNTER"
		}
}```
```const decreaseCounter = () => {
     return {
		 name: "DECREASE_COUNTER"}
}```
Note: where I have "name" you might also see "type", no difference, comes down to preference.

Reducers describe how Actions transform the current state into the next state. In our example, we'd probably have something like a counterReducer. When setting up Reducers, you need to passin two parameters, one is the initial state and the other is an Action. In the below example, the ```switch(action.name)``` line looks at the Action names and invokes the correct one.

```const counterReducer = (state = 0, action) => {
      switch(action.name){
			        case "INCREASE_COUNTER":
							     return state + 1;
							case "DECREASE_COUNTER":
							     return state - 1;
			}
}```

Dispatch works as the bridge connecting Actions to the Reducers, when an Action gets dispatched to the Reducer, the Reducer checks what to do based on the name of said Action and then updates the State.

Store is where the globalized State for the application gets stored (get it?) It's kept at the root of the application where everything is imported to the application gets to enjoy the wonderful process of Redux.

**Redux Review**

In a nuthell, the data flow of Redux works as follows:

* We have the current state of the application.
* The users does something like, clicking a button, or submitting information. Anything that would update the State.
* The Action gets dispatched to the Reducer
* The Reducer checks to see the Action name/type and executes the appropriate action.
* The State is updated in the Store and the Component rerenders with the new State.

These are the basic principals of React/Redux. There are many more things that these libraries have to offer but a solid base is important to build knowledge. Nailing the simple things is important for a programmer's understanding and confidence.




