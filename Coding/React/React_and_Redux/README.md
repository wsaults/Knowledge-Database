# Buildng Applications with React and Redux

### About this Course

Redux is a state management framework that provides a robust infrastructure that complements React applications. This course will build on the Scoreboard application that was developed in the React Basics course.

#### What you'll learn

- Managing application UI state and Logical state
- Understanding pure functions
- Building a stable and predictable client application
- One-way data binding



## Getting Started with Redux

### What is Redux?

**Terms:**

- **Redux:** A JavaScript framework for managing and maintaining application state usually used in conjunction with other frameworks to build applicatoins.
- **Store:** Refers to the applicatoin state container for the entire application.
- **Actoin:** Refers to an explicit event that occurs within a Redux application that will impact application state.
- **Container:** A React component that subscribes to specific Reducer updates and propagates data to other React components known as presentational components.
- **Immutability:** Refers to an object that cannot be changed once it has been created.



### Redux Initial Setup

Dev Dependencies

```
npm install --save redux react-redux
```

index.js

```
npm install
npm start
```



------



## Modularizing the React Scoreboard Application

### Developing Your Component Hierarchy

**New Terms:**

- **Container Component:** Redux aware component that usually defines no markup of its own but instead relies on composing presentational components into a cohesive UI.
- **Logical Component:** Presentational component that has its own state to manage and may or may not make use of React lifecycle events.
- **Pure Component:** Presentation component that is implemented as a pure funciton. These components are passed props and return markup, no questions asked, no side-effects. That means they do not manage a state of their own and do not take part in React life cycle events.
- **Component Hierarchy:** A composition of React components represented as a tree that depicts the component structure.



### Building the Stopwatch Logical Component

```jsx
import React, { Component, PropTypes } from 'react';

export default class Stopwatch extends Component {
  state = {
    running: false,
    previouseTime: 0,
    elapsedTime: 0,
  };

  componentDidMount() {
    this.interval = setInterval(this.onTick);
  };

  componentWillUnmount() {
    clearInterval(this.interval);
  }

  onStart = () => {
    this.setState({
      running: true,
      previousTime: Date.now(),
    });
  };

  onStop = () => {
    this.setState({
      running: false,
    });
  };

  onReset = () => {
    this.setState({
      elapsedTime: 0,
      previousTime: Date.now(),
    });
  };

  onTick = () => {
    if (this.state.running) {
      var now = Date.now();
      this.setState({
        elapsedTime: this.state.elapsedTime + (now - this.state.previousTime),
        previousTime: Date.now(),
      });
    }
  };

  render() {
    var seconds = Math.floor(this.state.elapsedTime / 1000);
    return (
      <div className="stopwatch" >
        <h2>Stopwatch</h2>
        <div className="stopwatch-time"> {seconds} </div>
        { this.state.running ?
          <button onClick={this.onStop}>Stop</button>
          :
          <button onClick={this.onStart}>Start</button>
        }
        <button onClick={this.onReset}>Reset</button>
      </div>
    )
  };
}
```



### Building the Stats and Counter Pure Component

```jsx
import React, { PropTypes } from 'react';

const Counter = props => {
  return (
    <div className="counter" >
      <button className="counter-action decrement" onClick={() => props.onChange(-1)}>
        -
      </button>
      <div className="counter-score"> {props.score} </div>
      <button className="counter-action increment" onClick={() => props.onChange(1)}>
        +
      </button>
    </div>
  );
 }
 
 Counter.propTypes = {
   onChange: React.PropTypes.func.isRequired,
   score: React.PropTypes.number.isRequired,
 };

 export default Counter;
```



### Building the AddPlayerForm Logical Component

```jsx
import React, { Component, PropTypes } from 'react';

export default class AddPlayerForm extends Component {
  // Using static to perform a property initializer.
  static propTypes: { 
    onAdd: React.PropTypes.func.isRequired,
  };

  state = {
    name: ''
  };

  onNameChange = (e) => {
    const name = e.target.value;
    this.setState({ name: name });
  };

  onSubmit = (e) => {
    if (e) e.preventDefault();
    this.props.onAdd(this.state.name);
    this.setState({ name: '' });
  };

  render() {
    return (
      <div className="add-player-form">
        <form onSubmit={this.onSubmit}>
          <input
            type="text"
            value={this.state.name}
            onChange={this.onNameChange}
            placeholder="Player Name"
          />
          <input type="submit" value="Add Player" />
        </form>
      </div>
    );
  };
}
```



### Building the Player and Header Pure Components

```jsx
import React, { PropTypes } from 'react';
import Stats from './Stats';
import Stopwatch from './Stopwatch';

const Header = props => {
  return (
    <div className="header">
      <Stats players={props.players} />
      <h1>Scoreboard</h1>
      <Stopwatch />
    </div>
  );
}

Header.propTypes = {
  players: PropTypes.array.isRequired, // React.PropTypes can be changed to PropTypes
};

export default Header;
```



### Cleaning up the Scoreboard Container Component

