# Mục lục
1. Render

2. JSX

3. Lifecycle

4. Context, HOC
- Context:
    ```javascript
    - createContext
        const AppContext = React.createContext($defaultValue);
    - Context.Provider
        <AppContext.Provider value="">

        </AppContext.Provider>

    - Context.Consumer
        <AppContext.Consumer>
            ((value) => (<div>...</div>))
        </AppContext.Consumer>

    - Class.contextType = AppContext;
    - let value = Class.context;

    ```

5. Refs

6. Hook

7. Redux

8. Thunk

9. Saga