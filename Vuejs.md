# Two core features of Vue:

Declarative Rendering: Vue extends standard HTML with a template syntax that allows us to declaratively describe HTML output based on JavaScript state.

Reactivity: Vue automatically tracks JavaScript state changes and efficiently updates the DOM when changes happen.

# Single File Component (SFC)

Vue components using an HTML-like also known as `*.vue`

# API Styles

Vue components can be authored in two different API styles: **Options API** and **Composition API**.

# React alike

Cuz i started as a react dev so compare with it would be ezier

- state                                 : reactive
- ref                                   : **ref** too but this one take ref.value (**warning** this ref rerender: component on change)
- useEffect[] || componentDidMount      : onMounted
- React Portal                          : Teleport

# v-

To bind an attribute to a dynamic value, we use the **v-bind** directive can be shorthanded as **:id**

        <div v-bind:id="dynamicId"></div>

We can listen to DOM events using the **v-on** directive:

        <button v-on:click="increment">{{ count }}</button>

Due to its frequent use, **v-on** also has a shorthand syntax:

        <button @click="increment">{{ count }}</button>

To simplify two-way bindings, Vue provides a directive, **v-model**, which is essentially a syntax sugar for the above (***powerfull***)

        <input v-model="text">

We can use the v-if directive to conditionally render an element:
We can also use v-else and v-else-if to denote other branches of the condition:

        <h1 v-if="awesome">Vue is awesome!</h1>
        <h1 v-else>Oh no 😢</h1>

Introducing **computed()**. We can create a computed ref that computes its .value based on other reactive data sources:

        import { ref, computed } from 'vue'

        const hideCompleted = ref(false)
        const todos = ref([
        /* ... */
        ])

        const filteredTodos = computed(() => {
        // return filtered todos based on
        // `todos.value` & `hideCompleted.value`
        })

Side Effect with watch

        import { ref, watch } from 'vue'

        const count = ref(0)

        watch(count, (newCount) => {
        // yes, console.log() is a side effect
        console.log(`new count is: ${newCount}`)
        })

The parent can pass the prop to the child just like attributes. To pass a dynamic value, we can also use the v-bind syntax:

        <ChildComp :msg="greeting" />

A child component can accept input from the parent via props. First, it needs to declare the props it accepts:

        <!-- ChildComp.vue -->
        <script setup>
        const props = defineProps({
        msg: String
        })
        </script>

### Emits
In addition to receiving props, a child component can also emit events to the parent:

        <script setup>
        // declare emitted events
        const emit = defineEmits(['response'])

        // emit with argument
        emit('response', 'hello from child')
        </script>

### Slots
Component put in this is the fall back component and will be displayed if the parent did not pass down any slot content