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
		<div>
			<p className='f3'>
				{'This Magic Brain will detect faces in your pictures. Git it and try. '}
			</p>
			<div className='center'>
				<div className='form center pa4 br3 shadow-5'>
					<input className='f4 pa-2 w-70 center' type='tex' />
					<button className='w-30 grow f4 link ph3 pv2 dib what bg-light-purple'>Detect</button>
				</div>
			</div>
		</div>
		);


}
export default ImageLinkForm;
```
 To get everything all components centered - create in app.css: 

```
.center {
  display: flex;
  justify-content:center;

}
```

Create ImageLinkForm .css taking pattern from https://leaverou.github.io/css3patterns/#blueprint-grid :
```
.form {
	width: 700px;
	background-color:#269;
	background-image: linear-gradient(white 2px, transparent 2px),
	linear-gradient(90deg, white 2px, transparent 2px),
	linear-gradient(rgba(255,255,255,.3) 1px, transparent 1px),
	linear-gradient(90deg, rgba(255,255,255,.3) 1px, transparent 1px);
	background-size: 100px 100px, 100px 100px, 20px 20px, 20px 20px;
	background-position:-2px -2px, -2px -2px, -1px -1px, -1px -1px;
}
```
Then import it in ImageLinkForm.js:

```
import './ImageLinkForm.css';
```

Then in index.css: 
```

button {
	cursor: pointer;
}
```
This adds cursor when hover over the button. 


Then add rank component to App.js 
```
import Rank from './Components/Rank/Rank'; 

<Rank />
```
Also create Rank Folder in Components then add Rank.js. 

Then add following to Rank.js: 

```
import React from 'react';


const Rank = (Component) => {
	return (
		<div>
		
			<div className='white f3'>
				{'Rob, your current rank is....'}
			</div>

			<div className='white f1'>
				{'#5'}
			</div>


		</div>
		);


}
export default Rank;
```

Change font family in index.css: 

```
body {
  margin: 0;
  font-family: "Courier New", Courier, monospace;
 ```
  
  Add particles API: 
  
  ```
   npm install react-particles-js 
   
  
  ```
  Paste example from npm page https://www.npmjs.com/package/react-particles-js to App.js:
  
  ```
  function App() {
  return (
    <div className="App">
     <Particles 
              params={{
                particles: {
                  line_linked: {
                    shadow: {
                      enable: true,
                      color: "#3CA9D1",
                      blur: 5
                    }
                  }
                }
              }}
              style={{
                width: '100%',
                backgroundImage: `url(${logo})` 
              }}
      />
     <Navigation />
     <Logo />
      <Rank />
     <ImageLinkForm />
     
    { 
      // 
     // 
     // <FaceRecognition />
   }
    </div>
  );
}

```
Then clear out parameters and add a constant:
```
import Particles from 'react-particles-js';

const particlesOptions = {
  particles: {
    line_linked: {
      shadow: {
        enable: true,
        color: "#3CA9D1",
        blur: 5
      }
    }
  }
}
  
function App() {
  return (
    <div className="App">
     <Particles 
     className='particles'
     params={particlesOptions}
      />
     <Navigation />
     <Logo />
      <Rank />
     <ImageLinkForm />
     
    { 
      // 
     // 
     // <FaceRecognition />
   }
    </div>
  );
}
```
This will overwrite page and requires changes in css. When using fixed position can apply z-index, this tells you what layer you want image to be on: 
```
.particles {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index -1
}
```

Edit const particlesOptions again: 

```
const particlesOptions = {
  particles: {
    number: {
      value: 300,
      density: {
        enable: true,
        value_area: 800
      }
    }
  }
 
 }  
 ```
