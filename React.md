# Immune Props

1. Object Freeze
2. Proxy the Object and throw error if set is called
3. Immuntable.js
4. Object.define property
5. Object.seal
6. private field

# what happen when setState() is called

The first thing React will do when setState is called is **merged the object** you passed into setState into the current state of the component. This will kick off a process called **reconciliation**. The end goal of reconciliation is to, in the most efficient way possible, update the UI based on this new state.

To do this, React will construct a new tree of React elements (which you can think of as an object representation of your UI). Once it has this tree, in order to figure out how the UI should change in response to the new state, React will diff this new tree against the previous element tree.

By doing this, React will then know the exact changes which occurred, and by knowing exactly what changes occurred, will able to **minimize its footprint** on the UI by only making updates where absolutely necessary.

The setState() will run functions in this order:

1. shouldComponentUpdate()
2. componentWillUpdate()
3. render()
4. componentDidUpdate()

# Key

When children have keys, React uses the key to match children in the original tree with children in the subsequent tree.

The key only has to be unique among its siblings, not globally unique.

# React-Virtualize

So many elements in the DOM can cause two problems:

- Slow initial rendering
- Laggy scrolling

> How does react-virtualized work?

**rendering only what is visible**, this one is the same as List Adapter in Android

1. They calculate which items are visible inside the area where the list is displayed (the viewport).
2. They use a container (div) with relative positioning to absolute position the children elements inside of it by controlling its top, left, width and height style properties.

### Important HOC for this article

- **ArrowKeyStepper**. It decorates another component so it can respond to arrow-key events.
- **AutoSizer**. It automatically adjusts the width and height of another component.
- **CellMeasurer**. It automatically measures a cell’s contents by temporarily rendering it in a way that is not visible to the user.
- **ColumnSizer**. It calculates column-widths for Grid cells.
- **InfiniteLoader**. It manages the fetching of data as a user scrolls a List, Table, or Grid.
- **MultiGrid**. It decorates a Grid component to add fixed columns and/or rows.
- **ScrollSync**.It synchronizes scrolling between two or more components.
- **WindowScroller**. It enables a Table or List component to be scrolled based on the window’s scroll positions.

**Components like AutoSizer use a pattern named function as child components.**

    <AutoSizer>
    ({ width, height }) => {
    }
    </AutoSizer>

**cannot share a CellMeausure cache between two components**

# React vs React Native?

> What's the different ?

React -> JS Engine -> Browser (Document) -> OS
React Native -> JS Engine -> Brige -> OS

In React Native, js code will be serialize (parse) into the OS language its required to run on native apps

React is a library, it's allow you to do more than follow a fixed structure while React Native is a framework which force you to follow the structure

# Stale Closure when using React Hooks

    function WatchCount() {
        const [count, setCount] = useState(0);
        useEffect(function() {
            setInterval(function log() {
            console.log(`Count is: ${count}`);
            }, 2000);
        }, []);
        return (
            <div>
            {count}
            <button onClick={() => setCount(count + 1) }>
                Increase
            </button>
            </div>
        );
    }

> Here's how to fix it

    useEffect(function() {
        const id = setInterval(function log() {
        console.log(`Count is: ${count}`);
        }, 2000);
        return function() {
            clearInterval(id);
        }
    }, [count]);

We fix the interval by creating a new one after 2 second -> that's when closure capture new value

# Render Props

Refer to a technique for sharing code between React components using a prop whose value is a function

> Remove duplicate code between components

The Pattern is to create a **wrapper function** at the top level -> passing down the props as function use to render the state and wire it with function that use to modify the state.

more depth: https://www.youtube.com/watch?v=3IdCQ7QAs38

# Virtual DOM vs Real DOM

compare works in RAM for Virtual DOM so it's faster than RealDOM
