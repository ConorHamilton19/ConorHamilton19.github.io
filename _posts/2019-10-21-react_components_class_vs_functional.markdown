---
layout: post
title:      "React Components: Class vs Functional"
date:       2019-10-21 15:46:42 +0000
permalink:  react_components_class_vs_functional
---


Two major types of components in React are Class Components and Functional Components. Though they work to accomplish similar goals, there are some major differences that makes each a better fit for different situations. 

**Class Component**

![](https://media.giphy.com/media/hFROvOhBPQVRm/giphy.gif)

A class component is a smart component in React. This means that by extending the "Component" class from React, this type of component gets a little bit of extra added functionality. You must import the "Component" class from React:

`import React, { Component } from 'react'`

One of the major ways this added functionality helps is in the use and setting of State. State is important because it allows data to be able to be manipulated inside of the component. This makes the component much more interactive than merely just passing around props. Another big advantage of Class Components is using Lifecycle Methods. These methods are called in order during the "lifecycle" of a component and help control what happens during each part of the rendering of a component from Mounting to Un-Mounting.

```
import React, { Component } from 'react'

class Hello extends React.Component {
   state: {
  }

  render() {
    return <h1>Hello</h1>;
  }
}

export default Hello
```

Pros:
* Use and Setting of State
* Lifecycle methods to mange the rendering of the component

Cons:
* Added functionality also creates unnecessary code for many components


**Functional Component**

![](https://media.giphy.com/media/LnKa2WLkd6eAM/source.gif)

A functional component is considered a dumb component in React. These components are very simple and are mainly used for presentational components that do not rely on State. 

```
import React from "react";

const Hello = props => (
  <div>
    <h1>Hello, {props.name}</h1>
  </div>
);

export default Hello;
```

One advantage of having a simple component is that they can be written in JS function form(usually arrow) with props being passed as an argument. This keeps the code very simple and helps make it obvious which components are only presentation verse which components have logic and state in them. This organization can be very important when you have a large React app. 

Pros:
* Simple and effective at presenting components 
* Help keep code base organized

Cons:
* No logic or State manipulation 
* No use of lifecycle methods
