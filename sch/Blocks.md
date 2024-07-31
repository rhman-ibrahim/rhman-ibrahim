[![Tools](https://skillicons.dev/icons?i=js,vite,react,redux)](https://skillicons.dev)

# Blocks

A JavaScript, React (Vite) components library to build a responsive flex layout.

---

01. State
    01. [Blocks Slice](#block-slice)
    02. [Theme Slice](#theme-slice)
02. Main Components
    01. [Column](#column)
    02. [Layout](#layout)
03. Side Components
    01. [Header](#header)
    02. [Aside](#aside)
    03. [Footer](#footer)
04. Hooks
    01. [useWindowHeight](#the-window-height-hook)
    02. [useObserver](#the-observer-hook)

---

# State

In Blocks the state is managed with **Redux** and **Redux Tool Kit**, because of their excellence in management state in React applications due to their predictable state management, which simplifies debugging and testing.

|Dependency|Role|
|---|---|
|Redux|Provides a centralized store for all application state, ensuring consistency across components.|
|Redux Tool Kit|Enhances Redux by reducing boilerplate code, offering built-in best practices, and integrating tools like `createSlice` and `createAsyncThunk` for easier reducer and asynchronous logic creation, making state management more efficient and developer-friendly.|

## Block Slice

### Porperties

|Property|Usage|
|---|---|
|`type`|A string value that defines the currently in use **Layout** type.|
|`nav`| A boolean value that states the dispay state of **Nav** buttons.
|`column`|A string value that defines the displayed section if it is hidden by default according to the CSS media queries.|
|`header`|A string value that defines the currently displayed **Header** identifier.|
|`aside`|A string value that defines the currently displayed **Aside** identifier.|
|`footer`|A string value that defines the currently displayed **Footer** identifier.|

### Reducers

|Reducer|Usage|
|---|--|
|`setType`|Sets the **Layout** type value, this value is used by other components like **SectionButtons**, this reducer is used in the component's UseEffect hook only.|
|`toggleNav`|Toggles the **Nav** buttons display state between true and false.|
|`setSection`|Sets the displayed **Column** name which results in dislaying it if it is not displayed.|
|`setHeader`|Sets the **Header** identifier which results in displaying it, only a single **Header** could be displayed at a time.|
|`setAside`|Sets the **Aside** identifier which results in displaying it, only a single **Aside** could be displayed at a time.|
|`setFooter`|Sets the **Footer** identifier which results in displaying it, only a single **Footer** could be displayed at a time.|
|`unsetBlocks`| Unsets each of section, footer and aside.

## Theme Slice

### Porperties

|Property|Usage|
|---|---|
|`mode`|Difines the current theme mode which should be **dark** by default or **light**.|
|`node`|Defines the current theme node which contains ***mode***: the current mode name, ***icon***: the current mode icon, and ***next***: the next mode if toggled.|

### Reducers

|Reducer|Usage|
|---|--|
|`toggleTheme`|Toggles the current theme between (dark (default) and light) modes.|
|`resetTheme`|Resets the theme mode to the browser preference if there is, else it sets it to **dark**.|

---

# Main Components

The main components are essential for **Blocks** to work properly, they are `Layout` and `Column`, use the main components to display the main content in columns.

## Column

01. The **Column** component is the building block of the layout, it is a flex element with a *flex's direction set to column* and its *justify-content* and *gap* properties are set by its props: `String: justify` ***'flex-start' (default), 'center', 'flex-end'*** and `Numbe: gap` ***8 (default), values passed are converted using string template to '8px'***. But, the main prop is the `position` prop ***String: 'left', 'center' (default) or 'right'*** which sets the position of the column in the layout.
    

    01. A primary **Column**'s ***position*** prop is to `'center'`.
    02. A secondary **Column**'s ***position*** prop is to `'left'` or `'right'`.
    03. A Secondary section is hidden by default, it is displayed by navigation button (at bottom right of the screen) or automatically at the layout configured breakpoint.
    04. A Layout consists of at least 1 single primary column only, or at most of 1 single primary column and 2 secondary columns (with different directions). 

## Layout

02. The **Layout** component (layout) is a flex element with a *flex's direction set to row*, it wraps the (**Column**) component/s.

    ### Props

    01. ***type*** is a string prop (set to `M1` by default), it also coud be set to `'M1', 'M2','MS','ME','M3','MC'`.
    02. ***notificationsAside*** is a boolean prop (set to `false` by deault) which adds the notifications aside's open button in the nav if set to `true`.
    03. ***actionsAside*** is a boolean prop (set to `false` by deault) which adds the actions aside's open button in nav if set to `true`.
    04. ***leftColumnIcon*** is an object prop (set to `{type:'material-symbols-outlined', name:'chevron_right'}` by default) which sets the left's section button's icon.
    05. ***rightColumnIcon*** is an object prop (set to `{type:'material-symbols-outlined', name:'chevron_left'}`) which sets the right's section button's icon.

    ### Types

    01. **`'M1'`** is the default **Layout** type, it consists of a single column with a maximum width of `640px`, extra width is splitted on both sides.
    ```
    <Layout>
        <Column>
            <h1>Hello, World!</h1>
        </Column>
    </Layout>
    ```
    02. **`'M2'`** consists of **2** columns with ***1:1 ratio*** (columns are equal in width). The secondary section is displayed at `640px` breakpoint.
    ```
    <Layout type='M2'>
        <Column>
            <h1>primary</h1>
        </Column>
        <Column position='right'>
            <h1>secondary</h1>
        </Column>
    </Layout>
    ```
    03. **`'MS'`** consists of **2** columns with ***2:1 ratio*** (the first column is twice the width of second section). The second section is displayed at `960px` breakpoint.
    ```
    <Layout type='MS'>
        <Column>
            <h1>primary</h1>
        </Column>
        <Column position='right'>
            <h1>secondary</h1>
        </Column>
    </Layout>
    ```
    04. **`'ME'`** consists of 2 columns with ***1:2 ratio*** (the second column is twice the width of first column). The second section is displayed at `960px` breakpoint.
    ```
    <Layout type='ME'>
        <Column position='left'>
            <h1>secondary</h1>
        </Column>
        <Column>
            <h1>primary</h1>
        </Column>
    </Layout>
    ```
    05. **`'M3'`** consists of **3** columns with **1:1:1 ratio** (columns are equal in width). The right section is displayed at `640px` and the left section is displayed at `960px`.
    ```
    <Layout type='M3'>
        <Column position='left'>
            <h1>secondary 1</h1>
        </Column>
        <Column>
            <h1>primary</h1>
        </Column>
        <Column position='right'>
            <h1>secondary 2</h1>
        </Column>
    </Layout>
    ```
    06. **`'MC'`** consists of 3 columns with **1:2:1 ratio** (the middle section is twice each of left and right sections). The right section is displayed at `960px` and the left section is displayed at `1280px`.
    ```
    <Layout type='M3'>
        <Column position='left'>
            <h1>secondary 1</h1>
        </Column>
        <Column>
            <h1>primary</h1>
        </Column>
        <Column position='right'>
            <h1>secondary 2</h1>
        </Column>
    </Layout>
    ```

    ### Elements

    05. **nav** is a part of the **Layout** component, it provides layout buttons positioned at the bottom right corner.

        01. ***Columns buttons*** a button for every layout section.
        02. ***ThemeButton*** is used to toggle the theme modes.
        03. Actions aside button if the *actionsAside* prop is `true` this button is used to open it.
        04. Notifications aside button if the *notifyAsude* prop is `true`, this button is used to to open it.
        05. ***AsideCloseButton*** if there is an opened aside, this button is used to close it.
        06. ***FooterCloseButton*** if there is an opened footer, this button is used to close ot.
    
    02. **hr** is a part of the **Layout** component, it overflows the **Layout** causing a blur effect when a section or aside is opened.

    ### Events

    01. **keydown** it listens to key stroks the combination of `Alt, 'l'` opens the left section, the combination of `Alt, r` opens the right section and `Esc` closes everything.

# Side Components

The side components are optional to use, they are `Header`, `Aside` and `Footer`, each is opened by a click on `HeaderButton`, `AsideButton` and `FooterButton` respectively and closed by ***nav** close button in **Layout**. Use side components to display content needed on request/click.

## Header

04. Use **Header** component to let the use take an action. **Header** is positioned at top, with full width. To use the **Header** component create a **Header** and **HeaderButton** components of the same `identifier`.

    01. The **Header** component should be inside the **Layout** before its closing tag **\<Layout />**.
    ```
        <Header
            identifier="BlocksHeader"
            message="Greetings"
            actions={
                [
                    {
                        name:'emoji_people',
                        icon:'material-symbols-outlined',
                        function: () => {
                            const greetings = [
                                "مرحبا",
                                "Hello!",
                                "Hi there!",
                                "Greetings!",
                                "Howdy!",
                                "Hey!",
                                "What's up?",
                                "Good to see you!",
                                "Hiya!",
                                "Bonjour!",
                                "Hola!"
                            ];

                            alert(
                                greetings[
                                    Math.floor(
                                        Math.random() * greetings.length
                                    )
                                ]
                            );
                        }
                    },
                    {
                        name:'Say Bye!,
                        function: () => {
                            alert('Bye!');
                        }
                    }
                ]
            }
        />
    ```

    02. To use the **Header** component properly provide at least one of its props: `message` to show a suitable message according to the context, or `actions` to provide a list of actions/single action.

    03. Use the `autoClose` prop to close the **Header** component after executing the action clicked by the user, (the default is `false`: which means that it won't close by itself after the action being executed).

    04. For each action provided a button will be created, provide a name/icon name for this button as in the example above.

## Aside

05. Use the **Aside** component to show side content, **Aside** is positioned at the right, with full height and 320px with. To use the **Aside** component create an **Aside** and **AsideButton** components of the same `identifier`.

    01. The **Aside** component should be inside **Layout**, after the **Footer**.
    ```
        <Aside identifier="BlocksFooter">
            ....
        </Aside>
    ```
     
    02. The **AsideButton** should be inside a section directly or indirectly.
    ```
        <AsideButton
            identifier="BlocksAside"
        />
    ```
    
    03. The **AsideButton** has an icon prop to be used with ***Google Material Icons***, by default it uses `open_in_new` from `material-symbols-outlined`.
    ```
        <AsideButton
            identifier="BlocksAside"
            icon={
                type:'material-icons',
                name:'person'
            }
        />
    ```

### Special Asides

Special asides are ready to use asides with predefined identifiers for common needs accross different applications, the special thing about special asides that they have a separate special button in the **Layout**'s nav.


01. `ActionsAside`, use this aside to display user actions that always needed to be accessible every where.

    ```
    <ActionsAside>
        ....
    </ActionsAside>

    // or

    <ActionsAside children={ .... } />
    ```

02. `NotificationsAside`, use this aside to display notifications.

    ```
    <NotificationsAside>
        ....
    </NotificationsAside>

    // or

    <NotificationsAside children={ .... } />
    ```

## Footer

06. Use the **Aside** component to show side content, **Footer** is positioned at the bottom with height of 120px, and a width of maximum 480px at 640px breakpoint and of width of maximum 720px at 960px breakpoint. To use the **Footer** component create a **Footer** and **FooterButton** components of the same `identifier`.

    01. The **Footer** component should be inside **Layout**, after the **Layout** opening tag directly.
    ```
        <Footer identifier="BlocksFooter">
            ....
        </Footer>
    ```
     
    02. The **FooterButton** should be inside a section directly or indirectly.
    ```
        <FooterButton
            identifier="BlocksFooter"
        />
    ```
    
    03. The **FooterButton** has an icon prop to be used with ***Google Material Icons***, by default it uses `open_in_new_down` from `material-symbols-outlined`.
    ```
        <FooterButton
            identifier="BlocksFooter"
            icon={
                type:'material-icons',
                name:'settings'
            }
        />
    ```
# Hooks

Custom hooks in React are a way to encapsulate and reuse stateful logic across multiple components. They allow you to extract component logic into reusable functions. A custom hook is essentially a JavaScript function whose name starts with "use" and that can call other hooks.

## The Window Height Hook

`useWindowHeight` is used internally to set the **Layout** and **Column** components height to the visible space's height (space available for the content only).

## The Observer Hook

`useObserver` Utlizies the built-in JavaScript Intersection Observer API, it should be provided with 2 values to work (CSS selector and the least threshold to be recognized as visible).