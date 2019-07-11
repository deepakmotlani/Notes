## React Lifecycle methods

**So basically there are 3 stages in which lifecycle methods can be categorized**
* Initializtion
* Mounting
* Updation
* Unmounting

**Each of these phases have lifecycle methods associated as below**

Note - Constructor is a part of initialization.

![Component Life Cycle](https://github.com/deepakmotlani/Notes/blob/master/Front-End/React/lifecycle.png)

**As a part of React 16.3+, there are 2 methods addded in liefecycle**

**getDerivedStateFromProps**: Invoked right before calling render() method, & is invoked on every render. This exists
for reare use dases where you need derived state.

**getSnapshotBeforeUpdate**: Executed right before rendered output is committed to DOM. Any value returned by this 
will be passed into componentDidUpdate().