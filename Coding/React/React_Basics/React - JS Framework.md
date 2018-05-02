# React - JS Framework 

> Note: This is a teamtreehouse.com Course



# React Basics



### First Steps in React

#### Why React

React provides a powerfull toolset that utilizes a virtual dom to keep the browser and datamodel in sync.

##### New Terms:

- **Imperative:** A programming model where we describe the steps to achieve our result. (ie. javascript)
- **Declarative:** A programing model where we describe the result we want to achieve. (ie. html)
- **Component:** A self-contained, resusable piece of our interface. (A funamental part of react) 



#### State and the Virtual DOM

A react component will create a representation of its markup in JavaScript, using basic JavaScript data types, like objects, arrays, and strings. This JavaScript representation of the DOM elements is called the Virtual DOM in react.

##### New Terms:

- **DOM:** (Document Object Model) The interface for managing the elements in an HTML page.
- **Virtual DOM:** A pure Javascript representation of a DOM tree.



#### Understanding JSX

JSX is a tool, that while not required, makes working with React much easier to write and understand.

Instead of writing...

```jsx
var myLink = React.createElement('a', {
    href: "https://teamtreehouse.com"
}, "Treehouse");
```

We can write…

```jsx
var myLink = (
	<a href="https://teamtreehouse.com">Treehouse</a>
);
```

##### New Terms:

- **JSX:** An extension to the JavaScript language that provides an XML syntax.
- **Babel.js:** A complier that creates standard, compatible Javascript from code that utilzes new JavaScript features and JSX.




------



### Thinking in Components

#### Mocking up our Application

Example elements using `className` to set the class of the element.

```jsx
<div className="application"></div>
<button className="counter-action increment"> + </button>
```



#### Properties

An example of using properties or "props".

> Note: Props passed to a component should not be changed by that component.

 ```jsx
function Application(props) {
    return (
      <div className="header">
        <h1>{props.title}</h1> // Note: you cannot use if / else statements inside JSX expressions.
      </div>
    )
}

ReactDOM.render(<Applicatoin title="My Title" />, document.getElementById('container'));
 ```



#### PropTypes and DefaultProps

> Note: PropTypes and DefaultProps are NOT required.

```jsx
function Application(props) {
    return ()
}

Application.propTypes = {
    title: React.PropTypes.string.isRequired,  // The console will error if the type is not a string or is missing.
};

Application.defaultProps = {
  title: "Scoreboard", // 'isRequired' from above is unnecessary with a default prop.  
};

ReactDOM.render(<Applicatoin title="My Title" />, document.getElementById('container'));
```



#### Decomposing our Application

Here is an example of extracting parts of the application code into smaller and reusable chunks

```jsx
function Header(props) {
  return (
    <div className="header">
      <h1>{props.title}</h1>
    </div>
  );
}

Header.propTypes = {
  title: React.PropTypes.string.isRequired,
}

function Player(props) {
    return (
      ...   
    );
}

function Application(props) {
  return (
    <div className="scoreboard">
      <Header title={props.title} />
      ...
          <Player name="The Name" score={10} />
      ...
  )
}
```

##### New Terms:

- Composition: A method of combining many smaller or simpler pieces to create a larget piece.
- Decompose: Break a large component in to smaller components that can be composed together.




#### Loops and Lists in JSX

An examply of an array used for a prop

```jsx
var PLAYERS = [
  {
    name: "Will Saults",
    score: 31,
    id: 1,
  },
  {
    name: "Wade Watts",
    score: 8,
    id: 2,
  },
];
```

You can simply specify that the players prop is a required array. 

```jsx
Application.propTypes = {
  players: React.PropTypes.array.isRequired,
};
```

You can specifiy that an array should be of a certain type. In this case it requires an object.

```jsx
Application.propTypes = {
  players: React.PropTypes.arrayOf(React.PropTypes.object).isRequired,
};
```

Going a step further allows you to specify the objects inside the array.

```jsx
Application.propTypes = {
  players: React.PropTypes.arrayOf(React.PropTypes.shape({
    name: React.PropTypes.string.isRequired,
    score: React.PropTypes.number.isRequired,
    id: React.PropTypes.number.isRequired,
  })).isRequired,
};
```

Using the map function to iterate over and array:

```jsx
<div className="players">
	{props.players.map(function(player) {
		return <Player name={player.name} score={player.score} key={player.id} />
	})}
</div>
```

> Note: Not only is a key required when generating a list, it also helps react know if the list is simply reordered rather than having to rerender the content of the list.



