# React Router 4 Basics

> Note: This is a TeamTreeHouse course at: https://teamtreehouse.com/library/react-router-4-basics-2

Link to the project: https://github.com/wsaults/Treehouse-React-Router-4

About this Course**

Learn to use React Router v4, a declarative routing solution for React, to manage navigation and rendering of components in your applications.



**What you'll learn**

- Declaring routes

- Navigating between routes

- Nesting routes

- URL parameters

- 404 error routes

- Changing routes programmatically

  ​



## Getting Started with React Router



### Expand Your React Skills

Routing is the process of matching a URL to the set of components being rendered. Routing dynamically loads components and changes what's displayed in the browser as users navigate an app, all without reloading the page. React does not have built-in routing features, so developrs rely on React Router, an external library designed specifially for React.



### What is Routing?

In single-page apps (SPAs), routing is responsible for loading and unloading content while matching the URL with the set of components being rendered. Routing should also keep track of browser history and link users to specific sections of your app.



### Installing React Router and Declaring Routes

Use the following terminal command to save React Router to the project.

```
npm install --save react-router-dom
```



**Terms:**

- <BrowserRouter> // Route routing component which keeps your UI in sync with the url
- <Route> // Renders a component in the app when it's url matches the path



Use `Route` components inside `BrowserRouter` to load components like `Home` and `About` depending on the url.

> Note: use the keyword `exact` to let `route` know that the path should match exactly.


```jsx
const App = () => (
  <BrowserRouter>
  <div className="container">
    <Header /> // This component stays and isn't dependent on the path.
    <Route exact path="/" component={Home} /> // Renders the Home component when the url is "/"
    <Route path="/about" component={About} />
  </div>
  </BrowserRouter>
);
```



### Inline Rendering with <Route>

Replace `component` with `render` to load a component via an arrow function. This gives you the ability to pass props to the component.

```jsx
<Route path="/about" render={ () => <About title='About' /> } />
```



------



## Navigating, Nesting and Redirecting Routes



### Navigating Between Routes

We'll use React Router's `<Link>` component to navigate between our routes.

> Note: `to` replaces the anchor tag's `href` property.

```jsx
const Header = () => (
  <header>
    <span className="icn-logo"><i className="material-icons">code</i></span>
    <ul className="main-nav">
      <li><Link to="/">Home</Link></li>
      <li><Link to="/about">About</Link></li>
      <li><Link to="/teachers">Teachers</Link></li>
      <li><Link to="/courses">Courses</Link></li>
    </ul>    
  </header>
);
```



### Styling Active Links

Use `NavLink` to enforce active states in the navigation.

> Note: you can use `activeStyle` and `activeClassName` to override styles or the active class.

```jsx
<li><NavLink exact to="/" activeStyle={{ background: 'tomato' }}>Home</NavLink></li>
<li><NavLink to="/about" activeClassName="actyMcActiveFace">About</NavLink></li>
```



### Redirecting a Route

React Router provides an `<Redirect>` component that instructs the router to redirect form one route to another.

```jsx
// Example in Courses.js
<Route exact path="/courses" render={ () => <Redirect to="/courses/html" /> } />
```



### Using the Match Object

The `match` object contains information about how a route is matching the URL. We can access this data form inside components being rendered by `<Route>`. Here, we'll use `match` to dynamically match `<Route>` and `<NavLink>` to the current URL and path.

```jsx
const Courses = ({match}) => (
  <div className="main-content courses">
    <div className="course-header group">
      <h2>Courses</h2> 
      <ul className="course-nav">
        <li><NavLink to={`${match.url}/html`}>HTML</NavLink></li>
        <li><NavLink to={`${match.url}/css`}>CSS</NavLink></li>
        <li><NavLink to={`${match.url}/javascript`}>JavaScript</NavLink></li>
      </ul>
    </div>
    
    <Route exact path={match.path} render={ () => <Redirect to={`${match.path}/html`} /> } />
    <Route path={`${match.path}/html`} component={HTML} />
    <Route path={`${match.path}/css`} component={CSS} />
    <Route path={`${match.path}/javascript`} component={Javascript} />
  </div>
);
```

