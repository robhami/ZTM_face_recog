## Face Recog 1 ##

Create React App

Remove logo file.
Remove import logo from App.js.

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
 Add Navigation folder on Components folderAdd Navigation.js file inside Navigation folder
 Install Tachyons:
```
npm tachyons

npm install tachyons
```

In index.js: 

```
import 'tachyons';

```
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

Add to index.css body tag: 

```
background:linear-gradient(89deg, #FF5EDF 0%, #84C8DE 100%);
```

Create Logo folder in src and add logo.js file to it.
Add Logo tag to App.js  and import logo file: 

``
import React from 'react';
import './App.css';
import Navigation from './Components/Navigation/Navigation'; 
import Logo from './Components/Logo/Logo'; 
function App() {
  return (
    <div className="App">
     <Navigation />
    
     <Logo />

    { 
     
     // <ImageLinkForn />
     // <FaceRecognition />
   }
    </div>
  );
}

export default App;
```

Install library:
```
npm install --save react-tilt
```

Add to logo.js: 

```

import React from 'react';

const Logo = (Component) => {
	return (
		<div className='ma4 mt8'>

		);


}

export default Navigation;
