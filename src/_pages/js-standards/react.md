---
layout: default
title: React Code Standards
permalink: /js-standards/react/
---

# React Style Guide

<div class="notification">
   <p> Please note that the style choices on this page cannot be automatically enforced, it's on you as a developer to make sure you are following these guidelines </p>
</div>

This style guide inherits all of the [standards and criteria for developing JavaScript]({{site.url}}/js-standards). In the event of a conflict, the rules outlined on this page will trump the main style guide *only* when working with React. If you are familar with AirBnb's React style guide, you'll see alot of similarities in the outline below

### Component Architecture: Props

**ALL** props should be declared with PropTypes and sensible defaults should be provided where it makes sense.

```
export default class ProfileContainer extends Component {
 
  static propTypes = {
    model: object.isRequired,
    title: string
  }
 
  static defaultProps = {
    model: {
      id: 0
    },
    title: 'Your Name'
  }
```

### Component Architecture: Initial State

State should be defined as a property of the React component class. Please note, that this is a newer method of defining default state, as previously developers have done in the class constructor method

```
export default class ProfileContainer extends Component {

  state = { expanded: false, loading: true }
  
 //rest of component code
}
```

### Component Architecture: Higher Order vs. Presentational

In general (ie: 99% of use cases) our components should follow an HOC (Higher Order Container/Higher Order Component) architecture. 

This involves one encapsilating component that handles fetching data and callback functions. 

This component should use presentational (also known as stateless) components to display data / UI elements. The presentational components will recieve data from the HOC as props. This allows greater reusability among UI components.

Think of the HOC as your "page" and the Presentational components as the pieces that make up your page. 

Typically the router will route to an HOC component as well. 

```
    <Route to="/class/:classId" component={ClassDetail}>
```

Here's an example of a User List HOC

```
//containers/UserList/index.jsx
import React, { Component } from 'react'

class UserList extends Component {

    componentDidMount()
    {
        //fetch users and set it in state as 'users'
    }

    render () {
        return (
            <div>
                //map over users and call User component
                users.map((item,index)=>{
                    //if a click handler is needed, pass it down as a prop
                    <User user={item} />
                })
            </div>
        )
    }
}

export default UserList

//components/User/index.jsx
import React from 'react'

const User = (props) => {
    return (
        <div>
            <div class="avatar">...</div>
            <div class="name">{props.user.firstName}</div>
        </div>
    )
}

export default componentName
```

### Component Architecture: Actions & Reducers

Due to the application architecture of HOCs and Presentational components, the accepted method for working with actions and reducers are in the HOC container. The presentational component should call a callback that's passed as a prop. That callback, housed in the HOC, should interact with the state. 

### Passing setState a function

There are valid scenarios where you my find yourself needing to do something like this:

```
this.setState({ expanded: !this.state.expanded })
```

However set state is actually asynchronous. React batches state changes for performance reasons, so the state may not change immediately after setState is called.

That means you should not rely on the current state when calling setState — since you can’t be sure what that state will be!

Here’s the solution — pass a function to setState, with the previous state as an argument.

```
this.setState(prevState => ({ expanded: !prevState.expanded }))
```

### Class vs React.createClass vs stateless

If you have internal state and/or refs, prefer `class extends React.Component` over `React.createClass`

```
// bad
const Listing = React.createClass({
  // ...
  render() {
    return <div>{this.state.hello}</div>;
  }
});

// good
class Listing extends React.Component {
  // ...
  render() {
    return <div>{this.state.hello}</div>;
  }
}
```

And if you don't have state or refs, prefer normal functions (not arrow functions) over classes:

```
// bad
class Listing extends React.Component {
  render() {
    return <div>{this.props.hello}</div>;
  }
}

// bad (relying on function name inference is discouraged)
const Listing = ({ hello }) => (
  <div>{hello}</div>
);

// good
function Listing({ hello }) {
  return <div>{hello}</div>;
}
```

### Naming

**Extensions:** Use .jsx extension for React components.

**Filename:** Use PascalCase for filenames. E.g., ReservationCard.jsx.

**Reference Naming:** Use PascalCase for React components and camelCase for their instances. eslint: react/jsx-pascal-case

```
// bad
import reservationCard from './ReservationCard';

// good
import ReservationCard from './ReservationCard';

// bad
const ReservationItem = <ReservationCard />;

// good
const reservationItem = <ReservationCard />;
```

**Component Naming:** Use the filename as the component name. For example, ReservationCard.jsx should have a reference name of ReservationCard. However, for root components of a directory, use index.jsx as the filename and use the directory name as the component name:

```
// bad
import Footer from './Footer/Footer';

// bad
import Footer from './Footer/index';

// good
import Footer from './Footer';
```

**Higher-order Component Naming:** Use a composite of the higher-order component's name and the passed-in component's name as the displayName on the generated component. For example, the higher-order component withFoo(), when passed a component Bar should produce a component with a displayName of withFoo(Bar).

