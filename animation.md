# Every thing about i know about ANIMATION in web development

## Browser phases

1. Recalculate style
2. Layout
3. Paint

usually the longest-running step of the rendering process

4. Composite

Phase **2 and 3** are the most heavy computing for CPU

There's 2 threads 
1. Main thread
2. Composite thread

Composite will have opererations that runs in GPU which will accelerate the animating process rather than leave the animating part for main thread

> Choose `transform` and `opacity`

These property animation will let the browser not re-do the layout and paint and it only affect the composite part - which can be run in GPU

## What can we do if we want to animate other property

1. Animate the deepest element you can choose

Choosing element which doesn't have many childs and elements inside it can lower the performance needed to be recalculate 

2. Direct DOM manipulation

> force synchronous layout

- Javascript always caches a snapshot of the previous frame’s layout so when writing to the DOM, the browser is smart enough to not run Layout until the end of Javascript

> Don't do DOM **reading** after **writing**

Because it will force the browser to run **Layout** before the end of JS phase, generate unnesscesary works

Elements that are hidden with `display: none` do not trigger the rendering waterfall when they are changed. If possible, make changes to the element before it becomes visible

3. requestAnimationFrame

- delay and only call this when before painting of each frame

4. Web Animation API

- lets you build Javascript animations that run on the compositor thread

## Always be measuring

1. **Paint Flashing** and **Layer Borders**

Paint Flashing highlights the parts of a page that need to be repainted by flashing them in green

2. Analyze Runtime Performance