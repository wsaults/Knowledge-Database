# Data Fetching in React



## Fetching Data with the Fetch API

```jsx
export default class App extends Component {
  
  constructor() {
    super();
    this.state = {
      gifs: []
    };
  } 

  componentDidMount() {
    // This is a good place because componentDidMount holds a copy of the dom representation.
    fetch('http://api.giphy.com/v1/gifs/trending?api_key=dc6zaTOxFJmzC')
    .then(response => response.json())
    .then(responseData => {
      this.setState({ gifs: responseData.data });
    })
    .catch(error => {
      console.log('Error fetching and parsing data', error);
    });
  }

  render() {
    console.log(this.state.gifs); 
    return (
      <div>
        <div className="main-header">
          <div className="inner">
            <h1 className="main-title">GifSearch</h1>
            <SearchForm />      
          </div>   
        </div>    
        <div className="main-content">
          <GifList />
        </div>
      </div>
    );
  }
}
```



## Fetching Data with Axios

Axios: a promised-based library that's similar to the Fetch API. In addition to having stronger browser support than fetch(), Axios provides many useful built-in features.

```
npm install --save axios
```

```jsx
export default class App extends Component {
  
  constructor() {
    super();
    this.state = {
      gifs: []
    };
  } 

  componentDidMount() {
    axios.get('http://api.giphy.com/v1/gifs/trending?api_key=dc6zaTOxFJmzC')
      .then(response => {
        this.setState({
          gifs: response.data.data
        });
      })
      .catch(error => {
        console.log('Error fetching and parsing data', error);
      });
  }

  render() {
    console.log(this.state.gifs); 
    return (
      <div>
        <div className="main-header">
          <div className="inner">
            <h1 className="main-title">GifSearch</h1>
            <SearchForm />      
          </div>   
        </div>    
        <div className="main-content">
          <GifList />
        </div>
      </div>
    );
  }
}
```



## Displaying the Data

App.js

```jsx
 <GifList data={this.state.gifs}/>
```

GifList.js

```jsx
const GifList = props => { 

  const results = props.data;
  let gifs = results.map(gif => 
    <Gif url={gif.images.fixed_height.url} key={gif.id} />
  );
  
  return(
    <ul className="gif-list">
      {gifs}
    </ul> 
  );
}
```

Gif.js

```jsx
const Gif = props => (
  <li className="gif-wrap">
    <img src={props.url} alt=""/>
  </li>
);
```



## Building a Search Feature

App.js

```jsx
performSearch = (query) => {
    axios.get(`http://api.giphy.com/v1/gifs/search?q=${query}&limit=24&api_key=dc6zaTOxFJmzC`)
      .then(response => {
        this.setState({
          gifs: response.data.data
        });
      })
      .catch(error => {
        console.log('Error fetching and parsing data', error);
      });
  }


...

<SearchForm onSearch={this.performSearch} />  
```

SearchForm.js

```jsx
handleSubmit = e => {
    e.preventDefault();
    this.props.onSearch(this.state.searchText);
    e.currentTarget.reset();
  }
```



## Displaying the Search Results

SearchForm.js

```jsx
handleSubmit = e => {
    e.preventDefault();
    this.props.onSearch(this.query.value);
    e.currentTarget.reset();
  }

render() {  
    return (
      <form className="search-form" onSubmit={this.handleSubmit} >
        <label className="is-hidden" htmlFor="search">Search</label>
        <input type="search" 
               onChange={this.onSearchChange}
               name="search"
               ref={(input) => this.query = input} 
               placeholder="Search..." />
        <button type="submit" id="submit" className="search-button"><i className="material-icons icn-search">search</i></button>
      </form>      
    );
  }
```

