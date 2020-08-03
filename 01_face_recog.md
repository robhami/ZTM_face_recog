## Face Recog 1 ##

Create React App

REmove logo file
Remove import logo from App.js

Delete React stuff from App.js, to leave:

```
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
     
    </div>
  );
}

export default App;
        
 ```
 ### Navigation ###
 
 Add Components folder in src folder
 Add Navigaction folder on Components folderAdd Navigation.js file inside Navigation folder
 
 Add following code to Navigation.js: 
 
 ```
 import React from 'react';

const Navigation = (Component) => {
	return (
		<nav style={{display: 'flex', justifyContent: 'flex-end'}}>
			<p className='f3 link dim black underline pa3 pointer'>Sign Out </p>
		</nav>

		);


}

export default Navigation;

```

Import Navigation.js to App.js: 

```
import Navigation from './Components/Navigation/Navigation'; 
```
Install Tachyons:
```
npm tachyons

npm install tachyons
```

In index.js: 

```
import 'tachyons';
