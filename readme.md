#1 Simple element
```javascript
ReactDOM.render(
  <h1>Hello React!</h1>,
  document.getElementById('app')
);

```	
#2 JSX
```javascript
var Greeter = React.createClass({
  render: function () {
    return (
      <div>
        <h1>Hello React!</h1>
        <p>This is form a component!</p>
      </div>
    );
  }
});

ReactDOM.render(
  <Greeter/>,
  document.getElementById('app')
);
```
#3 Properties
` getDefaultProps:`

`<Greeter name={firstName}`

` <h1>Hello {name}!</h1>`

```javascript
var Greeter = React.createClass({
  getDefaultProps: function () {
    return {
      name: 'React',
      message: 'This is the default message!'
    };
  },
  render: function () {
    var name = this.props.name;
    var message = this.props.message;

    return (
      <div>
        <h1>Hello {name}!</h1>
        <p>{message + '!!'}</p>
      </div>
    );
  }
});

var firstName = 'Andrew';

ReactDOM.render(
  <Greeter name={firstName} message= 'This is the message!'/>,
  document.getElementById('app')
);

```
#4 Input
`<form onSubmit={this.onButtonClick}>`

`var name = this.refs.name.value;`

```javascript
var Greeter = React.createClass({
  getDefaultProps: function () {
    return {
      name: 'React',
      message: 'This is the default message!'
    };
  },
  onButtonClick: function (e) {
    e.preventDefault(); // prevent page refresh

    var name = this.refs.name.value;

    alert(name);
  },
  render: function () {
    var name = this.props.name;
    var message = this.props.message;

    return (
      <div>
        <h1>Hello {name}!</h1>
        <p>{message + '!!'}</p>

        <form onSubmit={this.onButtonClick}>
          <input type="text" ref="name"/>
          <button>Set Name</button>
        </form>
      </div>
    );
  }
});

var firstName = 'Andrew';

ReactDOM.render(
  <Greeter name={firstName}/>,
  document.getElementById('app')
);

```
#5 State
States will be updated, props no.

` getInitialState: function () {`

`var name = this.state.name;`

`this.setState({name: name });`

