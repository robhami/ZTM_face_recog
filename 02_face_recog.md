
Need to create state to deal with any input (i.e. our apps knows what the user entered value is, remembers it, and updates it any time in changes). 
This is done by adding a constructor.
Also seems like you have to change function App to a class and put render around return. 
The input will have arrow function- onInputChange. This is an eventlistener so will receive an event and do something with it.  :

```
import React, {Component} from 'react';

class App() extends Component {
  constructor() {
    super();
    this.state = {
      input: '',
    }
  }

  onInputChange = (event) => {
      console.log(event);

  }
  
   render () {
    return (
      <div className="App">
       <Particles 
       className='particles'
        params={particlesOptions}
        />
       <Navigation />
       <Logo />
        <Rank />
       <ImageLinkForm onInputChange={this.onInputChange}/>
       
      { 
        // 
       // 
       // <FaceRecognition />
     }
      </div>
    );
  }
```

Also need to pass event as a prop to ImageLinkForm:

```
 <ImageLinkForm onInputChange={onInputChange}/>
```

In ImageLinkForm.js can destructure onInputChange and add an onChange event to input element:

```
const ImageLinkForm = ({onInputChange}) => {
	return (
		<div>
			<p className='f3'>
				{'This Magic Brain will detect faces in your pictures. Git it and try. '}
			</p>
			<div className='center'>
				<div className='form center pa4 br3 shadow-5'>
					<input className='f4 pa-2 w-70 center' type='tex' onChange={onInputChange}/>
					<button className='w-30 grow f4 link ph3 pv2 dib what bg-light-purple'>Detect</button>
				</div>
			</div>
		</div>
		);
```

Change console.log to get what is input into input element:

```
 onInputChange = (event) => {
      console.log(event.target.value);

  }
```
Add function to deal with button being clicked:
```
 onButtonSubmit = () => {
    console.log('click');
  }
```

Also need to pass event as a prop to ImageLinkForm from/in App.js: 
```
onButtonSubmit={this.onButtonSubmit}
```

In ImageLinkForm.js can destructure onButtonSubmit and add an onButtonSubmit event to button element: 
```
const ImageLinkForm = ({onInputChange, onButtonSubmit}) => {
	return (
		<div>
			<p className='f3'>
				{'This Magic Brain will detect faces in your pictures. Git it and try. '}
			</p>
			<div className='center'>
				<div className='form center pa4 br3 shadow-5'>
					<input className='f4 pa-2 w-70 center' type='tex' onChange={onInputChange}/>
					<button className='w-30 grow f4 link ph3 pv2 dib what bg-light-purple'
					onClick={onButtonSubmit}
					>Detect</button>
				</div>
			</div>
		</div>
		);


}
```

Sign up for Clarifai API at: https://www.clarifai.com/model-gallery

Run NPM install:
```
npm install clarifai
```
Take code from site and add to button submit function: 
```
 onButtonSubmit = () => {
    console.log('click');
    app.models.predict("a403429f2ddf4b49b307e318f00e528b", "https://samples.clarifai.com/face-det.jpg").then(
      function(response) {
        // do something with response
      },
      function(err) {
        // there was an error
      }
    );
  }
```
Use import code and API key code: 

```
const Clarifai = require('clarifai');

const app = new Clarifai.App({
 apiKey: "825fc9edc4d84b5a8af93639ba0cc3b4"
});
```
Can also use React import method instead of "const Clarifai = require('clarifai');".

Create FaceRecognition folder and .js file in Components folder. Then import into App.js: 
```
import FaceRecognition from './Components/FaceRecognition/FaceRecognition'; 
```
Then add FaceRecognition component to App.js:
```
 render () {
    return (
      <div className="App">
       <Particles 
       className='particles'
        params={particlesOptions}
        />
       <Navigation />
       <Logo />
        <Rank />
       <ImageLinkForm 
        onInputChange={this.onInputChange} 
        onButtonSubmit={this.onButtonSubmit}/>
       
       <FaceRecognition />
  
      </div>
    );
  }
}
```
Then add following to FaceRecognition.js, this just adds image at bottom of page : 
```
import React from 'react';

const FaceRecognition = (Component) => {
	return (
		<div className='center'>
			<img alt='' src={'https://samples.clarifai.com/face-det.jpg'} />
		</div>
		);


}

export default FaceRecognition;
```
Add to App.js below code. This adds imageUrl prop to state, uses Clarifai colour model, then console.log response from the model
: 
```

  class App extends Component {
  constructor() {
    super();
    this.state = {
      input: '',
      imageUrl: ''
    }
  };

  onInputChange = (event) => {
      console.log(event.target.value);

  }

  onButtonSubmit = () => {
    this.SetState({imageUrl: input});
    
    console.log('click');
    app.models.predict(
      Clarifai.COLOR_MODEL,
      "https://samples.clarifai.com/face-det.jpg")
    .then(
      function(response) {
        console.log(response);
      },
      function(err) {
        // there was an error
      }
    );
  }
```
