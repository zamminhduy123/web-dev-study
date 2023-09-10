# **BEM - Block | Element | Modifier**

## Others Methodologies 

- **OOCSS** — Separating container and content with CSS “objects”
- **SMACSS** — Style-guide to write your CSS with five categories for CSS rules
- **SUITCSS** — Structured class names and meaningful hyphens
- **Atomic** — Breaking down styles into atomic, or indivisible, pieces

## **Definition**

### Block

Standalone entity that is meaningful on its own.

Ex: header, container, menu, checkbox, input, ...

### Element

A part of a block that has no standalone meaning and is semantically tied to its block.

Examples: menu item, list item, checkbox caption, header title

Modifier
A flag on a block or element. Use them to change appearance or behavior.

Examples: disabled, highlighted, checked, fixed, size big, color yellow


### Benefits

- **Modularity**
Block styles are never dependent on other elements on a page, so you will never experience problems from cascading.

You also get the ability to transfer blocks from your finished projects to new ones.

- **Reusability**
Composing independent blocks in different ways, and reusing them intelligently, reduces the amount of CSS code that you will have to maintain.

With a set of style guidelines in place, you can build a library of blocks, making your CSS super effective.

- **Structure**
BEM methodology gives your CSS code a solid structure that remains simple and easy to understand.


## **Dive Deep**

1. ### **Block**

The block name describes its purpose ("What is it?" — menu or button), **not its state** ("What does it look like?" — red or big).

The block **shouldn't influence its environment**, meaning you shouldn't set the external geometry (margin) or positioning for the block.

> You also shouldn't use CSS tag or ID selectors when using BEM.

- Nesting
Blocks can be nested in each other. You can have any number of nesting levels.

2. ### **Element**

The element name **describes its purpose** ("What is this?" — item, text, etc.), **not its state** ("What type, or what does it look like?" — red, big, etc.).

The structure of an element's full name is **block-name__element-name**. The element name is separated from the block name with a double underscore (__).

- Elements can be nested inside each other. You can have any number of nesting levels.

- An element is always part of a block, not another element. This means that element names can't define a hierarchy such as block__elem1__elem2.
- An element is always **part of a block,** and you shouldn't use it separately from the block.

### **What to choose (Element || Block)**

- ### Block: If a section of code might be reused and it doesn't depend on other page components being implemented.

- ### Element: If a section of code can't be used separately without the parent entity (the block).

> In the BEM methodology, you can't create elements of elements. In a case like this, instead of creating an element, you need to create a service block.

3. ### **Modifier**

An entity that defines the appearance, state, or behavior of a block or element.

- The modifier name describes its appearance ("What size?" or "Which theme?" and so on — size_s or theme_islands), its state ("How is it different from the others?" — disabled, focused, etc.) and its behavior ("How does it behave?" or "How does it respond to the user?" — such as directions_left-top).

- The modifier name is separated from the block or element name by a single underscore (_).

### **Types of modifiers**

- Boolean: focused, disabled, ...
- Key-value: theme_dark, theme_islands, ... **(theme is modifier key and dark is modifier value)**


### **Guildlines**

- Can't be used alone: From the BEM perspective, a modifier **can't be used in isolation** from the modified block or element. A modifier **should change the appearance, behavior, or state** of the entity, not replace it.

### **Mix**
A technique for using different BEM entities on a single DOM node.

A technique for using different BEM entities on a single DOM node.

Mixes allow you to:

Combine the behavior and styles of multiple entities without duplicating code.

Create semantically new UI components based on existing ones.

Example

        <!-- `header` block -->
        <div class="header">
            <!--
                The `search-form` block is mixed with the `search-form` element
                from the `header` block
            -->
            <div class="search-form header__search-form"></div>
        </div>

### **File structure**

Features:

- A single block corresponds to a single directory.

- The block and the directory have the same name. For example, the header block is in the header/ directory, and the menu block is in the menu/ directory.

- A block's implementation is divided into separate technology files. For example, header.css and header.js.

- The block directory is the root directory for the subdirectories of its elements and modifiers.

- Names of element directories begin with a double underscore (__). For example, header/__logo/ and menu/__item/.

- Names of modifier directories begin with a single underscore (_). For example, header/_fixed/ and menu/_theme_islands/.

- Implementations of elements and modifiers are divided into separate technology files. For example, header__input.js and header_theme_islands.css.

# Ref
- https://en.bem.info/methodology/quick-start/
- https://getbem.com/introduction/