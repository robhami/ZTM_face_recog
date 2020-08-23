## Sign in Form ##

Create SignIn folder in src and SignIn.js file inside. Get signIn form from tachyons website and paste into react component code. Need to close input tags:

```javascript
import React from 'react';


const SignIn = () => {
	return (
		<main class="pa4 black-80">
		<form class="measure center">
		<fieldset id="sign_up" class="ba b--transparent ph0 mh0">
		<legend class="f4 fw6 ph0 mh0">Sign In</legend>
		<div class="mt3">
		<label class="db fw6 lh-copy f6" for="email-address">Email</label>
		<input class="pa2 input-reset ba bg-transparent hover-bg-black hover-white w-100" type="email" name="email-address"  id="email-address"/>
		</div>
		<div class="mv3">
		<label class="db fw6 lh-copy f6" for="password">Password</label>
		<input class="b pa2 input-reset ba bg-transparent hover-bg-black hover-white w-100" type="password" name="password"  id="password"/>
		</div>
		<label class="pa0 ma0 lh-copy f6 pointer"><input type="checkbox"/> Remember me</label>
		</fieldset>
		<div class="">
		<input class="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" type="submit" value="Sign in"/>
		</div>
		<div class="lh-copy mt3">
		<a href="#0" class="f6 link dim black db">Sign up</a>
		<a href="#0" class="f6 link dim black db">Forgot your password?</a>
		</div>
		</form>
		</main>
		);


}

export default SignIn;
```

In App.js import SignIn.js.
```
import SignIn from './Components/SignIn/SignIn'; 
```
Then add SignIn element to App.js:
```
 render () {
    return (
      <div className="App">
       <Particles 
       className='particles'
        params={particlesOptions}
        />
       <Navigation />
       <SignIn />
       <Logo />
        <Rank />
       <ImageLinkForm 
        onInputChange={this.onInputChange} 
        onButtonSubmit={this.onButtonSubmit}/>
       
       <FaceRecognition box={this.state.box} imageUrl={this.state.imageUrl}/>
  
      </div>
    );
  }
}
```
Tidy up code: 
```
const SignIn = () => {
	return (
	<article className="br3 ba b--black-10 mv4 w-100 w-50-m w-25-l mw6 shadow-5 center">
		<main className="pa4 black-80">
		<form className="measure">
		<fieldset id="sign_up" className="ba b--transparent ph0 mh0">
		<legend className="f1 fw6 ph0 mh0">Sign In</legend>
		<div className="mt3">
		<label className="db fw6 lh-copy f6" for="email-address">Email</label>
		<input className="pa2 input-reset ba bg-transparent hover-bg-black hover-white w-100" type="email" name="email-address"  id="email-address"/>
		</div>
		<div className="mv3">
		<label className="db fw6 lh-copy f6" for="password">Password</label>
		<input className="b pa2 input-reset ba bg-transparent hover-bg-black hover-white w-100" type="password" name="password"  id="password"/>
		</div>
		
		</fieldset>
		<div className="">
		<input className="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" type="submit" value="Sign in"/>
		</div>
		<div className="lh-copy mt3">
		<a href="#0" className="f6 link dim black db">Register</a>
	
		</div>
		</form>
		</main>
	</article>
		);


}

export default SignIn;
```
Create route state: 
```
class App extends Component {
  constructor() {
    super();
    this.state = {
      input: '',
      imageUrl: '',
      box: {},
      route: 'signin'
    }
  };
```
Create conditional that shows sign in if route = signin: 
```
render () {
    return (
      <div className="App">
       <Particles 
       className='particles'
        params={particlesOptions}
        />
       <Navigation />
       {this.state.route === 'signin' ?

       <SignIn />
       :
         <div>
         <Logo />
          <Rank />
         <ImageLinkForm 
          onInputChange={this.onInputChange} 
          onButtonSubmit={this.onButtonSubmit}/>
         
         <FaceRecognition box={this.state.box} imageUrl={this.state.imageUrl}/>
         </div>
      }

      </div>
    );
  }
}
```

Then add  function call/prop to SignIn element: 

```
<SignIn onRouteChange={this.onRouteChange}/>
```
and create function for it: 
```
onInputChange = (event) => {
      this.setState({input: event.target.value});
  }
```
Then in SignIn component, add onclick to signin button to receive onRouteChange event handler:
```
<input 
		onClick={onRouteChange}
		className="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" 
		type="submit" 
		value="Sign in"/>
```
signin button to receive onRouteChange event handler:
```
const SignIn = ({onRouteChange}) => {
```
This will remove signin when signin button clicked.

Can pass onRouteChange into Navigation component as a prop and add onClick to p element that calls onRouteChange: 

```
const Navigation = ({onRouteChange}) => {
	return (
		<nav style={{display: 'flex', justifyContent: 'flex-end'}}>
			<p onClick={onRouteChange} className='f3 link dim black underline pa3 pointer'>Sign Out </p>
		</nav>

		);


}
```
And add to element in App.js

```
 <Navigation onRouteChange={this.onRouteChange}/>
 ```
 Then change function to dynamically change route: 
 ```
 onRouteChange = (route) => {
    this.setState({route: route});
  }
```
Then change signin.js, need to put arrow function in so it runs when clicked on not when rendered: 
```
<input 
	onClick={() => onRouteChange('home')}
	className="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" 
	type="submit" 
	value="Sign in"/>

```
Do same in Navigation.js:
```
<p onClick={()=> onRouteChange('signin')} className='f3 link dim black underline pa3 pointer'>Sign Out </p>

```
Now signin screen shows when click sign out.

### Register ###