------



### Stateful Components

#### Creating a Component Class

The SFC counter function from above can be converted to this component class.

> Note: use `this.props.score` to access the props of the new class.

```jsx
var Counter = React.createClass({
  propTypes: {
  	score: React.PropTypes.number.isRequired,      
  },
  render: function() {
    return (
    <div className="counter">
      <button className="counter-action decrement"> - </button>
      <div className="counter-score"> {this.props.score} </div>
      <button className="counter-action increment"> + </button>
    </div>
    );
  }
});
```

##### New Terms:

- **Stateless Functional Component (SFC):** A component defined as a function. It takes only props as an argument and returns a virtual DOM.
- **Component Class:** A component definition that can include things like state., helper methods and other advanced hooks into the page's DOM.



#### Understanding State

> State is just data that changes over time.
>
> Note: `this.props.score` changes to `this.state.score` and score can be removed from propTypes.

```jsx
var Counter = React.createClass({
  ... // score can be removed from propTypes
  getInitialState: function() {
    return {
      score: 0
    }
  },
  
  render: function() {
    return (
    <div className="counter">
      <button className="counter-action decrement"> - </button>
      <div className="counter-score"> {this.state.score} </div>
      <button className="counter-action increment"> + </button>
    </div>
    );
  }
});

...
<Counter /> // the score can be removed from the Counter element
...
```

##### New Terms:

- `getInitialState`: Component method for defining the initla state of your component.
- **Flux:** A pattern for organizing your state in an applicatoin. https://facebook.github.io/flux/
- **Redux:** A popular library for managing application state and state changes. http://redux.js.org/index.html



#### Updating State

The following can be added to the Counter class.

```jsx
incrementScore: function() {
    this.setState({ // Notifies the counter class that its state has been updated.
      score: (this.state.score + 1),
    })
}

<button className="counter-action increment" onClick={this.incrementScore}> + </button>
```



------



### Designing Data Flow

#### Unidirectional Data Flow

There are two types of state: Applicatoin state and Component state.

> Note: A component only knows about itself, the properties that were passed to it, and the children the component may render.

##### Key Terms:

- **Unidiretional Data Flow:** All data in our application flow in a single direction. In React it flows down the tree from parent to child. This makes tracking the source and destination easy compared to other architectures where data may be coming form many parts of the application.
- **Applicatoin State:** The state or data in our application that is core to the functionality of the application as a whole. This usually includes a list of the models and data being manipulated by the interface. If we were to reload our application, the Application state is what we would like to persist the most.
- **Local Component State:** This is state that is sued ot allow a component to function. Local component state is typically not used by other components in the application, and is less important to persist if the applicaiton resets.



#### Communicating Events

Using `onChange` to handle score changes so that the parent will know that the value has changed.

```jsx
Counter.propTypes = {
  ...
  onChange: React.PropTypes.func.isRequired,
};

// The button uses an anonymous function to pass the change.
<button className="counter-action increment" onClick={function() {props.onChange(1);}}> + </button>

// Player uses onScoreChange to relay the change to the Application
Player.propTypes = {
  ...
  onScoreChange: React.PropTypes.func.isRequired,
};

// Player passes onScoreChange to the counter
<Counter score={props.score} onChange={props.onScoreChange} />


// Inside application we can specifiy an onScoreChange function to be passed to the player and called at a later time.
onScoreChange: function(index, delta) {
    this.state.players[index].score += delta;
    this.setState(this.state);
},

...
// Inside the application players can use onScoreChange but it must bind the scope of 'this' before it will recognise this.onScoreChange as belonging to the this outside of the map.
<div className="players">
        {this.state.players.map(function(player, index) {
          return (
            <Player 
              onScoreChange={function(delta) {this.onScoreChange(index, delta)}.bind(this)}
              name={player.name} 
              score={player.score}
              key={player.id} />
          )
        }.bind(this))}
      </div>
```



#### Building the Statistics Component

> Note: It's important to add a `<tbody>` and a `<thead>` when buildng a table in React because the browser will automatically add one for you if you didn't. This causes problems for React because the virtual DOM is trying to manage the actual DOM but the browser is modifying it underneath you.

```jsx
function Stats(props) {
  var totalPlayers = props.players.length;
  var totalPoints = props.players.reduce(function(total, player){
    return total + player.score;
  }, 0);
  
  return(
    <table className="stats">
      <tbody>
        <tr>
          <td>Players:</td>
          <td>{totalPlayers}</td>
        </tr>
        <tr>
          <td>Total Points:</td>
          <td>{totalPoints}</td>
        </tr>
      </tbody>
    </table>
  )
}
  
Stats.propTypes = {
  players: React.PropTypes.array.isRequired,
};
```



