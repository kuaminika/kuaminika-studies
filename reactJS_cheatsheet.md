# React cheat sheet

Note: you'll need a chrome extension to access devtools when doing using react : https://chromewebstore.google.com/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi


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
|**What happens**| Mounting <br> **Note**: _useEffect_ hook Occurs here    | This is when the whole function component is ran <br> **Note**: the _useState_ hook set state can cause a rerender  which will make the whole function compoenent to run again  | the unmount occurs|

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
