---
id: day6
title: Day 6. Hover Effects
sidebar_label: Day 6. Hover Effects
---

import OnboardingTutorialHoverState from '/src/svg/onboarding-tutorial-hover-state.svg';

import OnboardingTutorialBackgroundPosition from '/src/svg/onboarding-tutorial-background-position.svg';

import OnboardingTutorialCodePreview from '/src/svg/onboarding-tutorial-code-preview.svg';

import OnboardingTutorialTransitionFilled from '/src/svg/onboarding-tutorial-transition-filled.svg';

### Change the card background

1. **Hover state** <br/>
   With the Hover effect, you can change the state of the element, for example, add tips, make smooth transitions, transforms, rotations, zoom, shift, etc. that will be displayed when you mouse over the element.
   <OnboardingTutorialHoverState />

2. **Change the Background position** <br/>
   Select the previously created Box and go to the hover tab.
   Now you can change any CSS property that will be applied to the Box when hovering over it. To see how it works, let's change, for example, the Background-position and set the values: 100% 100%. Screenshot:
   <OnboardingTutorialBackgroundPosition />

3. **Go to Preview** <br/>
   To check how Hover works, go to the Preview mode by clicking on the "eye" icon <OnboardingTutorialCodePreview /> in the upper left corner of the screen.
   
   The Preview can also be opened by pressing `Ctrl` + `P` or `⌘ (Cmd)` + `P`. In this mode, if you mouse over the Box, you'll notice that this effect works correctly. In this mode, you can also see how the page will look to your visitors.

### Change the button background color

1.  You can also set hover effects for other elements. Choose the Button primitive, go to the hover tab, set Background, and choose the color-orange `#FF7C22` color.
   
   ![Hover button](/scr/day6-hover-button.png)<br/>

:::note
You can also check how this property works in the *Preview mode*. 
:::


### Change transition

The CSS property transition affects the transition state between the two states of the element (e.g. default and hover).

Transition properties:
- property — specifies which style will be affected by the transition;
- duration — defines the animation time;
- timing-function — animation speed;
- delay — the waiting time before starting the transition.

1. **Set the background Transition** <br/>
   This all sounds very complicated, but in reality it's not. As an example, let's set the following values of the Box where we changed the Hover.<br/>
   For the default state.
   <OnboardingTutorialTransitionFilled /><br/>

2. **Set the transition button** <br/>
   Set the same value for the button, but set the property to background-color.
   Now in the Preview mode, you can see that the transition between states is smoother.<br/>

   ![Transition background-color](/scr/day6-background-color.png)

### There are other states that can be influenced

Apart from the Hover state, there are others like Focus, Active, and Disabled. Let's have a look at them:

- **The Focus state** defines the style for the element that gets the focus.
- **The Active state** defines the style for the active link. The link becomes active when you click on it.
- **The Disabled state** is used to apply the style to locked form elements. These elements can't be the focus, be clicked, or be activated, and you can't type in the text fields.

---