```jsx
import React, { Component } from 'react';
import AddPlayerForm from '../components/AddPlayerForm'
import Player from '../components/Player'
import Header from '../components/Header'

export default class Scoreboard extends Component {
  state = {
    players: [
      {
        name: 'Jim Hoskins',
        score: 31,
      },
      {
        name: 'Andrew Chalkley',
        score: 20,
      },
      {
        name: 'Alena Holligan',
        score: 50,
      },
    ],
  }

  onScoreChange = (index, delta) => {
    this.state.players[index].score += delta;
    this.setState(this.state);
  };

  onAddPlayer = (name) => {
    this.state.players.push({ name: name, score: 0 });
    this.setState(this.state);
  };

  onRemovePlayer = (index) => {
    this.state.players.splice(index, 1);
    this.setState(this.state);
  };

  render() {
    return (
      <div className="scoreboard">
        <Header players={this.state.players} />
        <div className="players">
          {this.state.players.map(function(player, index) {
             return (
               <Player
                 name={player.name}
                 score={player.score}
                 key={player.name}
                 onScoreChange={(delta) => this.onScoreChange(index, delta)}
                 onRemove={() => this.onRemovePlayer(index)}
               />
             );
           }.bind(this))}
        </div>
        <AddPlayerForm onAdd={this.onAddPlayer} />
      </div>
    );
  }
};
```



------



## Actions, Dispatch, and Reducers. Oh my!



### Intro to Action Types

Adding action types to player.js

```js
export const ADD_PLAYER = 'player/ADD_PLAYER';
export const REMOVE_PLAYER = 'player/REMOVE_PLAYER';
export const UPDATE_PLAYER_SCORE = 'player/UPDATE_PLAYER_SCORE';
```



**New Terms:**

- **Action Type:** An action type in Redux represents an explicit action type that will occure within the application. It is express in Javascript as a string constant.



### Intro to Reducers

> Note: Reducers should be written as a pure function and not mutate the state.

```js
// Takes all exports from player.js in actiontypes and sets them as properties on PlayerActoinTypes
import * as PlayerActionTypes from '../actiontypes/player';

const initialState = [
  {
    name: 'Jim Hoskins',
    score: 31,
  },
  {
    name: 'Andrew Chalkley',
    score: 20,
  },
  {
    name: 'Alena Holligan',
    score: 50,
  },
];

// Set the state using the initialState
export default function Player(state=initialState, action) {
  switch(action.type) {
    case PlayerActionTypes.ADD_PLAYER:
    return [
      ...state,
      {
        name: action.name,
        score: 0
      }
    ];

    case PlayerActionTypes.REMOVE_PLAYER:
    return [
      ...state.slice(0, action.index),
      ...state.slice(action.index + 1)
    ];

    case PlayerActionTypes.UPDATE_PLAYER_SCORE:
    return state.map((player, index) => {
      if(index === action.index) {
        return {
          ...player,
          score: player.score + action.score
        };
      }
      return player;
    });

    default:
      return state;
  }
}
```

**New Terms:**

- **Reducer:** A Redux construct that is responsible for maintaining a specific portion of the Redux store, which holds the app's state. In JavaScript, a reducer is implemented as a pure function that takes two arguments, the current state and the aciton being taken, and produces the next state. In order for REdux to work properly, Reducers must not mutate the current state. In other words, the state for a reducer must be treated as immutable.



### Actions and Action Creators

> Note: Action Creators that return an action which ties into the action types and passes the appropriate data.

```js
import * as PlayerActionTypes from '../actiontypes/player';

export const addPlayer = name => {
  return {
    type: PlayerActionTypes.ADD_PLAYER,
    name
  };
};

export const removePlayer = index => {
  return {
    type: PlayerActionTypes.REMOVE_PLAYER,
    index
  };
};

export const updatePlayerScore = (index, score) => {
  return {
    type: PlayerActionTypes.UPDATE_PLAYER_SCORE,
    index,
    score
  };
};
```

**New Terms:**

- **Actions:** Explicit events that occur in our application represented by a type and any relevant metadata associated with the action.
- **Action Creators:** In Redux, a construct for generating an action.



------



## Putting it all Together



### Creating the Redux Store

```jsx
import React from 'react';
import { render } from 'react-dom';
import { Provider } from 'react-redux';
import { createStore } from 'redux';
import PlayerReducer from './src/reducers/player';
import Scoreboard from './src/containers/Scoreboard';

const store = createStore(
  PlayerReducer
);

render(
  <Provider store={store}>
    <Scoreboard />,
  </Provider>,
  document.getElementById('root')
);
```



### Connecting the Scoreboard Container to Redux

```jsx
import React, { Component, PropTypes } from 'react';
import { bindActionCreators } from 'redux';
import { connect } from 'react-redux';
import * as PlayerActionCreators from '../actions/player';
import AddPlayerForm from '../components/AddPlayerForm';
import Player from '../components/Player';
import Header from '../components/Header';

class Scoreboard extends Component {
  
  static propTypes = {
    players: PropTypes.array.isRequired
  };

  render() {
    const { dispatch, players } = this.props;
    const addPlayer = bindActionCreators(PlayerActionCreators.addPlayer, dispatch);
    const removePlayer = bindActionCreators(PlayerActionCreators.removePlayer, dispatch);
    const updatePlayerScore = bindActionCreators(PlayerActionCreators.updatePlayerScore, dispatch);

    const playerComponents = players.map((player, index) => (
      <Player
        index={index}
        name={player.name}
        score={palyer.score}
        key={player.name}
        updatePlayerScore={updatePlayerScore}
        removePlayer={removePlayer}
      />
    ));

    return (
      <div className="scoreboard">
        <Header players={players} />
        <div className="players">
          { playerComponents }
        </div>
        <AddPlayerForm addPlayer={addPlayer} />
      </div>
    );
  }
}

const mapStateToProps = state => (
  {
    players: state
  }
);

export default connect(mapStateToProps)(Scoreboard);
```

> Note: A bound action creator works exactly like a normal action creator, but in addition to generating an action, the action generated is also dispatched to the Redux store immediately.

>  Note: When connecting to Redux, you must provide: A method for mappintStateToProps, and a container

**New Terms:**

- **Bound Action Creator:** An action creator that generates an action and is immediately dispatched to the Redux store.