```javascript

	var Greeter = React.createClass({
	  getDefaultProps: function () {
	    return {
	      name: 'React',
	      message: 'This is the default message!'
	    };
	  },
	  getInitialState: function () {
	    return {
	        name: this.props.name
	    };
	  },
	  onButtonClick: function (e) {
	    e.preventDefault();

	    var nameRef = this.refs.name;
	    var name = nameRef.value;
	    nameRef.value = '';

	    if (typeof name === 'string' && name.length > 0) {
	      this.setState({
	        name: name
	      });
	    }
	  },
	  render: function () {
	    var name = this.state.name;
	    var message = this.props.message;

	    return (
	      <div>
	        <h1>Hello {name}!</h1>
	        <p>{message + '!!'}</p>

	        <form onSubmit={this.onButtonClick}>
	          <input type="text" ref="name"/>
	          <button>Set Name</button>
	        </form>
	      </div>
	    );
	  }
	});

	var firstName = 'Andrew';

	ReactDOM.render(
	  <Greeter name={firstName}/>,
	  document.getElementById('app')
	);

```
#6 Nested Components
States can be changed.   
Props can't.   
CONTAINER: maintain  state. only render children
PRESENTATIONAL: Print something,  (don't maintain state)  

```javascript

	var GreeterMessage = React.createClass({
	    render: function () {
	      return (
	        <div>
	          <h1>Some H1</h1>
	          <p>Some paragraph</p>
	        </div>
	      );
	    }
	});

	var GreeterForm = React.createClass({
	  render: function () {
	    return (
	      <form>
	        <input type="text" ref="name"/>
	        <button>Set Name</button>
	      </form>
	    );
	  }
	});

```

```javascript
	
	// PRESENTATIONAL: Print somthing (don't maintain state)  //
	var GreeterMessage = React.createClass({
	    render: function () {
	      var name = this.props.name;
	      var message = this.props.message;

	      return (
	        <div>
	          <h1>Hello {name}!</h1>
	          <p>{message}</p>
	        </div>
	      );
	    }
	});

	// PRESENTATIONAL: Print somthing (don't maintain state)  //
	var GreeterForm = React.createClass({
	  onFormSubmit: function (e) {
	    e.preventDefault();

	    var name = this.refs.name.value;

	    if (name.length > 0) {
	      this.refs.name.value = '';
	      this.props.onNewName(name);
	    }
	  },
	  render: function () {
	    return (
	      <form onSubmit={this.onFormSubmit}>
	        <input type="text" ref="name"/>
	        <button>Set Name</button>
	      </form>
	    );
	  }
	});

	// CONTAINER: maintain  state. only render children//
	var Greeter = React.createClass({
	  getDefaultProps: function () {
	    return {
	      name: 'React',
	      message: 'This is the default message!'
	    };
	  },
	  getInitialState: function () {
	    return {
	        name: this.props.name
	    };
	  },
	  handleNewName: function (name) {
	    this.setState({
	      name: name
	    });
	  },
	  render: function () {
	    var name = this.state.name;
	    var message = this.props.message;

	    return (
	      <div>
	        <GreeterMessage name={name} message={message}/>
	        <GreeterForm onNewName={this.handleNewName}/>
	      </div>
	    );
	  }
	});

	var firstName = 'Andrew';

	ReactDOM.render(
	  <Greeter name={firstName}/>,
	  document.getElementById('app')
	);
```

##WEBPACK

sudo npm install -g webpack

npm install react reac-dom
npm install --save-dev webpack babel-core babel-loader babel-preset-es2015 babel-preset-react


Origin->Destiny
webpack ./public/app.js ./public/bundle.js

###webpack.config.js
```json

	module.exports = {
	  entry: './public/app.js',
	  output: {
	    path: __dirname,
	    filename: './public/bundle.js'
	  },
	  resolve: {
	    extensions: ['', '.js', '.jsx']
	  }
	};
```
###Bable jsx loader
```json

	module.exports = {
	  entry: './public/app.jsx',
	  output: {
	    path: __dirname,
	    filename: './public/bundle.js'
	  },
	  resolve: {
	    extensions: ['', '.js', '.jsx']
	  },
	  module: {
	    loaders: [
	      {
	        loader: 'babel-loader',
	        query: {
	          // parse them through react and run them in es2015 		
	          presets: ['react', 'es2015']
	        },
	        // get the jsx files
	        test: /\.jsx?$/,
	        //ignore this folders
	        exclude: /(node_modules|bower_components)/ 
	      }
	    ]
	  }
	};

###Webpack aliases
```json

	module.exports = {
	    entry: './public/app.jsx',
	    output: {
	      path: __dirname,
	      filename: './public/bundle.js'
	    },
	    resolve: {
	      root: __dirname,
	      alias: {
	        Greeter: 'public/components/Greeter.jsx',
	        GreeterMessage: 'public/components/GreeterMessage.jsx',
	        GreeterForm: 'public/components/GreeterForm.jsx'
	      },
	      extensions: ['', '.js', '.jsx']
	    },
	    module: {
	      loaders: [
	        {
	          loader: 'babel-loader',
	          query: {
	            presets: ['react', 'es2015']
	          },
	          test: /\.jsx?$/,
	          exclude: /(node_modules|bower_components)/
	        }
	      ]
	    }
	  };
```
###EXperimental
`npm install --save-dev babel-preset-stage-0`
In Webpack: `presets: ['react', 'es2015','stage-0']`
#5.-Routing
`npm install react-router --save`

##Object Destructuring 
```javascript

	var obj = {name:'Hugo'}
	var {name} = obj <===> var name = obj.name
```

##Basic Routing
```html

	ReactDOM.render(
	  <Router history={hashHistory}>
	    <Route path="/" component={Main}>

	    </Route>
	  </Router>,
	  document.getElementById('app')
	);
```
## Basic Main Component
```javascript

	var React = require('react');

	var Main = React.createClass({
	  render: function () {
	    return (
	     //The HTML/Components we want to render inside
	    );
	  }
	});

	module.exports = Main;

```

##Routing 
3 Parts

###1 The Router Object
Is in the app.jsx. In the entry point of the app.  

The _Router_ is the main component `<Router history={hashHistory}>` it needs the history to handle the backs.  

Inside the _Router_ there is the main _Route_ where we set which will be children elements and theirs routes.`<Route path="/" component={Main}>`   

Inside the main _Route_ there are the child Routes `<Route path="about" component={About}/>` and the _IndexRoute_ that is the route that will be render when we are in `"/"` 


```javascript

	ReactDOM.render(
		<Router history={hashHistory}>
	    	<Route path="/" component={Main}>
		    	<Route path="about" component={About}/>
		    	<Route path="examples" component={Examples}/>
	    		<IndexRoute component={Weather}/>
	    	</Route>
	    </Router>,
	  document.getElementById('app')
	);
```
###2 Main

The _Main_ object will be in charge of rendering the different pages of the  routing, therefore we need to set where we want the children to be rendered `{this.props.children}` 

```javascript

	var Main = React.createClass({
	  render: function () {
	    return (
	      <div>
	        <Nav/>
	        <h2>Main Component</h2>
	        {this.props.children}
	      </div>
	    );
	  }
	});
```


###3 Nav
In the Navigator component we can set `Links` that will redirect the app to the pages we want to show.

});```javascript

	var Nav = React.createClass({
	  render: function () {
	    return (
	      <div>
	        <h2>Nav Component</h2>
	        <Link to="/">Get Weather</Link>
	        <Link to="/about">About</Link>
	        <Link to="/examples">Examples</Link>
	      </div>
	    );
	  }
	});



##Links
IndexLink is the one set to the index: route `/` so React do not mess up other properties. 

`activeClassName` is used to know wich page/link is active in any moment.

```javascript

	var {Link, IndexLink} = require('react-router');

	var Nav = React.createClass({
	  render: function () {
	    return (
	      <div>
	        <h2>Nav Component</h2>
	        <IndexLink to="/" activeClassName="active" activeStyle={{fontWeight: 'bold'}}>Get Weather</IndexLink>
	        <Link to="/about" activeClassName="active"  activeStyle={{fontWeight: 'bold'}}>About</Link>
	        <Link to="/examples" activeClassName="active" activeStyle={{fontWeight: 'bold'}}>Examples</Link>
	      </div>
	    );
	  }
	});
```

#Promises
##Promises vs Callbacks
Callbacks can be call several times.`callback(undefined, 78); callback('City not found');` and every time they will run its code.
Callbacks need to handle error messages in an ugly way.
```javascript

	function getTempCallback (location, callback) {
	   callback(undefined, 78);
	   callback('City not found');
	 }

	 getTempCallback('Philadelphia', function (err, temp) {
	   if (err) {
	     console.log('error', err);
	   } else {
	     console.log('success', temp)
	   }
	 });
```

Promises call `resolve` or `reject` never both.
Handling errors or success is much easier and clean.
`then` is used to wait for the resolution of the promise.
```javascript

	 function getTempPromise (location) {
	   return new Promise(function (resolve, reject) {
	       resolve(79);
	       reject('City not found');// This will never be called
	   });
	 }

	 getTempPromise('Philadelphia').then(function (temp) { 
	   console.log('promise success', temp);
	 }, function (err) {
	   console.log('promise error', err);
	 });
```

#Conditional Rendering
Add a function inside the render that returns a JSX file, and call it from inside the _return_ of the _render_ `{renderMessage()}`

```javascript

	render: function () {
  	var {isLoading, temp, location} = this.state;

    function renderMessage () {
      if (isLoading) {
        return <h3>Fetching weather...</h3>;
      } else if (temp && location) {
        return <WeatherMessage temp={temp} location={location}/>;
      }
    }
    return (
    	<div>
        <h3>Weather</h3>
        <WeatherForm onSearch={this.handleSearch}/>
        {renderMessage()}
		</div>
    );
  }
```
#Debugging
In Chrome install `React Developer Tools`

Add `debugger;` to add a breackpoint

Add `devtool: "eval-source-map"` to see in the console the source code as we have it (without the webpack processing).

#Arrow Functions
###EXAMPLE: Anonymous functions vs arrow functions
 
 ```javascript
 	
 	var names = ['Andrew', 'Julie', 'Jen'];

	 names.forEach(function (name) {
	   console.log('forEach', name);
	 });

	 names.forEach((name) => {
	   console.log('arrowFunc', name);
	 });

	 names.forEach((name) => console.log(name));
```

###EXAMPLE: Implicit return values
```javascript

	var returnMe = (name) => name + '!';
	console.log(returnMe('Andrew'));

```

#Render Only Components

We can substitute the way we create them

```javascript

	var About = (props) => {
	  return (
	    <h3>About Component</h3>
	  )
	};

```

```javascript

	var WeatherMessage = ({temp, location}) => {
	  return (
	    <h3>It's it {temp} in {location}.</h3>
	  )
	};

```

#Styling
npm install css-loader script-loader style-loader jquery foundation-sites --save-dev

##Update Webpack entries
```javascript

	var webpack = require('webpack');

	module.exports = {
	  entry: [
		'script!jquery/dist/jquery.min.js',
		'script!foundation-sites/dist/foundation.min.js',
		'./app/app.jsx'
		],
	  externals: {
	    jquery: 'jQuery'
	  },
	  plugins: [
	    new webpack.ProvidePlugin({
	      '$': 'jquery',
	      'jQuery': 'jquery'
	    })
	  ],
	  ...
```
## Add CSS
**app.jsx**
```javascript
	
	// App css
	require('style!css!applicationStyles');

	// Load foundation
	require('style!css!foundation-sites/dist/foundation.min.css')
	$(document).foundation();
```

##Style JSX

Change HTML `class` to `className`
```javascript
	<div className="top-bar">
```

##React life cycle
Mounting: [componentDidMount](https://facebook.github.io/react/docs/component-specs.html#mounting-componentdidmount)
We can call a javascript function inside a component calling it from `componentDidMount`

```javascript
  componentDidMount: function () {
    var modal = new Foundation.Reveal($('#error-modal'));
    modal.open();
  },
``` 

##propTypes and required props
We can force the props that are passed to a component to be always set.

```javascript

  propTypes: {
      title: React.PropTypes.string,
      message: React.PropTypes.string.isRequired
  },
``` 

##Using SCSS and Sass
`npm install sass-loader node-sass --save-dev`

Chage name to `app.scss`

```javascript
	// App css
	require('style!css!sass!applicationStyles') 
```

##Send parameters via url query parameters
Automatically trigger action when the component is mount
Get the query parameter: `var location = this.props.location.query.location;`
Set the route to our application `window.location.hash = '#/';`
```javascript

  componentDidMount: function () {
    var location = this.props.location.query.location;

    if (location && location.length > 0) {
      this.handleSearch(location);
      window.location.hash = '#/';
    }
  },
```  


###Catching changes on props
Called any time the props get updated.

```javascript

	componentWillReceiveProps: function (newProps) {
	    var location = newProps.location.query.location;

	    if (location && location.length > 0) {
	      this.handleSearch(location);
	      window.location.hash = '#/';
	    }
	  },
```

#SCSS Grouping
**app.scss**

```javascript
@import "base/variables";
@import "components/navigation";
```
It is important to prefix the file names with `_`
**_variables.scss**
```javascript

	// Colors
	$grey: #333333;

	// Navigation colors
	$nav-background: $grey;
	$nav-text-color: white;

```

#Testing
Assertions with [expect.js](https://github.com/mjackson/expect)
##Configuring
`npm install karma karma-chrome-launcher karma-mocha karma-mocha-reporter karma-sourcemap-loader karma-webpack mocha expect --save-dev`

* Karma: test runner
* Mocha: test framework


Files that are going to use for testing `files: ['app/tests/**/*.test.jsx'],` 
Preprocessors to build up the test files `  'app/tests/**/*.test.jsx': ['webpack', 'sourcemap']`
Reporters the framework.
Timeout is important to be fast when tests not finish.

**karma.cong.js**
```javascript

	var webpackConfig = require('./webpack.config.js');

	module.exports = function (config) {
	  config.set({
	    browsers: ['Chrome'],
	    singleRun: true,
	    frameworks: ['mocha'],
	    files: ['app/tests/**/*.test.jsx'],
	    preprocessors: {
	      'app/tests/**/*.test.jsx': ['webpack', 'sourcemap']
	    },
	    reporters: ['mocha'],
	    client: {
	      mocha: {
	        timeout: '5000'
	      }
	    },
	    webpack: webpackConfig,
	    webpackServer: {
	      noInfo: true
	    }
	  });
	};

```

**app.test.jsx**
```javascript

	var expect = require('expect');

	describe('App', () => {
	  it('should properly run tests', () => {
	    expect(1).toBe(1);
	  });
	});
```

**package.json**
```javascript
	
	"scripts": {
	    "test": "karma start",
	    "start": "node server.js"
	  },
	  ...
```

##Tests in react
`npm install react-addons-test-utils --save-dev`

```javascript

	var React = require('react');
	var ReactDOM = require('react-dom');
	var expect = require('expect');
	var $ = require('jQuery');
	var TestUtils = require('react-addons-test-utils');

	var Clock = require('Clock');

	describe('Clock', () => {
	  	it('should exist', () => {
	    	expect(Clock).toExist();
	  	});
	  	describe('formatSeconds', () => {
    		it('should format seconds', () => {
	    	  expect(actual).toBe(expected);
    	});
    	...
	});
```
###UI Tests
```javascript
	  
	  describe('render', () => {
	    it('should render clock to output', () => {
	      var clock = TestUtils.renderIntoDocument(<Clock totalSeconds={62}/>);
	      var $el = $(ReactDOM.findDOMNode(clock));
	      var actualText = $el.find('.clock-text').text();

	      expect(actualText).toBe('01:02');
	    });
	  });
```
###Tests spies
Check if a function is called

```javascript

	  it('should call onSetCountdown if valid seconds entered', () => {
	    var spy = expect.createSpy();
	    var countdownForm = TestUtils.renderIntoDocument(<CountdownForm onSetCountdown={spy}/>);
	    var $el = $(ReactDOM.findDOMNode(countdownForm));

	    countdownForm.refs.seconds.value = '109';
	    TestUtils.Simulate.submit($el.find('form')[0]);

	    expect(spy).toHaveBeenCalledWith(109);
	  });
```

###Catch component updates
```javascript

  componentDidUpdate: function (prevProps, prevState) {
    if (this.state.countdownStatus !== prevState.countdownStatus) {
      switch (this.state.countdownStatus) {
        case 'started':
          this.startTimer();
          break;
      }
    }
  },
```
#Functions returning new functions
Section8 - 77. Pausing, Starting, and Resetting

```javascript

	onStatusChange: function (newStatus) {
	    return () => {
	      this.props.onStatusChange(newStatus);
	    }
	  },
	  render: function () {
	    var {countdownStatus} = this.props;
	    var renderStartStopButton = () => {
	    	...
	        return <button className="button secondary" onClick={this.onStatusChange('paused')}>Pause</button>
	      }
	    };
	    ...
```

#More life cycle
`componentWillMount()`

`componentWillUnmount()`

`componentDidMount()`

`componentWillUUpdate()`

`componentWillReceiveProps()`


# Add libraries to Karma
**karma.config.js**
```javascript

    files: [
      'node_modules/jquery/dist/jquery.min.js',
      'node_modules/foundation-sites/dist/foundation.min.js',
      'app/tests/**/*.test.jsx'
    ],
```

##Add Foundation to SASS loader

Section 8 Lecture 83
**webpack.config.js**
```javascript

	var path = require('path');

  sassLoader: {
    includePaths: [
      path.resolve(__dirname, './node_modules/foundation-sites/scss')
    ]
  },
```  

**app.scss**

```javascript

	// foundation
	@import "base/foundation-settings";
	@import "foundation";
	@include foundation-everything;
	...

```

**_foundation-settings**
Copy it from foundation

# SECTION 9 TODO

##Add components to webpack Automatically

```javascript
resolve: {
    
    modulesDirectories: [
      'node_modules',
      './app/components'
    ],
    ...
  },
```


##Spread operator      
Useful to call functions with parameters that come from an array.
```javascript

	var person = ['Andrew', 25];
	var personTwo = ['Jen', 29];

	function greet (name, age) {
  		console.log('Hi ' + name + ', you are ' + age);
	}
	greet(...person);
	greet(...personTwo);
```	

To remove the array inside: `[3,[1,2]] => [3,1,2]`
```javascript

	var groupA = ['Jen', 'Cory'];
	var groupB = ['Vikram'];
	var final = [...groupB, 3, ...groupA];
	console.log(final);
```



##Send values as prop objects to a component without declaring all of them

`key={todo.id}` creates an id for each object. It is needed so react knows that every item is different.
`{...todo}` **spread operator** spread all the properties of an object, (in this case) into individual props[...](http://odetocode.com/blogs/scott/archive/2014/09/02/features-of-es6-part-5-the-spread.aspx)

```javascript

	todos.map((todo) => {
		return (
			<Todo key={todo.id} {...todo}/>
		);
	}
```  

##Test how many elements of a component are inside another component
Return the `Todo` component in the `todoList`    
`var todosComponents = TestUtils.scryRenderedComponentsWithType(todoList, Todo);`

##onChange
`onChange` instead of onClick or onSubmit it is fired any time the `<input>` is changed

#REDUX
**Use Pure Functions**

* Same output for the same input
* No side effects. Don't change nothing
* Synchronous 

## Store and Reducer
The reducer has a state and an actions as parameters. 
We can set a default paramater input if it is empty. 

```javascript

	var stateDefault = {
	  searchText: '',
	  showCompleted: false,
	  todos: []
	};
	//var reducer = function(state, action) {
	//   if (state=undefined)	
	//		state = stateDefault;
	//   return state;
	//};
	var reducer = (state = stateDefault, action) => {
	  return state;
	};

	var store = redux.createStore(reducer);
```

## Dispatch & Handling Actions
Actions are objects
They must have a parameter `type` with the name of the action
**Action**
```javascript
	
	var action = {
		type: 'CHANGE_NAME'
		name: 'Hugo'
	}
```
**Dispatch**
```javascript

	store.dispatch(action)
```
**Reducer**
```javascript

	var reducer = (state = {name: 'Anonymous'}, action) => {
	  switch (action.type) {
	    case 'CHANGE_NAME':
	      return {
	        ...state,
	        name: action.name
	      };
	    default:
	      return state;
	  }
	};
```
##Subscribing To Changes & Debugging
Any time the store state changes the subscriber will run.
```javascript
	
	store.subscribe(() => {
  		var state = store.getState();
  		console.log(state);
	});
```

**Unsubscribe**
`subscribe` returns and object that when called it unsubscribes.
```javascript

	// Subscribe to changes
	var unsubscribe = store.subscribe(() => {
	  var state = store.getState();

	  console.log('Name is', state.name);
	  document.getElementById('app').innerHTML = state.name;
	});
	unsubscribe();
```

##Extension **Redux DevTools**
Add this to the store to use the extension
```javascript
	
	var store = redux.createStore(reducer, redux.compose(
  		window.devToolsExtension ? window.devToolsExtension() : f => f
	));
```

##Combine Reducers
A way to separate code from the reducer.
```javascript

	var nameReducer = (state = 'Anonymous', action) => {
	  switch (action.type) {
	    case 'CHANGE_NAME':
	      return action.name;
	    default:
	      return state;
	  };
	};

	var hobbiesReducer = (state = [], action) => {
	 ...
	};


	var reducer = redux.combineReducers({
	  name: nameReducer,
	  hobbies: hobbiesReducer,
	});

	var store = redux.createStore(reducer);
```

##Action Generators

Simple way to create our action objects.
```javascript

	var changeName = (name) => {
	  return {
	    type: 'CHANGE_NAME',
	    name // Same as  <name: name>
	  }
	};

	store.dispatch(changeName('Hugo'));
```

##Asynchronous Actions
First create the `reducer`
```javascript

	var mapReducer = (state = {isFetching: false, url: undefined}, action) => {
	  switch (action.type) {
	    case 'START_LOCATION_FETCH':
	      return {
	        isFetching: true,
	        url: undefined
	      };
	    case 'COMPLETE_LOCATION_FETCH':
	      return {
	        isFetching: false,
	        url: action.url
	      };
	    default:
	      return state;
	  }
	};
```

Then the actions
```javascript

	var startLocationFetch = () => {
	  return {
	    type: 'START_LOCATION_FETCH'
	  };
	};

	var completeLocationFetch = (url) => {
	  return {
	    type: 'COMPLETE_LOCATION_FETCH',
	    url
	  };
	};
```
Finally the function that will be in charge of the asynchrony 
```javascript

	var fetchLocation = () => {
	  store.dispatch(startLocationFetch());

	  axios.get('http://ipinfo.io').then(function (res) {
	    var loc = res.data.loc;
	    var baseUrl = 'http://maps.google.com?q='

	    store.dispatch(completeLocationFetch(baseUrl + loc));
	  });
	};
```

##Organize Reducers
Separate actions, reducers and store in different folders in files called **index.jsx**   
We can export each object like

```javascript
	
	export var changeName = (name) => {
	  return {
	    type: 'CHANGE_NAME',
	    name // Same as  <name: name>
	  }
	};
```


Then if we need to access the store from inside actions 
```javascript

	var fetchLocation = () => {
	  store.dispatch(startLocationFetch());
	  ...

```

 we need to add a new library  `npm install redux-thunk save-dev`

and use it as a middleware in  **configStore.jsx** `redux.applyMiddleware(thunk),`

```javascript

	var thunk = require('redux-thunk').default;

	  var store = redux.createStore(reducer, redux.compose(
	    redux.applyMiddleware(thunk),
	    ...
	  ));

	  return store;
	}

```

Change the way we use the `store` it in the `action`

```javascript

	export var fetchLocation = () => {
	  return (dispatch, getState) => {
	    dispatch(startLocationFetch());
	    	...
	  };
	};
```

And the way we call the `action`
`store.dispatch(actions.fetchLocation());`

## Testing Reducers
Deep Freeze will throw an error if a variable is changed.
`npm install deep-freeze-stric --save-dev`

```javascript
	var df = require('deep-freeze-strict');


	describe('Reducers', () => {
	  describe('searchTextReducer', () => {
	      var res = reducers.searchTextReducer(df(''), df(action));
	    });
	  });
```

## Connect React Component with Redux
`npm install save--dev react-redux`

The `Provider` is used to provide a store to its children.

Every component inside the `Provider` (and it children) will have access to the store.

**app.jsx**

```javascript
	
	var {Provider} = require('react-redux');

	ReactDOM.render(
	  <Provider store={store}>
	    <TodoApp/>
	  </Provider>,
	  document.getElementById('app')
	);

```
###Connect
`Connect` is the companion of the `Provider` component   

`var {connect} = require('react-redux');`

`connect` is called after the components are created.

Instead of `exports` the react component, we connect the component to the provider `connect()(TodoList)` . The component can now request data.
We pass to `connect`  a function that have the `state` as an only argument `(state) => {}` and returns the object that we need to pass to our component.`todos: state.todos`


```javascript

	module.exports = connect(
	  (state) => {
	    return {
	      todos: state.todos
	    };
	  }
	)(TodoList);
```

####Allow dispatch in components
`connect` already allow us to use `dispatch`.

```javascript
	
	var {id, text, completed, createdAt, completedAt, dispatch} = this.props;

	var Todo = React.createClass({
		...
		dispatch(actions.toggleTodo(id));
	})
	module.exports = connect()(Todo)
```
##Test React components with Redux
Because we change the `exports` in the components we need to make some changes.   

Directly `export` the components.   
`export var Todo = React.createClass({`

Use `export default` instead of  `module.export` so what we get from making a `require` will be it. If we want the component (`Todo`) we will call it differently .
`export default connect()(Todo);`

Because we are now using `export default` we need to get the modules differently.

`import TodoList from 'TodoList'` instead of `require` 

```javascript