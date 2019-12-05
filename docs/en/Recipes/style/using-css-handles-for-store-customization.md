---
title: Using CSS Handles for store customization
description: "CSS Handles are magic tools developed by VTEX IO to make it easier to customize components using CSS. Have a look at this recipe for more on how to identify and apply CSS Handles to your store, without the need for HTML CSS selectors"
date: "10/24/2019"
tags: ["customization", "css", "css-selectors", "css-handles", "layout"]
version: "0.x"
git: "https://github.com/vtex-apps/io-documentation/blob/master/docs/en/Recipes/style/using-css-handles-for-store-customization.md"
---

# Using CSS Handles for store customization

## Introduction 

CSS Handles is a **HTML elements identifier**. Therefore, it can be used to customize any of your store components by simply using CSS classes through the store theme's code. 

At the end of the day, CSS Handles are nothing more than your **store's layout building assistants**. Follow the step-by-step below and find out how to use them in a fast and simple way! 

## Step by step 

1. While you are viewing your workspace on your browser, add `?__inspect` at the end of the URL of the page, and press enter. For example, `https://yourworkspace--youraccount.myvtex.com?__inspect`. Note that it must be a development workspace, rather than a production one, and it must be under the domain `myvtex.com`.

2. Hover on the element you want to customize. It should display its available CSS handles in a box (the large names beginning with `.`), along with their respective CSS file names, and other information.

![css-handles-inspect](https://user-images.githubusercontent.com/5691711/70256857-ffdd8780-1767-11ea-936d-a98cbfc924c1.png)

3. In your store theme code, create a file inside the `css` folder, with name displayed below the desired handle (in the example above, `vtex.menu.css`).

3. In the new file, use one of the CSS handles listed and customize its properties. For example:

```css
/* vtex.menu.css */

.menuItem {  
    background: rgba(0, 0, 0, 0.2);
    margin: 5px;
    border-radius: 5px;
}
```

Once you app is linked and the changes duly saved, the new customization should immediately be reflected onto your workspace.  

![css handles customization applied to the menuItem](https://user-images.githubusercontent.com/5691711/70257811-d160ac00-1769-11ea-8434-67f71afc2056.png)

Note that the change was applied to all `menu-item` blocks. To apply changes to a single `menu-item` block or to a subsect of blocks, you should use the  `blockClass` prop.

1. In the `json` file where your block is declared, add the prop `blockClass` to the element you want to customize, with any name as a value.

For example:
```json
"menu-item#your-item": {
  "props": {
    ...,
    "blockClass": "header"
  },
  ...
}
```

After saving and updating your workspace, when you inspect the element it should display an additional CSS handle along with its default one, like this:

![css handles with block class](https://user-images.githubusercontent.com/5691711/70259211-7c726500-176c-11ea-9252-32b4aad76c12.png)

After that, you can use the class `.menuItem--header` to target specifically the elements that have this `blockClass`.

![specific menu items with css handles applied using blockClass](https://user-images.githubusercontent.com/5691711/70259424-e985fa80-176c-11ea-93e7-5c72770804f6.png)

<div class="alert alert-info">  
Our team is constantly working on developing CSS Handles for every possible store component. If however your are unable to find a CSS Handle for a component you wish to customize, share this scenario with us at <a href="https://github.com/vtex-apps/store-discussion">Store Discussion</a>.  
</div>

## Best practices

In order to standardize CSS customization and avoid any potential breakdown in layout, **we recommend store customization to be performed exclusively using CSS Handles**. 

However, it's common to come across store scenarios whose customization uses CSS Selectors. As the name implies, they are used to select elements for CSS customization according to the page HTML hierarchy. 

This customization practice by HTML hierarchy was mostly deprecated. It means that **only** the CSS Selectors listed below will continue to be allowed for your store customization:

- `:hover`   
- Link selectors, such as `:visited`, `:active` and `:focus`.   
- Every pseudo-element, such as  `::before`, `::after` and `::placeholder`. 
- `:nth-child(even)` and `:nth-child(odd)` 
- `:first-child` and `:last-child`
- Descendant combination element through space, such as `.{Element1} .{Element2}` 
- `[data-*]` 
- `:global(vtex-{AppName}-{AppVersion}-{ComponentName})`

**Any CSS Selectors not on this list, such as** `:nth-child(n)`**,** `foo > bar` **and** `[alt="bar"]`**, will no longer be accepted by Toolbelt during the [linking](https://vtex.io/docs/recipes/store/linking-an-app) of the store's theme with its local files.**

<div class="alert alert-warning">  
Bear in mind that any customization that uses CSS Selectors is dependent on a HTML structure that, when changed, can break the retailer's desired customization.<strong> Always opt to use CSS Handles</strong>. 
</div>
