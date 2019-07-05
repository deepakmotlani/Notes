## Refs

Refs provide a way to access DOM nodes or React elements created in render method.

In typically flows, parent & child component can interact only through props, to modify a child, you re-render it
with new props. However there are few cases where you need to modify a child outside typical dataflow. Child to be
modified could be an instance of React Component, or it could be a DOM element. For both of these cases, ReactJs
provides an escape.

Don't overuse refs

### Creating Refs

Refs are created using React.createRef() & attached to elements via ref attribute. 

```
class MyComponent extends React.Component {
	constructor(props) {
		super(props);
		this.myRef = React.createRef();
	}
	render() {
		return <div ref={this.myRef}/>
	}
}
```

You can also create Ref with Ref callbacks without using constructor.

```
class MyComponent extends React.Component {
	constructor(props) {
		super(props);
	}
	render() {
		return <div ref={(element) => {this.ref = element}}/>
	}
}
```

### Accessing ref

When created using constructor, when ref is passed to an element in render, reference to node becomes accessible 
at current attribute of ref.

> const node = this.ref.current

**Value of ref differs depending on type of node:**
* When ref attribute is used on HTML element, ref created in constructor using React.createRef receives underlying
	DOM element as its current property.
* When ref is used on custom component the ref object receives mounted instance of component.
* You may not use ref attribute on function component because they don't have instances. So you should convert
	function to Class if you need a ref to it.

Example - This is not allowed, because FirstName is function component
```
function FirstName() {
	return (
		<span>First Name</span>
	);
}
class MyComponent extends React.Component {
	render() {
		return(
			<FirstName ref={(e) => {this.ref = e}}>
		);
	}
}
```

Example - also this is not allowed
```
function FirstName() {
	return (
		<span ref={(e) => {this.ref = e}}>First Name</span>
	);
}
```

But you can create Ref in function component usinf React.createRef, like below
```
function FirstName() {
	let spanRef = React.createRef();
	return (
		<span ref={spanRef}>First Name</span>
	);
}
```

### Exposing DOM Ref to Parent Component
In rare cases, we might want to access to child's DOM node from parent component. This is generally not recommended
because it breaks component encapsulation, but it can be occasionally useful.

In React 16.3 or higher, we recommend using Ref Forwarding. Ref forwarding lets a component take a ref & pass it
further down. Example -

```
function FancyButton = React.forwardRef((props, ref) => {
	<button ref={ref}>
		{Submit}
	</button>
});

function MyComponent() {
	const ref = React.createRef();
	return (
		<FancyButton ref={ref}>Click Me!</FancyButton>
	);
}
```

This way MyComponent gets a direct access to FancyButton DOM button. 2nd arguement ref only exists when you define
component using React.forwardRef.

If you use React 16.2 or lower, you can acheive same by passing ref as a named property.

```
function FancyButton(props) {
	return (
		<button ref={props.buttonRef}>
			{Submit}
		</button>
	);
});

function MyComponent() {
	const ref = React.createRef();
	return (
		<FancyButton buttonRef={ref}>Click Me!</FancyButton>
	);
}
```

**Refs are guaranteed to be updated before componentDidMount or componentDidUpdate fires.**
