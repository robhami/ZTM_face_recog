
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

Then add to ImageLinkForm elementin App.js: 
```
onButtonSubmit={this.onButtonSubmit}
```

Add to ImageLinkForm.js: 
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
