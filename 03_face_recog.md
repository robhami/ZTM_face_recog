
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
