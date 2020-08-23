## Sign in Form ##

Create SignIn folder in src and SignIn.js file inside. Get signIn form from tachyons website and paste into react component code. Need to close input tags as this is needed in JSX but not in html:

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
```javascript
import SignIn from './Components/SignIn/SignIn'; 
```
Then add SignIn element to App.js:
```javascript
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
Tidy up code, add article tag around signin code to give a card effect. Also remove forgot password, remember me. Change all class tags to className. Remove centre from form as article is centred.  Change SignUp text to Register.
```javascript
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

### Create Route State ###

Create route state in App.js to keep track of where we are on page. In our case we want to start at signin when app loads: 

```javascript
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

### Create Conditional in App.js for sign in state ###
Create conditional that shows sign in if route = signin. Can't do if statement because returning the elements. But because this is JSX we can wrap things in curly brackets and do a ternary conditional. If route = signin state return signIn component else load app page (e.g. search bar etc). Need to wrap multiple elements from App main page in div

```javascript
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

### onRouteChange function ###

Then add  function call/prop to SignIn element: 

```javascript
<SignIn onRouteChange={this.onRouteChange}/>
```
and create function for it: 
```javascript
onRouteChange = () => {
	this.setState({route: 'home'});
}
```
Then in SignIn component, add onclick to signin button to receive onRouteChange event handler:
```javascript
<input 
		onClick={onRouteChange}
		className="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" 
		type="submit" 
		value="Sign in"/>
```
Signin component to receive onRouteChange event handler:
```javascript
const SignIn = ({onRouteChange}) => {
```
This will remove signin when signin button clicked.


### SignOut ####
Want to sign out when click on that and go to sign in page. 

Can pass onRouteChange into Navigation component as a prop and add onClick to p element that calls onRouteChange: 

```javascript
const Navigation = ({onRouteChange}) => {
	return (
		<nav style={{display: 'flex', justifyContent: 'flex-end'}}>
			<p onClick={onRouteChange} className='f3 link dim black underline pa3 pointer'>Sign Out </p>
		</nav>

		);


}
```
And add to element in App.js

```javascript
 <Navigation onRouteChange={this.onRouteChange}/>
 ```
 Then change function to dynamically change route: 
 
 ```javascript
 onRouteChange = (route) => {
    this.setState({route: route});
  }
```
Then change signin.js, need to put arrow function in so it runs when clicked on not when rendered and tell it to go home: 
```javascript
<input 
	onClick={() => onRouteChange('home')}
	className="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" 
	type="submit" 
	value="Sign in"/>

```
Do same in Navigation.js but tell it to go to signin (i.e. this info is passed as route parameter to onRouteChange function):
```javascript
<p onClick={()=> onRouteChange('signin')} className='f3 link dim black underline pa3 pointer'>Sign Out </p>

```
Now signin screen shows when click sign out.

### Register ###

Create Register folder with Register.js file inside, add following text to .js file then copy code from SignIn component. Change name title to Register, add fields for name, change input button value to Register, remove register link: 

```javascript
import React from 'react';


const Register = ({onRouteChange}) => {
	return (
		<article className="br3 ba b--black-10 mv4 w-100 w-50-m w-25-l mw6 shadow-5 center">
		<main className="pa4 black-80">
		<form className="measure">
		<fieldset id="sign_up" className="ba b--transparent ph0 mh0">
			<legend className="f1 fw6 ph0 mh0">Register</legend>
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
			value="Register"/>
		</div>
		
		</form>
		</main>
		</article>
		);


}

export default SignIn;
```

In signin change register element to have onclick function: 
```javascript
<div className="lh-copy mt3">
			<p onClick={() => onRouteChange('register')} className="f6 link dim black db">Register</p>

		</div>
```
Then go to App.js and add conditional to give register:  

```javascript
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
```javascript
import Register from './Components/Register/Register'; 
```

Change value to Sign In on SignIn.js:
```javascript
<div className="">
			<input 
			onClick={() => onRouteChange('home')}
			className="b ph3 pv2 input-reset ba b--black bg-transparent grow pointer f6 dib" 
			type="submit" 
			value="Sign in"/>
		</div>
```
Add pointer to register so pointer shows on hover: 

```javascript
<p onClick={() => onRouteChange('register')} className="f6 link dim black db pointer">Register</p>
```


### Sign Out ###


Change Navigation. js to show register and sign in/out, then put conditional to change what shows depending on state. 

```javascript
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
						<p onClick={()=> onRouteChange('signin')} className='f3 link dim black underline pa3 pointer'>Sign In </p>
						<p onClick={()=> onRouteChange('register')} className='f3 link dim black underline pa3 pointer'>Register </p>
					</nav>
				);
			}
}

export default Navigation;
```
Also create isSignedIn state:
```javascript
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
Change onRouteChange function in App.js to add if statement for signed in and out state changes:

```javascript
onRouteChange = (route) => {
    if(route === 'signout') {
      this.setState({isSignedIn: false})
    } else if (route === 'home') {
      this.setState({isSignedIn: true})
    }
      this.setState({route: route});
  }
  ```

Then change Navigation Element on App.js to change signOut to change to SignIn: 

```javascript
<Navigation isSignedIn={this.state.isSignedIn} onRouteChange={this.onRouteChange}/>
```

### Tidy up ### 
   
Remove console.log(box)
   
Use destructuring to reduce this.state usage. Allows removal of this.state from all things listed in destructuring:
   
```javascript
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
```javascript
index.js:1 Warning: Invalid DOM property `for`. Did you mean `htmlFor`?
```
As can't use for= in JSX so change all these to htmlFor in SignIn.js and Register.js. 

Need to change form element to div because it is automatically submitting due to onSubmit event with type=submit. 
