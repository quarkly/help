---
id: day13
title: Day 13. React.js Components
sidebar_label: Day 13. React.js Components
---

### About React.js

Custom React.js components extend the builder capabilities. They simplify and speed up design creation because they contain ready-made styles, content, and logics. In addition, components can be nested in other components.

### About components
You can import components into other components: primitives, catalog components, custom components, and packages from npm. Here you can program any logic, fetch data, and send it via API.<br/>
You can make subcomponents so that they can be selected and styled on the panel. In Quarkly, you can also display the props of a component on the right panel as controls.

### How to create a custom component

![How to create a custom component](/scr/day13-components-general.png)

On the Adding panel in the Components section, you can find all your components:

- added from elements to the page
- added from the catalog
- custom components

To create a code component, click on the "+" icon. A window will open for you to enter the component name. After entering the name, a component with default code is created. You can edit it if needed.


### How to import primitives

You need to add an import line at the beginning of the file. For example, this is how you can 
```
import Box and Text:
import { Box, Text } from "@quarkly/widgets";
```

### How to import a custom React.js component

This way you can nest a previously created component, such as MyComponent, inside another component:
```
import MyComponent from "./MyComponent";
```

### Importing a module from NPM

You can also import any package from [npm](https://www.npmjs.com/), such as react-particles-js:
```
import Particles from "react-particles-js";
```

### Connected dependencies

You can add the version you want in your project settings under Dependencies:

![Connected dependencies](/scr/day13-connected-dependencies.jpeg)


### Displaying props on the right panel as controls
To add/configure component parameters, create the propInfo object where the properties are the names of the parameters and the values are their descriptions. For example:

```
propInfo: {
  someProp parameter: {
    title: 'Property Title',
    description: {
      en: 'Property Description',
    },
    control: 'select',
    variants: ['opt1', 'opt2'],
    multiply: true,
    category: 'Main',
    weight: 1
  }
}
```

Read more about what [types of controls](http://developers.quarkly.io/components/properties/propinfo-object) you can use.

### How to make subcomponents selectable and stylable (Overrides)
Overrides allow you to select nested subcomponents on the layers, and change their styles and props in the builder or directly in the component code. To do this, follow the steps below:

1. Import the useOverrides hook from the @quarkly/components library
2. Create an Override List
3. Use Overrides in a Component
4. Export a Component with Overrides

Read more about how to [work with overrides](http://developers.quarkly.io/components/overrides/overview).


You can find full info about how to work with components in the [guide for developers](https://developers.quarkly.io/).


**Congratulations!** You've covered all Quarkly basics.

---