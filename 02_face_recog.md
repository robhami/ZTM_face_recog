
Need to create state to deal with any input (i.e. our apps knows what the user entered value is, remembers it, and updates it any time in changes). 
This is done by adding a constructor.

The input will have arrow function- onInputChange. This is an eventlistener so will receive an event and do something with it.  :

```
function App() {
  constructor() {
    super();
    this.state = {
      input: '',
    }
  }

  onInputChange = (event) => {
      console.log(event);

  }
```

Also need to pass event as a prop to ImageLinkForm:

```
 <ImageLinkForm onInputChange={onInputChange}/>
```