Create Register folder with REgister.js file inside, add following text to .js file: 

```
import React from 'react';


const Register = ({onRouteChange}) => {
	return (
		<article className="br3 ba b--black-10 mv4 w-100 w-50-m w-25-l mw6 shadow-5 center">
		<main className="pa4 black-80">
		<form className="measure">
		<fieldset id="sign_up" className="ba b--transparent ph0 mh0">
			<legend className="f1 fw6 ph0 mh0">Sign In</legend>
			<div className="mt3">
				<label className="db fw6 lh-copy f6" for="name">Name</label>
				<input className="pa2 input-reset ba bg-transparent hover-bg-black hover-white w-100" type="name" name="name"  id="name"/>
			</div>
			<div className="mt3">
				<label className="db fw6 lh-copy f6" for="email-address">Email</label>
				<input className="pa2 input-reset ba bg-transparent hover-bg-black hover-white w-100" type="email" name="email-address"  id="email-address"/>
			</div>
			<div className="mv3">
				<label className="db fw6 lh-copy f6" for="password">Password</label>
				<input className="b pa2 input-reset ba bg-transparent hover-bg-black hover-white w-100" type="password" name="password"  id="password"/>
			</div>
		</fieldset>
		<div className="">
			<input 
			onClick={() => onRouteChange('home')}
			className="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" 
			type="submit" 
			value="Sign in"/>
		</div>
		
		</form>
		</main>
		</article>
		);


}

export default SignIn;
```
in signin change register element to have onclick function: 
```
<div className="lh-copy mt3">
			<p onClick={() => onRouteChange('register')} className="f6 link dim black db">Register</p>

		</div>
```
Then go to App.js and add conditional to give register:  
```
  render () {
    return (
      <div className="App">
       <Particles 
       className='particles'
        params={particlesOptions}
        />
       <Navigation onRouteChange={this.onRouteChange}/>
       {this.state.route === 'home' 
        ? <div>
            <Logo />
            <Rank />
            <ImageLinkForm 
            onInputChange={this.onInputChange} 
            onButtonSubmit={this.onButtonSubmit}/>

            <FaceRecognition box={this.state.box} imageUrl={this.state.imageUrl}/>
           </div>
           : (
              this.state.route === 'signin' 
              ? <SignIn onRouteChange={this.onRouteChange}/>
              : <Register onRouteChange={this.onRouteChange}/>
            )       
        }
      </div>
    );
  }
```
Also import register: 
```
import Register from './Components/Register/Register'; 
```

Change value to Sign In on SignIn.js:
```
<div className="">
			<input 
			onClick={() => onRouteChange('home')}
			className="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" 
			type="submit" 
			value="Sign in"/>
		</div>
```
Add ;pointer to register so pointer shows on hover: 
```
<p onClick={() => onRouteChange('register')} className="f6 link dim black db pointer">Register</p>
```

Change Navigation. js to show register and sign in/out, then put condtional to change what shows depending on state. 
```
import React from 'react';

const Navigation = ({onRouteChange, isSignedIn}) => {
	

	if(isSignedIn) {
		return (
			<nav style={{display: 'flex', justifyContent: 'flex-end'}}>
				<p onClick={()=> onRouteChange('signout')} className='f3 link dim black underline pa3 pointer'>Sign Out </p>
			</nav>
			);
			} else {
				return (
					<nav style={{display: 'flex', justifyContent: 'flex-end'}}>
						<p onClick={()=> onRouteChange('signin')} className='f3 link dim black underline pa3 pointer'>Sign Out </p>
						<p onClick={()=> onRouteChange('register')} className='f3 link dim black underline pa3 pointer'>Register </p>
					</nav>
				);
			}
}

export default Navigation;
```
Change onRouteChange function in App.js:
```
onRouteChange = (route) => {
    if(route === 'signout') {
      this.setState({isSignedIn: false})
    } else if (route === 'home') {
      this.setState({isSignedIn: true})
    }
      this.setState({route: route});
  }
  ```
  Also isSignedIn state:
  ```
  class App extends Component {
  constructor() {
    super();
    this.state = {
      input: '',
      imageUrl: '',
      box: {},
      route: 'signin',
      isSignedIn: false
    }
  };
  
  
  ```
  Then change Navigation Element on App.js: 
  ```
 <Navigation isSignedIn={this.state.isSignedIn} onRouteChange={this.onRouteChange}/>
 ```
   Tidy up: 
   
   Remove console.log(box)
   
   Use destructuring to reduce this.state usage. Allows removal of this.state from all things listed in destructuring:
   
   ```
    render () {
    const {isSignedIn, imageUrl, route, box} = this.state;
    return (
      <div className="App">
       <Particles 
       className='particles'
        params={particlesOptions}
        />
       <Navigation isSignedIn={isSignedIn} onRouteChange={this.onRouteChange}/>
       {this.state.route === 'home' 
        ? <div>
            <Logo />
            <Rank />
            <ImageLinkForm 
            onInputChange={this.onInputChange} 
            onButtonSubmit={this.onButtonSubmit}/>

            <FaceRecognition box={box} imageUrl={imageUrl}/>
           </div>
           : (
              route === 'signin' 
              ? <SignIn onRouteChange={this.onRouteChange}/>
              : <Register onRouteChange={this.onRouteChange}/>
            )       
        }
      </div>
    );
  }
```
Fix console.log error message saying:
```
index.js:1 Warning: Invalid DOM property `for`. Did you mean `htmlFor`?
```
As can't use for= in JSX so change all these to htmlFor in SignIn.js and Register.js. 


Need to change form element to div because it is automatically submitting due to onSubmit event with type=submit. 
