Quick Start Guide:

npm install
npm start
cd api
npm start


Notes:  The goal of this exercise is to connect Node.js to React.js using Express.js.  ***As with all programing languages, every detailed letter, space, and symbol is 'mission critical,' meaning that if something doesn't work along the way, please go back and review for all possible human errors.  Some example errors that were encountered along the way are included, but for time and efficient not all errors and edits are included in this text document, but the proper solutions are included leading to a functional outcome.***  Note that ".gitignore" is used in this package to reduce its weight.  This means that upon attempting to run in your environment will require that "ignored" modules be uploaded to your environment before the package runs.  One example includes the "node_modules" which will be installed when running the command below (i.e. "npx").  

1.  Start by ensuring that Node.js is installed
2.  Create a folder called "reactjsPractice1"
3.  Open "reactjsPractice1" in VS Code 
4.  Open Terminal/New
5.  Initiate reactedJS client creation using the following command:  npx create-react-app client
6.  The "npx" command will install and once installed it will execute installed modules setting up a pre-built file directory (client/node_modules, public, src, .gitignore, etc.).
7. After the client installation / execution was complete, there is a tip on getting started:

"We suggest that you begin by typing:

  cd client
  npm start

Happy hacking!"

8.  After changing the directory using command "cd client" and then npm start, the browser automatically loads display the React Logo on black background using:  localhost:3000/.
9.  Terminal displays:  

"Compiled successfully!

You can now view client in the browser.

  Local:            http://localhost:3000        
  On Your Network:  http://192.168.56.1:3000     

Note that the development build is not optimized.
To create a production build, use npm run build."

10.  Opened a new Command Prompt, ensure that previous node.js servers stopped running using Ctrl C.
11.  In the new command prompt create a new application, an "API" application using the following command:
npx express-generator api

    final display in command prompt - 
     change directory:
     > cd api

   install dependencies:
     > npm install

   run the app:
     > SET DEBUG=api:* & npm start


12.  After it installs and executes (i.e. np"x" instead of "m") open a new VS code instance.
13.  In the terminal of this new VS Code instance opened to the "api" application folder, install all necessary npm packages using command:
npm install.
14.  Good practice to run command:  npm install twice just to be sure, the 2nd time should be brief.
15.  Go back to the Client side VS code instance and in the Terminal, terminate the batch job using command:
Ctrl C, and Y
16.  Go back to the API VS Code instance terminal and initiate using command:
npm start
17.  Upon refreshing the browser at localhost:3000, the standard default page for Express will show, <h1>Express</h1>
<p>Welcome to Express</p>
replacing the original React that displayed in the browser previously.
18.  Inside of the VS Code instance for the API folder, go inside of the bin folder and select the "www" file.
19. Change the default PORT from 3000 to 9000:

var port = normalizePort(process.env.PORT || '9000');
app.set('port', port);

20.  In the terminal, terminate the batch job in the VS Code for the API app using Ctrl C.
21.  Still in the VS code instance for the API app go to the Routes folder and create a new file called, "testAPI.js"
22.  Provide instrunctions for default routing using express:
var express = require("express");
var route = express.Router();
23.  Include the standard "callback" function with parameters requests, response, and "next" as a placeholder in case we add an additional function later on:

router.get("/", function(req,res,next){
    res.send("API is working properly");
});

24.  Use pre-installed or built in node.js function commands module and exports to assign to the route to the default page "/".

25.  Next go the the app.js file and assign an additional app.use instruction to ***import*** by inserting under the other 2 app.use instructions:

app.use('/testAPI', testAPIRouter);

26.  In the same app.js file, under the other 2 router variable assignments, add a third, assigning the testAPIRouter which should auto populate as you begin typing:
testAPIRouter = require("./routes/testAPI");

coloring should match existing code elements.

27.  Next, use npm start to launch the API application in the terminal of the API VS code:
npm start
28.  ***This completes the API Test*** You should see "API is working properly" displayed in the browser at:  localhost:900/testAPI.  Following this go back to the Client side VS code instance.
29.  Next go the src folder and to the App.js file for edits below the existing imports already listed:


