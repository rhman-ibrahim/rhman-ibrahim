[![Tools](https://skillicons.dev/icons?i=js,vite,react)](https://skillicons.dev)

# Fields

A JavaScript, React (Vite) components library which provides a styled form with functional buttons and multiple input components.

---

01. [Form](#form)
    01. [Submit](#submit-button)
    02. [Reset](#reset-button)
02. [Numb](#number)
    01. [Float](#float-input)
    02. [Integer](#integer-input)
03. [Pick](#pick)
    01. [Select](#select-input)
    02. [Checkbox](#checkbox-input)
    03. [Radio](#radio-input)
    04. [File](#file-input)
04. [Text](#time)
    01. [Hidden](#hidden-input)
    02. [Copy](#copy-input)
    03. [Password](#password-input)
    04. [Text Area](#text-area)
    05. [Text](#text-input)
    06. [Search](#search-input)
05. [Time](#time)
    01. [Day](#day-input)
    02. [Month](#month-input)
    03. [Date](#date-input)
    04. [Time](#time-input)

## Form

The Form component is a context provider created used React `useContext`, it used to manage the form reset and submit functionalities by utilizing `useRef`, `useState` and it expects form inputs as `children`. 

01. ### Submit Button

In order to display the form submit button the submit function has to be provided to `onSubmit` prop.
The Form component will handle collecting the form data from input (`formData`) using a `useRef` set to a unique identifier and the built-in Form API, this parameter `formData` is a must.

```
    const logFormData = formData => {
        console.log(formData)
    }

    <Form onSubmit={ logFormData }>
        ...
    </Form>
```

02. ### Reset Button

To use the reset functionality set the `resetButton` boolean prop to true, by double-clicking the reset button all values will be reset to their defaults (initial values set during the form creation), as this will toggle the Form component `reset` state variable which triggers the inner Input component reset function.

```
    const logFormData = formData => {
        console.log(formData)
    }

    <Form onSubmit={ logFormData } resetButton>
        ...
    </Form>

    // or

    <Form onSubmit={ logFormData } resetButton={ true }>
        ...
    </Form>
```

## Number

The `Numb` component is a number input handler, it works with inetegers and floats using sort of validators: regular expressions, minimum and maximum. The `Numb` handler component provides 2 styles of inputing: directly by updating the input manually, and indirectly by clicking increment and decrement buttons.

03. ### Float Input

```
    <Form onSubmit={ logFormData } resetButton>
        <Numb config={{ name:"a", type:"float", initial:11.11, min:7.7, max:12.14 }} />
    </Form>

    // Using the stepper input: a readOnly input, the buttons are used to update the value.

    <Form onSubmit={ logFormData } resetButton>
        <Numb config={{ name:"b", type:"float", initial:11.11, min:7.7, max:12.14, setp:1.1 }} />
    </Form>
```

04. ### Integer Input

```
    <Form onSubmit={ logFormData } resetButton>
        <Numb config={{ name:"c", type:"integer", initial:11, min:7, max:12 }} />
    </Form>

    // Using the stepper input: a readOnly input, the buttons are used to update the value.

    <Form onSubmit={ logFormData } resetButton>
        <Numb config={{ name:"d", type:"integer", initial:11, min:7, max:12, setp:1 }} />
    </Form>
```

## Pick

The `Pick` handler component gathers all form inputs of selecting a single choice or multiple choices from a list of values: `select`, `checkbox`, `radio` and `file`. In all of mentioned inputs the `multiple` prop is `false` by default, except for `checkbox` which allows multiple choice by nature.

The list of available choices is defined by 2 values (`choices` and `headings`) each has a different use, `choices` is the actual values list and `headings` is the representation by default `headings` is set to `choices`, this could be useful when working with multiple lanuages.

Each of `select`, `checkbox`, and `file` has default minimum value of 2 and maximum value of 3. These are the limits of number of choices could be made, to update them set the `min` and `max` props.

05. ### Select Input

```
    const CITIES = ['Alexandria','Milano','Bucharest'];
    <Pick config={{ name:"a", type:"select", choices:CITIES }} />
    <Pick config={{ name:"b", type:"select", choices:CITIES, multiple:true }} />
```

06. ### Checkbox Input

```
    <Pick config={{ name:"a", type:"checkbox", choices:CITIES }} />
    <Pick config={{ name:"b", type:"checkbox", choices:CITIES, multiple:true }} />
```

07. ### Radio Input

```
    <Pick config={{ name:"a", type:"radio", choices:CITIES }} />
```

08. ### File Input

The `allowed` prop could `string` and also could be an `array` and it is not case-sensitive, also the file input in pick has a special prop of `size` and each of `min`, `max` and `base` has to be set explicitly.

These are the size units to be used: `B`,`KB`,`'MB`,`GB`,`TB` and `PB` with respect to the machine's binary prefix base `BI`: Binary (1024 units) and `SI` (1000 units), by default the `BI` is set as default as it is the most commonly used, and to update it, set the `base` in the `size` prop.

```
    <Pick config={{ name:"a", type:"file", allowed:'PNG', size:{max:'14 MB', min:'7 MB', base:'SI'} }} />
    <Pick config={{ name:"b", type:"file", allowed:['PNG', 'jpeg], size:{min:'7 MB', max:'14 MB'}, multiple:true }} />
```

## Text

The `Text` handler component manages all text inputs and this includes, `text`, `textarea`, `password`, `hidden` and 2 more special inputs `copy` and `search`.

09. ### Hidden Input

The hidden input expects 2 props to be set in order to work properly, the `name` and `initial` props.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Text config={{ type:"hidden", name:"a", initial:"ab" }} />
    </Form>
```

10. ### Copy Input

The copy input expects 2 props to be set in order to work properly, its an un-controlled input and it shows a read-only text input with a button that copies the input's value on click.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Text config={{ type:"copy", name:"message", value:"Hello, World!" }} />
    </Form>
```

11. ### Password Input

The password input expects `disabled`, `name`, `placeholder`, `regex`, `readOnly`, `required` props to be set.
If the the `regex` is not provided the input will be valid of it has a value.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Text config={{ type:"password", name:"password1" }} />
        <Text config={{ type:"password", name:"password2" }} />
    </Form>
```

12. ### Text Area

The text-area component expects `disabled`, `min`, `max`, `name`, `placeholder`, `required`, `value`, `criteria`. The `criteria` depends what to count *characters* (default: `chars`) or *words*, so `min` and `max` are either words or characeters depending on the `criteria` set. This component renders the HTML text-area element with a positioned counter. By default the `min` is `150` and `max` is `300`.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Text config={{ type:"textarea", name:"message", criteria:"chars" }} />
        <Text config={{ type:"textarea", name:"message", criteria:"words" }} />
    </Form>
```

13. ### Search Input

The search input expects a `reference` to work properly, the `reference` should be created `useRef`. The components hide items that do not fall into the search query, as it searches the element `textContent`. Using the `scope` prop, the component will look for a certain `data-` attribute.

```
    <SearchInput
        reference={ reference }
        placeholder="search"
    />
    // or
    <SearchInput
        reference={ reference }
        scope="nationality"
        placeholder="search"
    />
    // here the search will look for the item with `data-nationality` attribute.
```

14. ### Text Input

The text component expects `disabled`, `name`, `placeholder`, `regex`, `readOnly`, `required`, `initial` props, all except `name` prop are optional. The `initial` value may not be valid, at this case the component will show both, the initial value and the error message.

```
    <Text config={{ name:"username" }} />
    // or
    <Text config={{ name:"username", initial:"schemer" }} />
    // or
    <Text config={{ name:"username", initial:"schemer", regex:/^[a-zA-Z0-9_]{3,}$/ }} />
```

## Time

15. ### Day Input
16. ### Month Input

Both of day and month inputs are built using the `Pick` component, so they could have all of it forms, by setiing the `style` prop or `checkbox` (for multiple selection), `radio` or `style`. Please check the [Pick](#pick) section for more explanation.

17. ### Date Input

The date input expects `from`, `initial`, `max`, `min`, `multiple`, `name`, `required`, `to` props to be set. The `from` and `to` props shoudl be string formatted *d/m/yyyy*, by default the `from` is set to the date of and `to` is set to the next `14th of December`.

The date input has 3 buttons, previous, calendar and next. The calendar button shows the selection of there, previous and next update the toggles the month accordingly.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Time config={{ type:"date", name:"vacation" }} />
    </Form>
```

18. ### Time Input

The time input expects `name`, `hour`, `minute`, `period`, `required`, and `system` to work properly. The time input shows a 12-system or 24-system clock, the system is set to `12` by default.

These props `hour`, `minute` and `period` ar used to set an inital value for the input.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Time config={{ name:"take-off" }} />
    </Form>

    // or
    
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Time config={{ name:"take-off", system:24 }} />
    </Form>
```