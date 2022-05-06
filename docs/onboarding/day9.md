---
id: day9
title: Day 9. Project Theme
sidebar_label: Day 9. Project Theme
---
import YouTube from "../../src/components/YouTube";


### Why do I need the project theme?

When creating projects we often use a limited set of styles of text, colors, backgrounds, and other things. This may be due to the design system, brand, or simply personal preferences. We added a theme for that — a set of variables that can be used to design the page elements. These variables can be edited and they will change wherever they were applied in the project.

### Default theme

<YouTube videoId="fyLLNYVNG30" /> <br/> 


When you create a new project, you create a default theme with specific text styles, colors, backgrounds, shadows, transitions, transforms, filters, and breakpoints.<br/>
You can use them for your project, edit, delete, and move them.


### Adding a variable to a theme

To add a new value, click the `+` icon next to the category you want to add.
After that, enter your value name and the desired value, for example, if it's a color, enter the color code.

![Add new theme](/scr/day9-add-new-theme.png)

### Specify the button background with a variable from the theme

Let's change the button background with the theme by creating a variable in the Background Style category with the name "button" and giving it the red color code (#ff0000).<br/>
We've created a variable and it was saved automatically. Now select the button and set the background property to the value from the theme:

![Button theme](/scr/day9-button-theme.png)

### Changing the variable value

To change the value, click on it and the variable settings will open. As an example, let's change the font size in headline1 and set it to **42px**. <br/>

![Button theme](/scr/day9-headline-edit-theme.png) 

then set this value for the card title: <br/> 

![Font card](/scr/day9-headline-font-card.png)

### Removing a value

To delete an unnecessary variable, right-click on it and choose *Delete*. 

### Duplicating a value

To duplicate a variable, right-click on it and choose *Duplicate*. 


### Theme in blocks and templates

All ready-made blocks and templates are based on variables from the theme. This way you can change theme values to quickly edit default blocks or templates.

---