#### Adding Players to the Scoreboard

```jsx
var AddPlayerForm = React.createClass({
  propTypes: {
    onAdd: React.PropTypes.func.isRequired,
  },
  
  getInitialState: function() {
    return {
      name: "",
    };
  },
  
  onNameChange: function(e) {
    this.setState({name: e.target.value});
  },
  
  onSubmit: function(e) {
    e.preventDefault(); // Prevents the page from reloading just as expected.
  
    this.props.onAdd(this.state.name);
    this.setState({name: ""});
  },
  
  render: function() {
    return (
      <div className="add-player-form">
      <form onSubmit={this.onSubmit}>
        <input type="text" value={this.state.name} onChange={this.onNameChange} />
        <input type="submit" value="Add Player" />
      </form>
      </div>
    );
  }
});

...
// Inside application
onPlayerAdd: function(name) {
    this.state.players.push({
      name: name,
      score: 0,
      id: nextId, // nextId is a global var
    });
    this.setState(this.state); // The normal way would be to create a new state. This is just a stop-gap solution.
    nextId += 1;
}

... 
// Inside the application render
<AddPlayerForm onAdd={this.onPlayerAdd}/>
```



##### New Terms:

- **Controlled Component:** An input form is controlled when it's value is passed to it by the parent component. This requires us to update the passed value when it changes by listening for the onChange event of the input component.



------



### Component Lifecycle



#### Designing the Stopwatch

```jsx
var Stopwatch = React.createClass({
  getInitialState: function() {
    return {
      running: false,
      elapsedTime: 0,
      previousTime: 0,
    }
  },
  
  // componentDidMount() is invoked immediately after a component is mounted.
  componentDidMount: function() {
    this.interval = setInterval(this.onTick, 100);
  },
  
  // componentWillUnmount() is invoked immediately before a component is unmounted and destroyed.
  componentWillUnmount: function() {
    clearInterval(this.interval);
  },
  
  onTick: function() {
    if (this.state.running) {
      var now = Date.now();
      this.setState({
        previousTime: now,
        elapsedTime: this.state.elapsedTime + (now - this.state.previousTime),
      });
    }
  },
  
  onStart: function() {
    this.setState({ 
      running: true,
      previousTime: Date.now(),
    });
  },
  
  onStop: function() {
    this.setState({ running: false });
  },
  
  onReset: function() {
    this.setState({
      elapsedTime: 0,
      previousTime: Date.now(),
    });
  },
  
  render: function() {
    var seconds = Math.floor(this.state.elapsedTime / 1000);
    return (
      <div className="stopwatch">
        <h2>Stopwatch</h2>
        <div className="stopwatch-time">{seconds}</div>
        { this.state.running ? 
          <button onClick={this.onStop}>Stop</button> : 
          <button onClick={this.onStart}>Start</button> }
        <button onClick={this.onReset}>Reset</button>
      </div>
    );
  }
});
```





------



### The full jsx...

