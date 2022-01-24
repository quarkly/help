---
id: day8
title: Day 8. Components from elements
sidebar_label: Day 8. Components from elements
---


### Why do I need components from elements on the page?

You can create a component using any primitive or group of primitives. One of the main advantages is the ability to duplicate this component within your site pages. If you change the component style or content on one of the pages, you can apply those changes to all the other component copies that are placed in the project. This is also a very good way to make site-wide components, such as the header and footer. 

So a component can also be a header, a button, or a link with certain styles. They simplify and speed up design creation because they contain ready-made styles and content. In addition, components can be nested in other components.

### Turning a card into a component

**Convert to Component**<br/>
As an example, let's create a component from the previously created card. To do this, select the Box primitive holding `CTRL` or `⌘` for MacOS and `right-click` and select *Create new Component* and enter a name for the new component, for example: *Card*. Done! The first component is created!<br/>

![Convert to Component](/scr/day8-convert-to-component.png)

### Duplicating a card

Now the Card is in the Components section, and you can add it anywhere on the page. Let's place the second Card next to the first one as an example:<br/>

![Duplicating a card](/scr/day8-duplicate-card.png)

### Setting styles for the variant (Override)

1. Set styles for one of the cards
   You can also change the style of the card. Add indentation and set the indent 16px: <br/>

   ![Setting styles card](/scr/day8-setting-styles-card.png)

   As you can see, the changes were applied correctly.

### Make all cards like the selected option (send to the master)

1. *Push All to Master* or *Push to Master*
  There are some real advantages here. Select the modified Card and `right-click`. In this interface, you have 5 new items:
  
  ![Push to Master](/scr/day8-push-all-master.png)

- First, select *Push to Master* and use it to send changes to all copies of the Card component in the project. If you remember, you previously set a value for only one copy of the Card component.
  After applying *Push to Master*, the changes (margin) were applied to all copies of the Card component in the project.
- *Push All to Master* does the same thing, except that it sends changes not only to the main subcomponent but also to all nested subcomponents.

### Reset variant changes to master

- You can also undo changes made on a particular copy using *Reset Overrides*. This will undo the changes you made, and reset to the Card component's Master version. 
- *Reset All Overrides* does the same for all subcomponents.

### Convert the component back to a set of primitives (Detach)

- If you want to convert a component back to a set of primitives, i.e. return everything to the way it was before you created the component, you can choose *Detach*.

### And more

1. **Components from Components** <br/>
You can create components from other components and in doing so build complex components.

2. **Component code** <br/>
You can open and edit the code of components that you have created. To do this, select *Edit code* in the context menu.

3. **Replace component code** <br/>
Sometimes it's necessary to replace one component with another in all copies of the project. To do this, create a new component, copy its code, and paste it into an old component. By saving the changes, you get a new version of the component in the place of the old one. 

---