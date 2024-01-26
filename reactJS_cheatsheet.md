# React cheat sheet

## Developer tools and insigths

### Devtools

Note: you'll need a chrome extension to access devtools when doing using react : [here](https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

### Vite

It has some build tool that combines css and js to create a bundle css file and a buncle css file: [here](https://vitejs.dev/)

### Ideal folder structure

```js
/*
    src
        Pages
        Components
        Hooks
*/
```

**Hooks** folder should only contain pure js files that will be consumed by JSX compoentns inside the **Pages** and **Components** folders  

## Parent & child components

### Controlled vs Uncontrolled components

- A **controlled component** has its UI controlled by the react state.
- An **uncontrolled component** has its UI not controlled by the react state.

### Lifting  the state up

- It's process that you do when two sibling component would need to communicate.
  - You  would then keep the state variables in the parent
  - The parent will provide call back functions to the child components as props
  - The child components will use these call back functions to update state objects accordingly
  - Here is an example:
  - In the snippet below, the **_Todo_** Component is the parent component. The **_InputBox_** component (ie child) uses the _onSubmitInput_ method from the props to update update the _tasks_ state object which resides inside the parent.

    ```js
        function InputBox({ onSubmitInput }) {
            const [value, setValue] = useState("");
            return (
                <div className="input_box">
                    <input type="text"
                        value={value}
                        onChange={(e) => { setValue(e.target.value) }}
                    />
                    <button onClick={
                        () => {
                            onSubmitInput(value);
                            setValue("");
                        }
                    }

                    >Add</button>
                </div>
            )
        }




        function Todo() {

            const [tasks, setTasks] = useState([]);

            const AddTask = (value) => {

                // alert("Added new task")
                // take input -> something-> add a task / alert 
                const allTask = [...tasks, value];

                setTasks(allTask);
            

            }
            return (
                <>
                    <InputBox onSubmitInput={AddTask}></InputBox>
                    <List tasks={tasks}></List>

                </>
            )
        }

    ```

## Hooks - useRef

- This hook is useful for cases when you want to keep values that would be lost at every execution of the render component

## Hooks - useEffect

### Component life-cycle phases

|Phase name      |Create phase  |Rendering phase |delete phase |
|--              |--          |--          |--          |
|**What happens**| Mounting**Note**: _useEffect_ hook Occurs here    | This is when the whole function component is ran **Note**: the _useState_ hook set state can cause a rerender  which will make the whole function compoenent to run again  | the unmount occurs|

### Anatomy

- the anatomy of use effect is as follows

   ```js
   const cleanUpAfterFirstUseFn =  useEffect(whenMountingFn,dpenencyArray); 
   ```

  - _whenMountingFn_ is the funciton that runs when mounting occurs . It will run once if the _dpenencyArray_ is an empty array
  - _cleanUpAfterFirstUseFn_ is a function that gets executed when before a rerender
    - this is a function that is usually returned by the _whenMountingFn_ function
  - The _dpenencyArray_ is an array that that usually triggers the _whenMountingFn_ at the next rerender.
    - Whenever the _dpenencyArray_ is updated, _whenMountingFn_ is executed.
    - If it is an empty array, the  _whenMountingFn_ will only run at first mount
      - **Note:**  the _cleanUpAfterFirstUseFn_ will run after the first execution as well.
    - If it is undefined, the  _whenMountingFn_ will run at every render.

       ```js
          // this will make whenMountingFn run all the time      
          const cleanUpAfterFirstUseFn =  useEffect(whenMountingFn);    
       ```

- **Note:** in strict mode, it is called twice the _whenMountingFn_ function is executed twice.
- **Note:** The use _whenMountingFn_ should not be async.  This is because async functions return promises.

### Use cases

**Use case 1:** User patience

- It's when you use skeleton in UI before data comes (ie when fetching)
- When data comes you can render  the data using the UI.
- The _whenMountingFn_ will contain the fetch. It will also call the setState function to render data.

**Use case 2:** when using setInterval or  resizeWindow call backs
**Use case 3:** when using dependency array for executions

## Routing

**Note**: it is preferred to do routing in client instead of fetching all HTML from server because network lag is greater than DOM manipulation

### Link component

- It is a built in react component used to simulate anchor tag.
- we would prefer to use this instead of anchor tag because anchor tag will load a page and load time is greater than DOM manipulation

### Routes Compoenent

It is a built in react component used as follows:

```jsx
    <Routes>
        <Route path="/somePath" element={<SomeComponent />} />
    </Routes>
```

Note:

- The **element** property is in JSX  because Routes is analogous to a switch statement. If you're not passing it in JSX, then it's as if you're passing a render function instead of a component.
- The **path** property is a string which is known as the **Template route**. It can be used to pass variables that will consumed by the  **element** component.
  - example:

    ```jsx
        <Routes>
            <Route path="/somePath/:id" element={<SomeComponent />} />
        </Routes>
        // this means that SomeComponent will be able to use the id variable 
    ```

### Implementing nested routes

1. **Template route** should have '*'
2. The nested routes woudld be defined inside of  **element** compoenent

example:

```jsx
    <Routes>
        <Route path="/somePath/*" element={<SomeComponent />} />
    </Routes>

    function SomeComponent(props)
    {        
        return (<>
            <Routes>
                <Route path="/somePath/lookedDeeper" element={<SomeDeepComponent />} />
            </Routes>
        <div>I am some component</div></>)
    }

```

## Hooks -  useParams

Its used to get attribute values inside a **template route**.

## Hooks -  useContext hook ( ie Context API )

### Anantomy of useContext

The anatomy is as follows:

```js
const contextStateObj = useContext(ContextWrapper);
```

The **ContextWrapper** is an object that will contain a **Provider**. That provider is the component that is the actual context. the wrapper just wraps it.

- it is created using the React.createContext function.

The **contextStateObj** is the state object that has been provided by the root object.

It would usually go like this:

```jsx
const ContextWrapper = React.createContext();

// note the contextStateObj must be used through a custom hook
const useSomeCustomHookToGetContextObj = function(){
    const contextStateObj = useContext(ContextWrapper);
    return contextStateObj;
}

function SomeRootComponent(prop)
{
    const [mainUser,setMainUser] = useState({name:"Main Guy",age:"ancient"});
    return (
        <>
            <ContextWrapper.Provider value ={mainUser,setMainUser}>
                <SomeChildComponent />
            </ContextWrapper.Provider>
        </>
    )
}
function SomeChildComponent()
{
    const contextStateObj = useSomeCustomHookToGetContextObj();

    function makeYoung()
    {
        const user = {...contextStateObj.mainUser};
        user.age = "young";
        contextStateObj.setMainUser(user);
    }

    return (
        <div>
            <button onClick={makeYoung}>make young</button>
            {JSON.stringify(contextStateObj.mainUser)}
        </div>
    )
}


```

### Major use case of context API

- To reduce **pop drilling**.
  - Note: **pop drilling** is when you are lifting the state up to communicate with other components. However not all children state need to consume the state
- When the state is a global object, like the theme, auth, or cart

### Cons of context API

- If the state inside of context is updated, then all the sub components will be updated as well, and it hurts perfomance.

## Hooks -  useReducer hook

### Anantomy of useReducer

- The anatomy is as follows

  ```js
    const [state,dispatchFn] = useReducer(reducerFn,initialState);
  ```

  - **dispatchFn**: it is the funciton responsible for executing the **reducerFn**.
  - **reducerFn**: it is the function responsbile for managing ( i.e updating the state)
  - **state**: its the state object
  - **initialState**: initial value of state object

- The anatomy of the reducerFn (ie reducer function) is as follows:

  ```js
  // note this is kinda like a bad example because its supposed to return a new state. in this case its returning undefined
   const reducerFn = function(stateThatWillChange,chosenAction){

        const actionMenu = {
            "doThis" : ()=>{console.log("doing this")},
            "doThat" : ()=>{console.log("doing that")}
        };

        const runChosenAction = actionMenu[chosenAction];
        runChosenAction();
      
   } 
  ```

- Note: the reducer function will be executed when the **dispatchFn** is invoked as follows:
  
  ```js
        dispatch("doThis") // this will make sure that doThis is called
  ```

### Major use case of useReducer

- It is an alternative for **useState**.
- It is preferable to use it when dealing with complex state objects

### useState vs useReducer

- userState
  - input: intial state
  - returns: array with state obj, and setter function
- use reducer
  - input: initial state, reducer function
  - returns: array with state obj, and dispatch function

_**remark**: reducer seems very similar to front command pattern_

## Redux

### why redux

- So, one of the major cons using context is the fact that it renders sub component.
  - This is crazy considering that in real world applications, there can be thousands of sub-component.
- in the end , redux is goign to use context along with reducer to reduce rendering all sub-components.
