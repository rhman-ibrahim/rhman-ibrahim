[![Tools](https://skillicons.dev/icons?i=js,vite,react)](https://skillicons.dev)

# Fields

A JavaScript, React (Vite) components library which provides a styled form with functional buttons and multiple input components.

---

01. [Form](#form)
    - [Submit Button](#submit-button)
    - [Reset Button](#reset-button)
02. [Fields](#fields)
    01. [Number Field](#number)
        01. [Float Input](#float-input)
        02. [Integer Input](#integer-input)
    02. [Pick Field](#pick)
        01. [File Input](#file-input)
        02. [Select Input](#select-input)
        03. [Checkbox Input](#checkbox-input)
        04. [Radio Input](#radio-input)
    03. [Text Field](#time)
        01. [Hidden Input](#hidden-input)
        02. [Copy Input](#copy-input)
        03. [Text Area](#text-area)
        14. [Password Input](#password-input)
        05. [Search Input](#search-input)
        06. [Text Input](#text-input)
    04. [Time Field](#time)
        01. [Day Input](#day-input)
        02. [Month Input](#month-input)
        03. [Date Input](#date-input)
        04. [Time Input](#time-input)

---

## Form

The Form component expects `onSubmit` (function), `children` (inputs) and `resetButton` (boolean: optional) props to be set in order to work properly. The Form component is a context provider created using `createContext`, and it provides the reset functionality to its `children`.

- ### Submit Button

In order to display the form's submit button the submit function has to be provided through `onSubmit` prop.
The Form component will handle form data collecting, here insde the `handleSubmit` function, the `formData` parameter is an object of form input names as keys, and their values as values.

```
    const handleSubmit = formData => {
        console.log(formData)
    }

    <Form onSubmit={ handleSubmit }>
        ...
    </Form>
```

- ### Reset Button

To use the reset functionality set the `resetButton` boolean prop to true, and by double-clicking the reset button all values will be reset to their defaults (initial values set during the form creation).

```
    const handleSubmit = formData => {
        console.log(formData)
    }

    <Form onSubmit={ handleSubmit } resetButton>
        ...
    </Form>

    // or

    <Form onSubmit={ handleSubmit } resetButton={ true }>
        ...
    </Form>
```
---

## Fields

The input components created are `16`, they categorized under 4 categories, `Number`, `Pick`, `Text` and `Time`. This helps in reducing the number of exports from 16 to 4.

Each field component handles setting the default values for each input component if not provided; as  setting `required` to `true`, and `multiple` to `false` by default.

|Prop|Description|
|--|--|
|`type`|The type of input, a string value that decides which input is the default in a swtich/case statement in the field, its value depends on the field component.|
|`initial`|The starter value of the input, its type depends on the input nature.|
|`required`|A boolean value states if the input must have a value or not (optional), the default value of it is `true`.|
|`multiple`|A boolean value states if the input accepts more than a single value, the default value of it is `false`.|
|`min`|The lowest accepted value for an input for a single input value, or the minimum number of values accepted for a multiple value input, default value is `2`.|
|`max`|The highest accepted value for an input for a single input value, or the maximum number of values accepted for a multiple value input, default value is `3`.|

---

### Number

The `NumberField` expects `type`: float or integer (default), `name`, `placeholder`, `initial`, `min`: 2 (default), `max`: 3 (default), `step`, `required`, `min` and `max` props to be set. The `NumberField` component groups `NumberInput`, and `StepperInput`, it works with inetegers and floats using sort of validators: regular expressions, minimum and maximum.

- The `StepperInput` adds increment and decrement buttons to the input, in order to use it set a number value to the `set` prop.

- For `step` and `initial` the value is 1 for both with integer type and 1.1 for both with float type. The `min` and `max` are 2 and 3 respectively.

01. #### Float Input

```
    <Form onSubmit={ handleSubmit } resetButton>
        <NumberField config={{ name:"a", type:"float", initial:11.11, min:7.7, max:12.14 }} />
    </Form>

    // Using the stepper input: a readOnly input, the buttons are used to update the value.

    <Form onSubmit={ handleSubmit } resetButton>
        <NumberField config={{ name:"b", type:"float", initial:11.11, min:7.7, max:12.14, setp:1.1 }} />
    </Form>
```

02. #### Integer Input

```
    <Form onSubmit={ handleSubmit } resetButton>
        <NumberField config={{ name:"c", type:"integer", initial:11, min:7, max:12 }} />
    </Form>

    // Using the stepper input: a readOnly input, the buttons are used to update the value.

    <Form onSubmit={ handleSubmit } resetButton>
        <NumberField config={{ name:"d", type:"integer", initial:11, min:7, max:12, setp:1 }} />
    </Form>
```

---

### Pick

The `PickField` expects `name`, `choices`, `headings` to be set in order to work properly. The `PickField` component gathers `select`, `checkbox`, `radio` and `file` inputs.

The list of available values to choose from is defined by 2 values `choices` and `headings`, each has a different use, as `choices` is the actual values list and `headings` is the representation; by default `headings` is set to `choices`, this could be useful when working with multiple lanuages.

```
const CITIES = ['Alexandria','Milano','Bucharest'];
<Form onSubmit={ (formData) => console.log( formData ) } resetButton>
    <PickField config={{choices:CITIES, name:'city'}} />
</Form>
// to show values in Arabic language
const CITIES_ARABIC = ["الإسكندرية", "ميلانو", "بوخارست"];
<Form onSubmit={ (formData) => console.log( formData ) } resetButton>
    <PickField config={{choices:CITIES, name:'city', headings:CITIES_ARABIC}} />
</Form>
```

03. #### File Input

The `allowed` prop could `string` and also could be an `array` and it is not case-sensitive, also the file input in pick has a special prop of `size` and each of `min`, `max` and `base` has to be set explicitly.

These are the size units to be used: `B`,`KB`,`'MB`,`GB`,`TB` and `PB` with respect to the machine's binary prefix base `BI`: Binary (1024 units) and `SI` (1000 units), by default the `BI` is set as default as it is the most commonly used, and to update it, set the `base` in the `size` prop.

```
    <Pick config={{ name:"a", type:"file", allowed:'PNG', size:{max:'14 MB', min:'7 MB', base:'SI'} }} />
    <Pick config={{ name:"b", type:"file", allowed:['PNG', 'jpeg], size:{min:'7 MB', max:'14 MB'}, multiple:true }} />
```

04. #### Select Input

```
    const CITIES = ['Alexandria','Milano','Bucharest'];
    <Pick config={{ name:"a", type:"select", choices:CITIES }} />
    <Pick config={{ name:"b", type:"select", choices:CITIES, multiple:true }} />
```

05. #### Checkbox Input

```
    <Pick config={{ name:"a", type:"checkbox", choices:CITIES }} />
    <Pick config={{ name:"b", type:"checkbox", choices:CITIES, multiple:true }} />
```

06. #### Radio Input

```
    <Pick config={{ name:"a", type:"radio", choices:CITIES }} />
```

---

### Text

The `TextField` component gathers `text`, `textarea`, `password`, `hidden`, `copy` and `search`.

07. #### Hidden Input

The hidden input expects 2 props to be set in order to work properly, the `name` and `initial` props.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Text config={{ type:"hidden", name:"a", initial:"ab" }} />
    </Form>
```

08. #### Copy Input

The copy input expects 2 props to be set in order to work properly, its an un-controlled input and it shows a read-only text input with a button that copies the input's value on click.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Text config={{ type:"copy", name:"message", value:"Hello, World!" }} />
    </Form>
```

09. #### Text Area

The text-area component expects `disabled`, `min`, `max`, `name`, `placeholder`, `required`, `value`, `criteria`. The `criteria` depends what to count *characters* (default: `chars`) or *words*, so `min` and `max` are either words or characeters depending on the `criteria` set. This component renders the HTML text-area element with a positioned counter. By default the `min` is `150` and `max` is `300`.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Text config={{ type:"textarea", name:"message", criteria:"chars" }} />
        <Text config={{ type:"textarea", name:"message", criteria:"words" }} />
    </Form>
```

10. #### Password Input

The password input expects `disabled`, `name`, `placeholder`, `regex`, `readOnly`, `required` props to be set.
If the the `regex` is not provided the input will be valid of it has a value.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Text config={{ type:"password", name:"password1" }} />
        <Text config={{ type:"password", name:"password2" }} />
    </Form>
```

11. #### Search Input

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

12. #### Text Input

The text component expects `disabled`, `name`, `placeholder`, `regex`, `readOnly`, `required`, `initial` props, all except `name` prop are optional. The `initial` value may not be valid, at this case the component will show both, the initial value and the error message.

```
    <Text config={{ name:"username" }} />
    // or
    <Text config={{ name:"username", initial:"schemer" }} />
    // or
    <Text config={{ name:"username", initial:"schemer", regex:/^[a-zA-Z0-9_]{3,}$/ }} />
```

---

### Time

13. #### Day Input
14. #### Month Input

Both of day and month inputs are built using the `PickField` component, so they could have all of it forms, by setiing the `style` prop or `checkbox` (for multiple selection), `radio` or `style`. Please check the [Pick](#pick) section for more explanation.

15. #### Date Input

The date input expects `from`, `initial`, `max`, `min`, `multiple`, `name`, `required`, `to` props to be set. The `from` and `to` props shoudl be string formatted *d/m/yyyy*, by default the `from` is set to the date of and `to` is set to the next `14th of December`.

The date input has 3 buttons, previous, calendar and next. The calendar button shows the selection of there, previous and next update the toggles the month accordingly.

```
    <Form onSubmit={ (formData) => console.log( formData ) }>
        <Time config={{ type:"date", name:"vacation" }} />
    </Form>
```

16. #### Time Input

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