class App extends React.Component{
  constructor(props){
    super(props);
    this.state={apiResponse:""};
  }

  callAPI() {
    fetch("http://localhost:9000/testAPI")
      .then(res => res.text())
      .then(res => this.setState({apiResponse: res}));
  }

  componentWillMount(){
    this.callAPI();
  }
}
render(){
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
      
      </header>
      <p>{this.state.apiResponse}</p>
    </div>
  );
}


export default App;

30.  ***Cross Origin Resource Sharing: Allow the React application to communicate with another hosted domain; we need to enable cross origin scripting and sharing*** - back to the API side VS Code instance, and use Ctrl C to ensure that the batch job isn't running in the terminal.

Next, perform a global install for all applications:

npm install --save cors

***type cls & enter to clear the screen***

31.  Still in the API side of VS Code go into the app.js file to insert "cors" using app.use:

app.use(logger('dev'));
app.use(express.json());
app.use(cors());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, 'public')));

32.  Declar the cors variable and import it using require:

var logger = require('morgan');
var cors = require('cors');

33.  Next fire up the api application using:

npm start

34.  Next fire up the client side application using:

npm start

*35.  Note that localhost:3000 is the React application (i.e. the client) and localhost:9000 is the access point (API)through which we can interact with the client using Express.js.*

***When the client side application fired up, an error displayed in the browser with very clear instructions on where the concern was located and step 29 above was updated to properly close the render function with brackets(VS Code is set to autosave so after starting the client auto compilation began): ***

Failed to compile
./src/App.js
  Line 22:9:  Parsing error: Unexpected token, expected ";"

  20 |   }
  21 | }
> 22 | render(){
     |         ^
  23 |   return (
  24 |     <div className="App">
  25 |       <header className="App-header">
This error occurred during the build time and cannot be dismissed.

36.  With this error, go back and stop both client and api terminals using Ctrl C and restart, with API side first repeating steps 33 and 34.

37.  The same error appeared again, and it seems that the problem is on line 21 caused by an unecessary bracket.  Previous changes suggested in line 35 were undone to reflect the following:

render(){
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
      
      </header>
      <p>{this.state.apiResponse}</p>
    </div>
  );
 }
}

export default App;

38.  Once the unecessary bracket in code line 21 was removed, the "1" that appeared in the file director view next to App.js disappeared as well as the red underscore under the bracket next to render() on line 22.  Repeat step 36.

39.  This time the React.js logo appeared in the client browser as expected, and it now spins ; )

40.  Going to localhost:9000/testAPI yields the text message, "API is working properly" demonstrating that we have successfully pinged the API hosted in Node.js. The client side terminal yields:

Compiled successfully!

You can now view client in the browser.

  Local:            http://localhost:3000        
  On Your Network:  http://192.168.56.1:3000     

Note that the development build is not optimized.
To create a production build, use npm run build. 

API side terminal yields:

> api@0.0.0 start C:\Users\TopCoder\Documents\CodeSquad\Personal Project\Zillow Clone Examples\reactjsPractice1\api
> node ./bin/www

GET /testAPI 200 6.374 ms - 23
GET /testAPI 200 0.691 ms - 23
GET /testAPI 304 1.006 ms - -










***the text below was pre-populated by the bootstrapped:  Create React App***




This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br />
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br />
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

Video [Tutorials](https://www.youtube.com/watch?v=fnpmR6Q5lEc&feature=youtu.be). 

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: https://facebook.github.io/create-react-app/docs/code-splitting

### Analyzing the Bundle Size

This section has moved here: https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size

### Making a Progressive Web App

This section has moved here: https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app

### Advanced Configuration

This section has moved here: https://facebook.github.io/create-react-app/docs/advanced-configuration

### Deployment

This section has moved here: https://facebook.github.io/create-react-app/docs/deployment

### `npm run build` fails to minify

This section has moved here: https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify
