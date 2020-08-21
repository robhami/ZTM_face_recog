
Bounding box co-ordinates are percentages (e.g. top row is 18.7% of the image). 

```
{top_row: 0.18799154, left_col: 0.34647143, bottom_row: 0.6301852, right_col: 0.6681788}
```

Add state to App.js for box and create function to calculate face location: 

```
class App extends Component {
  constructor() {
    super();
    this.state = {
      input: '',
      imageUrl: '',
      box: {}
    }
  };


calculateFaceLocation = (data) => {


}

```

Then send Clarifai response data to function in App.js: 
```
function(response) {
        this.calculateFaceLocation(response);
        // console.log(response.outputs[0].data.regions[0].region_info.bounding_box);
      },
      
```
Tidy up code using arrow function in App.js onButtonSubmit function:
```
onButtonSubmit = () => {
    this.setState({imageUrl: this.state.input});
    console.log('click');
    app.models.predict(
      Clarifai.FACE_DETECT_MODEL,
      this.state.input)
    .then(response =>this.calculateFaceLocation(response))
    .catch(error => console.log(err));
  }
```
Move response to function response- add data. infront instead of response as function parameter is data. Also call image from FaceRecognition.js and extract height and width:

```
calculateFaceLocation = (data) => {
 
  const clarfaiface= data.outputs[0].data.regions[0].region_info.bounding_box;
  const image = document.getElementById('inputimage');
  const width =Number(image.width);
  const height =Number(image.height);
  console.log(width,height);
}

```
Add id to image in FaceRecognition.js that can be called in app.js above:

```
const FaceRecognition = ({imageUrl}) => {
	return (
		<div className='center ma'>
			<div className='absolute mt2'>
				<img id='inputimage' alt='' src={imageUrl} width='500px' height='auto' />
			</div>
		</div>
		);
}
```
Need to return object with 4 corners for the box. 

```

calculateFaceLocation = (data) => {
 
  const clarifaiFace= data.outputs[0].data.regions[0].region_info.bounding_box;
  const image = document.getElementById('inputimage');
  const width =Number(image.width);
  const height =Number(image.height);
  console.log(width,height);
  return {
    leftCol: clarifaiFace.left_col * width,
    topRow: clarifaiFace.top_row * height,
    rightCol: width - (clarifaiFace.right_col * width),
    bottomRow: height -(clarifaiFace.bottom_row * height)
  }
}

```
Create another function to use values to create box: 
```
displayFaceBox = (box) => {
  console.log(box);
  this.setState({box: box});

}
```
Then call displayFaceBox in onButtonSubmit function to take data from calculateFaceLocation by wrapping it as displayFaceBox's input: 

```
onButtonSubmit = () => {
    this.setState({imageUrl: this.state.input});
    console.log('click');
    app.models.predict(
      Clarifai.FACE_DETECT_MODEL,
      this.state.input)
    .then(response =>this.displayFaceBox(this.calculateFaceLocation(response)))
    .catch(err => console.log(err));
  }
```
Add box to FaceRecognition element in App.js: 
```
<FaceRecognition box={this.state box} imageUrl={this.state.imageUrl}/>
```
Add box to FaceREcognition variable in FaceRecognition.js. Also create new div and give className- 'bounding-box.
```
import React from 'react';

const FaceRecognition = ({imageUrl, box}) => {
	return (
		<div className='center ma'>
			<div className='absolute mt2'>
				<img id='inputimage' alt='' src={imageUrl} width='500px' height='auto' />
				<div className='bounding-box'></div>
			</div>
		</div>
		);


}

export default FaceRecognition;
```
Create new file in FaceRecogition folder called FaceRecognition.css. Import it to FaceRecognition.js:
```
import './FaceRecognition.css';
```
Copy css from Clarifai website:
```
.bounding-box {
    position: absolute;
    box-shadow: 0 0 0 3px #149df2 inset;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    -ms-flex-pack: center;
    justify-content: center;
    cursor: pointer;
	
}
```
Then add style to bounding box div in Facerecognition.js: 
```
	<div className='bounding-box' 
				style={{top: box.topRow, right: box.rightCol, bottom: box.bottomRow, left: box.leftCol}}></div>
```
