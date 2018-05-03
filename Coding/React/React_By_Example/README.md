# React by Example

> Note: This is a team treehouse course found here: https://teamtreehouse.com/library/react-by-example

Learn React programming patterns by building an application for keeping track of RSVP's! We'll start at the beginning, using [create react app](https://github.com/facebookincubator/create-react-app) to initialize the project, and by the end you'll have a functional application.

Topics covered:

- React
- Closures
- Event handling
- JSX




## Setting up with Create React App

### Setting up the Project

The project can be found here: https://github.com/wsaults/react-by-example



### Initialize the State

Added a state object to hold the guests.

```jsx
class App extends Component {

  state = {
    guests: [
      {
        name: 'Will',
        isConfirmed: false
      },
      {
        name: 'Johnny',
        isConfirmed: true
      }
    ]
  }

  getTotalInvited = () => this.state.guests.length;
...
```



------



## Building the Application



### Building the GuestList Component

> Note: used `npm install --save prop-types` at the start of this exercise.

```jsx
import React from 'react';
import PropTypes from 'prop-types';

const GuestList = props => 
    <ul>
        {props.guests.map((guest, index) => 
            <li key={index}> // A key is required
                <span>{guest.name}</span>
                <label>
                    <input type="checkbox" checked={guest.isConfirmed} /> Confirmed
                </label>
                <button>edit</button>
                <button>remove</button>
            </li>
        )}
    </ul>

GuestList.propTypes = {
    guests: PropTypes.array.isRequired
}

export default GuestList;

// Inside App.js
<GuestList guests={this.state.guests} /> // Passing the state to the GuestList
```





### Writing a Handler to Confirm Guests

> Note: the handler will be passed down to allow the App to responde to changes.

```jsx
// Inside App.js
toggleConfirmationAt = indexToChange => 
    this.setState({
      guests: this.state.guests.map((guest, index) => {
        if (index === indexToChange) {
          return {
            ...guest, // The spread operator transfers the keys and props from one obj to another.
            isConfirmed: !guest.isConfirmed
          }
        }

        return guest; // Returns the untouched object if there is no change.
      })
    });
```



### Connecting the Confirm Guests Handler

> Note: Function retain access to the scope in which they were defined. This is known as a closure.

Inside App.js

```jsx
<GuestList 
	guests={this.state.guests} 
	toggleConfirmationAt={this.toggleConfirmationAt} /> // Pass toggleConfirmationAt
```

Inside GuestList.js	

```jsx
<Guest 
...
	handleConfirmation={() => props.toggleConfirmationAt(index)} /> // Pass toggleConfirmationAt
```

Inside Guest.js

```jsx
<input 
	...
	onChange={props.handleConfirmation} /> Confirmed // Invoke the toggleConfirmationAt handler
```

> Note: When a user clicks a connected form element in a React app...
>
> …ths state is set first, then the element changes to show the new state.



### Toggling Edit State for Guests

Using the isEditing prop to dynamically change the UI.

```jsx
const GuestName = props => {
  if (props.isEditing) {
    return (
      <input type="text" value={props.children} />
    );
  }

  return (
    <span>
      {props.children}
    </span>
  );
}
```



### Changing Guest Name in State

Inside Guest.js

```jsx
<button onClick={props.handleToggleEditing}> // Use onClick to fireHandleToggleEditing
	{props.isEditing ? "save" : "edit"} // Show save or edit depending on isEditing
</button>
```

Inside GuestName.js

```jsx
handleNameEdits={e => props.setName(e.target.value)}>{props.name}</GuestName>
```



### Filtering Guests

Added `.filter` to remove guests that have not confirmed. The filter is only invoked when the isFiltered property is true.

```jsx
const GuestList = props => 
    <ul>
        {props.guests
            .filter(guest => !props.isFiltered || guest.isConfirmed)
            .map((guest, index) => 
            <Guest 
                key={index} 
                name={guest.name} 
                isConfirmed={guest.isConfirmed}
                isEditing={guest.isEditing}
                handleConfirmation={() => props.toggleConfirmationAt(index)} 
                handleToggleEditing={() => props.toggleEditingAt(index)} 
                setName={text => props.setNameAt(text, index)} />
        )}
    </ul>

GuestList.propTypes = {
    guests: PropTypes.array.isRequired,
    toggleConfirmationAt: PropTypes.func.isRequired,
    toggleEditingAt: PropTypes.func.isRequired,
    setNameAt: PropTypes.func.isRequired,
    isFiltered: PropTypes.bool.isRequired
};
```

In App.js

```js
toggleFilter = () =>
    this.setState({ isFiltered: !this.state.isFiltered });

// GuestList accepts the following:
isFiltered={this.state.isFiltered}
```



### Adding Guests to the List

In App.js

```jsx
state = {
    ...
    pendingGuest: "", // Add pendingGuest to the state.
    ...
}

// Handler called on submit
newGuestSubmitHandler = e => {
    e.preventDefault(); // Keeps the page from reloading.
    this.setState({ 
      guests: [
        {
          name: this.state.pendingGuest,
          isConfirmed: false,
          isEditing: false
        },
        ...this.state.guests
      ],
      pendingGuest: ''
    });
  }

...

render()

...

<form onSubmit={this.newGuestSubmitHandler}>
    
...

<input 
    type="text"
    onChange={this.handleNameInput} 
    value={this.state.pendingGuest} 
    placeholder="Invite Someone"/>
```



### Removing Names From the List

The removeGuestAt closure will be passed down through GuestList to Guest and invoked by the remove button.

```jsx
removeGuestAt = index =>
    this.setState({
      guests: [
        ...this.state.guests.slice(0, index), // Slice and spread up to the index.
        ...this.state.guests.slice(index + 1) // Then slice and spread after the index.
      ]
    })
```



### Creating the Counter

Calculate the values and pass them to the Counter.

```jsx
getTotalInvited = () => this.state.guests.length;

getAttendingGuests = () =>
	this.state.guests.reduce(
    	(total, guest) => guest.isConfirmed ? total + 1 : total, 
    0); // 0 sets the intial total.
    
    
// These are computed inside the render() and passed into Counter.js
const totalInvited = this.getTotalInvited();
const numberAttending = this.getAttendingGuests();
const numberUnconfirmed = totalInvited - numberAttending;
```



------



## Refining the App



### Refactor App Components

Time to implement the highlighted components.

- App
  - **Header** 
    - **GuestInputForm**
  - **MainContent**
    - **ConfirmedFilter**
    - Counter
    - GuestList
      - PendingGuest
      - Guest
        - GuestName

