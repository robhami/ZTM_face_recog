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

Add Navigation folder on Components folder

Add Navigation.js file inside Navigation folder
 
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

Add Logo tag to App.js and import logo file: 

```
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
import Tilt from 'react-tilt';
 

const Logo = (Component) => {
	return (
		<div className='ma4 mt8'>
			<Tilt className="Tilt br2 shadow-2" options={{ max : 55 }} style={{ height: 150, width: 150 }} >
	 		<div className="Tilt-inner"> 👽 </div>
			</Tilt>
		</div>
		);


}

export default Logo;

```

Create logo.css and add:
```
.Tilt {
	background:linear-gradient(89deg, #FF5EDF 0%, #84C8DE 100%);
}
```
Then import to Logo.js by adding: 
```
import './Logo.css'; 
```

Download brain logo then put in logo folder and import to Logo.js:

```
import brain from './brain.png'
```
Also edit logo component: 
```
const Logo = (Component) => {
	return (
		<div className='ma4 mt8'>
			<Tilt className="Tilt br2 shadow-2" options={{ max : 55 }} style={{ height: 150, width: 150 }} >
		 		<div className="Tilt-inner pa3"> 
		 			<img style={{paddingTop: '25px'}} alt='logo'  src={brain}/>
		 		</div>
			</Tilt>
		</div>
		);


}
```
Create imageLinkForm folder and file in src. 

Import to App.js and add element to app component:
```
import ImageLinkForm from './Components/ImageLinkForm/ImageLinkForm'; 


function App() {
  return (
    <div className="App">
     <Navigation />
    
     <Logo />
     <ImageLinkForm />
    { 
     
     // 
     // <FaceRecognition />
   }
    </div>
  );
}

export default App;

```
Then add to ImageLinkForm.js:

```
import React from 'react';


const ImageLinkForm = (Component) => {
	return (
		<div className='ma4 mt8'>
			
		
		</div>
		);


}
export default ImageLinkForm;
```