```jsx
var PLAYERS = [
  {
    name: "Jim Hoskins",
    score: 31,
    id: 1,
  },
  {
    name: "Andrew Chalkley",
    score: 35,
    id: 2,
  },
  {
    name: "Alena Holligan",
    score: 42,
    id: 3,
  },
];
var nextId = 4;
var Stopwatch = React.createClass({
  getInitialState: function() {
    return {
      running: false,
      elapsedTime: 0,
      previousTime: 0,
    }
  },
  
  componentDidMount: function() {
    this.interval = setInterval(this.onTick, 100);
  },
  
  componentWillUnmount: function() {
    clearInterval(this.interval);
  },
  
  onTick: function() {
    if (this.state.running) {
      var now = Date.now();
      this.setState({
        previousTime: now,
        elapsedTime: this.state.elapsedTime + (now - this.state.previousTime),
      });
    }
  },
  
  onStart: function() {
    this.setState({ 
      running: true,
      previousTime: Date.now(),
    });
  },
  
  onStop: function() {
    this.setState({ running: false });
  },
  
  onReset: function() {
    this.setState({
      elapsedTime: 0,
      previousTime: Date.now(),
    });
  },
  
  render: function() {
    var seconds = Math.floor(this.state.elapsedTime / 1000);
    return (
      <div className="stopwatch">
        <h2>Stopwatch</h2>
        <div className="stopwatch-time">{seconds}</div>
        { this.state.running ? 
          <button onClick={this.onStop}>Stop</button> : 
          <button onClick={this.onStart}>Start</button> }
        <button onClick={this.onReset}>Reset</button>
      </div>
    );
  }
});
  
var AddPlayerForm = React.createClass({
  propTypes: {
    onAdd: React.PropTypes.func.isRequired,
  },
  
  getInitialState: function() {
    return {
      name: "",
    };
  },
  
  onNameChange: function(e) {
    this.setState({name: e.target.value});
  },
  
  onSubmit: function(e) {
    e.preventDefault();
  
    this.props.onAdd(this.state.name);
    this.setState({name: ""});
  },
  
  
  render: function() {
    return (
      <div className="add-player-form">
        <form onSubmit={this.onSubmit}>
          <input type="text" value={this.state.name} onChange={this.onNameChange} />
          <input type="submit" value="Add Player" />
        </form>
      </div>
    ); 
  }
});
  
function Stats(props) {
  var totalPlayers = props.players.length;
  var totalPoints = props.players.reduce(function(total, player){
    return total + player.score;
  }, 0);
  
  return (
    <table className="stats">
      <tbody>
        <tr>
          <td>Players:</td>
          <td>{totalPlayers}</td>
        </tr>
        <tr>
          <td>Total Points:</td>
          <td>{totalPoints}</td>
        </tr>
      </tbody>
    </table>
  )  
}
  
Stats.propTypes = {
  players: React.PropTypes.array.isRequired,
};

function Header(props) {
  return (
    <div className="header">
      <Stats players={props.players}/>
      <h1>{props.title}</h1>
      <Stopwatch />
    </div>
  );
}

Header.propTypes = {
  title: React.PropTypes.string.isRequired,
  players: React.PropTypes.array.isRequired,
};

function Counter(props) {
  return (
    <div className="counter">
      <button className="counter-action decrement" onClick={function() {props.onChange(-1);}} > - </button>
      <div className="counter-score"> {props.score} </div>
      <button className="counter-action increment" onClick={function() {props.onChange(1);}}> + </button>
    </div>
  );
}
  
Counter.propTypes = {
  score: React.PropTypes.number.isRequired,
  onChange: React.PropTypes.func.isRequired,
}

function Player(props) {
  return (
    <div className="player">
      <div className="player-name">
        <a className="remove-player" onClick={props.onRemove}>✖</a>
        {props.name}
      </div>
      <div className="player-score">
        <Counter score={props.score} onChange={props.onScoreChange} />
      </div>
    </div>
  );
}

Player.propTypes = {
  name: React.PropTypes.string.isRequired,
  score: React.PropTypes.number.isRequired,
  onScoreChange: React.PropTypes.func.isRequired,
  onRemove: React.PropTypes.func.isRequired,
};

var Application = React.createClass({
  propTypes: {
    title: React.PropTypes.string,
    initialPlayers: React.PropTypes.arrayOf(React.PropTypes.shape({
      name: React.PropTypes.string.isRequired,
      score: React.PropTypes.number.isRequired,
      id: React.PropTypes.number.isRequired,
    })).isRequired,
  },
  
  getDefaultProps: function() {
    return {
      title: "Scoreboard",
    }
  },
  
  getInitialState: function() {
    return {
      players: this.props.initialPlayers,
    };
  },
  
  onScoreChange: function(index, delta) {
    this.state.players[index].score += delta;
    this.setState(this.state);
  },
    
  onPlayerAdd: function(name) {
    this.state.players.push({
      name: name,
      score: 0,
      id: nextId,
    });
    this.setState(this.state);
    nextId += 1;
  },
    
  onRemovePlayer: function(index) {
    this.state.players.splice(index, 1);
    this.setState(this.state);
  },
  
  render: function() {
    return (
      <div className="scoreboard">
        <Header title={this.props.title} players={this.state.players} />
      
        <div className="players">
          {this.state.players.map(function(player, index) {
            return (
              <Player 
                onScoreChange={function(delta) {this.onScoreChange(index ,delta)}.bind(this)}
                onRemove={function() {this.onRemovePlayer(index)}.bind(this)}
                name={player.name} 
                score={player.score} 
                key={player.id} />
            );
          }.bind(this))}
        </div>
        <AddPlayerForm onAdd={this.onPlayerAdd} />
      </div>
    );
  }
});  

ReactDOM.render(<Application initialPlayers={PLAYERS}/>, document.getElementById('container'));
```

