---
id: linkbox
title: LinkBox
sidebar_label: LinkBox
---

![The LinkBox Primitive on Page](/scr/primitives-linkbox.png)

The LinkBox primitive is used for:
- creating a link to other pages
- creating a link to parts within the current or another page (anchor link)
- creating a link to open files
- creating a link to write an email
- creating a link with a phone number

In the LinkBox properties, you can set the target address, the tab behavior when you click the link, the LinkBox behavior when transferring lines and when overflowing.

The difference between Link and LinkBox is that LinkBox is a container where other elements can be placed. These elements together will work as a link. 
For example, LinkBox is perfect for cards that link to another page.

##### Available props

| Prop name | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| :-------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| href      | Sets the address to go to when the link is clicked                                                                                                                                                                                                                                                                                                                                                                                                                |
| target    | You can define the window where the page opened by the link will be loaded: <br/>&emsp;\_self - loads the page into the current window;<br/>&emsp;\_blank - loads the page into a new browser window;<br/>&emsp;\_parent - loads the page into the frame parent. If there are no frames, this value works as \_self;<br/>&emsp;\_top - cancels all frames and loads the page in the full browser window. If there are no frames, this value works as \_self.<br/> |

---