**Why?** A component's displayName may be used by developer tools or in error messages, and having a value that clearly expresses this relationship helps people understand what is happening.

```
// bad
export default function withFoo(WrappedComponent) {
  return function WithFoo(props) {
    return <WrappedComponent {...props} foo />;
  }
}

// good
export default function withFoo(WrappedComponent) {
  function WithFoo(props) {
    return <WrappedComponent {...props} foo />;
  }

  const wrappedComponentName = WrappedComponent.displayName
    || WrappedComponent.name
    || 'Component';

  WithFoo.displayName = `withFoo(${wrappedComponentName})`;
  return WithFoo;
}
```

**Props Naming:** Avoid using DOM component prop names for different purposes.

**Why?** People expect props like style and className to mean one specific thing. Varying this API for a subset of your app makes the code less readable and less maintainable, and may cause bugs.

```
// bad
<MyComponent style="fancy" />

// good
<MyComponent variant="fancy" />
```

## Alignment

Follow these alignment styles for JSX syntax. eslint: react/jsx-closing-bracket-location react/jsx-closing-tag-location

```
// bad
<Foo superLongParam="bar"
     anotherSuperLongParam="baz" />

// good
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>

// if props fit in one line then keep it on the same line
<Foo bar="bar" />

// children get indented normally
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
>
  <Quux />
</Foo>
```

## Quotes

Always use double quotes (") for JSX attributes, but single quotes (') for all other JS. eslint: jsx-quotes

Why? Regular HTML attributes also typically use double quotes instead of single, so JSX attributes mirror this convention.

```
// bad
<Foo bar='bar' />

// good
<Foo bar="bar" />
{% raw %}
// bad
<Foo style={{ left: "20px" }} />

// good
<Foo style={{ left: '20px' }} /> 
{% endraw %}
```

## Props

Always use camelCase for prop names.

```
// bad
<Foo
  UserName="hello"
  phone_number={12345678}
/>

// good
<Foo
  userName="hello"
  phoneNumber={12345678}
/>
```

Omit the value of the prop when it is explicitly true.

```
// bad```
<Foo
  hidden={true}
/>

// good
<Foo
  hidden
/>

// good
<Foo hidden />
```

Always define explicit defaultProps for all non-required props.

**Why?** propTypes are a form of documentation, and providing defaultProps means the reader of your code doesn’t have to assume as much. In addition, it can mean that your code can omit certain type checks.

```
// bad
function SFC({ foo, bar, children }) {
  return <div>{foo}{bar}{children}</div>;
}
SFC.propTypes = {
  foo: PropTypes.number.isRequired,
  bar: PropTypes.string,
  children: PropTypes.node,
};

// good
function SFC({ foo, bar, children }) {
  return <div>{foo}{bar}{children}</div>;
}
SFC.propTypes = {
  foo: PropTypes.number.isRequired,
  bar: PropTypes.string,
  children: PropTypes.node,
};
SFC.defaultProps = {
  bar: '',
  children: null,
};
```

## Tags

Always self-close tags that have no children. eslint: react/self-closing-comp

```
// bad
<Foo className="stuff"></Foo>

// good
<Foo className="stuff" />
```

If your component has multi-line properties, close its tag on a new line. eslint: react/jsx-closing-bracket-location

```
// bad
<Foo
  bar="bar"
  baz="baz" />

// good
<Foo
  bar="bar"
  baz="baz"
/>
```

### Methods

Use arrow functions to close over local variables.

```
function ItemList(props) {
  return (
    <ul>
      {props.items.map((item, index) => (
        <Item
          key={item.key}
          onClick={() => doSomethingWith(item.name, index)}
        />
      ))}
    </ul>
  );
}
```

Bind event handlers for the render method in the constructor. eslint: react/jsx-no-bind

**Why?** A bind call in the render path creates a brand new function on every single render.

```
// bad
class extends React.Component {
  onClickDiv() {
    // do stuff
  }

  render() {
    return <div onClick={this.onClickDiv.bind(this)} />;
  }
}

// good
class extends React.Component {
  constructor(props) {
    super(props);

    this.onClickDiv = this.onClickDiv.bind(this);
  }

  onClickDiv() {
    // do stuff
  }

  render() {
    return <div onClick={this.onClickDiv} />;
  }
}
```

Do not use underscore prefix for internal methods of a React component.

**Why?** Underscore prefixes are sometimes used as a convention in other languages to denote privacy. But, unlike those languages, there is no native support for privacy in JavaScript, everything is public. Regardless of your intentions, adding underscore prefixes to your properties does not actually make them private, and any property (underscore-prefixed or not) should be treated as being public. See issues #1024, and #490 for a more in-depth discussion.

```
// bad
React.createClass({
  _onClickSubmit() {
    // do stuff
  },

  // other stuff
});

// good
class extends React.Component {
  onClickSubmit() {
    // do stuff
  }

  // other stuff
}
```

Be sure to return a value in your render methods. eslint: react/require-render-return

```
// bad
render() {
  (<div />);
}

// good
render() {
  return (<div />);
}
```