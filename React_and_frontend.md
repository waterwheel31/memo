# React, Redux and Web Frontend


## React 
- Concept
    - UI in React is a function of state
    - React has numbers of third party libraries to make fancy UI easier
    
- Setup
    - Install Node.js   (https://www.ostechnix.com/install-node-js-linux/)
    - `sudo apt-get install -y build-essential` 
    - install yarn  (Yarn is a package manager crated by Facebook)
    - `npm install -g create-react-app`  (this reads `package.json`)


- Create and run a project
    - `npx create-react-app <projectname>`  (be careful. not `npm`, but `npx`)
    - `npm install`
    - `npm start` or `yarn start` inside the project directory 
    

- Start server (Apache)
    - Run Apache server: `sudo service apache2 status`
    - Configure the server


- Key packages (optional)
    - `npm install --save react-router-dom`   (this is router for web)
        - and then `npm add react-router-dom` 
    - `npm install --save react-router-native` (this is for mobile)
    - `npm install --save form-serialize`
    - `npm install --save prop-types`
    - `npm install --save escape-string-regexp sort-by` 
    - `npm install react-reduct redux`
    - `npm add reduct-thunk` 
    - `npm add react-icons`
    ` `npm install @material-ui/core`


- Attributes
    - `state`: this is like member variable of a class. Called by `this.state.xxx` 
        - to change, use `this.setState()`
    - `props`: this is like arguments. Called by `this.props.xxx` 
        

- Special IF clauses often used in React community
   - ` A === B ? <true case> : <false case>` 
   - ` A === B && <true case>` 


## Redux 

- Concept:
    - Redux is a library to manage states
    - Can be used for any UI including React, Vue, HTML vanila JS, etc.
    - States are
        -  managed at one point (Store)
        -  read-only, meaning only changable by dispathing an action
    - Action is a dictionary like object and has `type` and `todo` attributes
    - Reducer is a function to tell new State
        - this should be a `pure function`
        - takes two arguments: `State' and 'Action' and return new 'State'
        - if multiple Reducers need to be callsed, a good way is to have a root Reducer to call other Reducers
    - Store has following functions 
        - `getState` : to return current State
        - `subscribe` : to listen changes 
        - `dispatch`: to update State
             - receive `Action`, call a `Reducer` to update to new `State`

- Usage
    - link to: `<script src="https://cdnjs.cloudflare.com/ajax/libs/redux/3.7.2/redux.min.js"></script>` 
    - `Redux.createStore()`
    - Middleware
        - `Redux.applyMiddleware(checker)
        - `const checker = (store) => (next) => (action){}`, and `return next(action)`
    - Use Redux state on React
        - `mapStateToProp`: to let component to access to the State
        - `mapDispatchToProp`
        - `connect`
        - then the states can be called from `this.props.<statesitem>`


- Reference
    - https://qiita.com/enshi/items/19b1924b72f8c2ffd1eb
    - https://qiita.com/mpyw/items/a816c6380219b1d5a3bf
    - https://koukitips.net/post1866/


## React Native

- React Native App 
    - install:  
        - `npm install -g expo-cli` 
    - Set Environment Variables
        - ANDROID_HOME
        - JAVA_HOME
    - Create: 
        - `expo init <projectname> 
    - Launch simulator on Andorid Studio
        - open expo project with Android Studio
        - Open AVD manager 
        - Run the emulator
    - Run the project 
        - `expo start` 
        - click run Android from expo   
    - Add packages
        - `expo install <package>` - do not use `npm install` or `yarn install`, since those may cause troubles
    
- EXPO
- Simulators
    - iOS
    - Android
        - install: JDK
        - install android studio: https://developer.android.com/studio
- 


## Javascript
-   Usage:
    - `(...)`: spreading values from an array
    - if a key name of an object is the same of the value for the key, the keyname can be omitted