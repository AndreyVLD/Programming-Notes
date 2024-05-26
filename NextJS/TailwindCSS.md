# Tailwind CSS
Tailwind CSS is designed to write CSS by using `class=` without leaving your `HTML` code.
In case of `Nextjs` `class=` becomes `className="css_rules_and_styles"`. 

## Installation
**ATTENTION**: You need to be inside your `hosting` directory if you work with `Firebase`.
To install Tailwind CSS you need to run the following commands:
```sh
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```
## Configuration
`init` command from above will generate 2 files: 
  - `tailwind.config.js`
  - `postcss.config.js`

Inside `tailwind.config.js` in the `content:` section you must add the path for the `.tsx` files that will use the Tailwind CSS.
For example for an `app` routing the path should be: `./app/**/*.{js,ts,jsx,tsx,mdx}`.

## Importing styles
In the `app` directory you will need to create `global.css` file where you will add the **Tailwind CSS directives**. These directives will be injected into a **Global Stylesheet** that will be used by the entire application.
In `app/globals.css:`
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
**IMPORTANT**: If you move your styles (`global.css` and others) in another directory than `app` you also need to include that path in the `content:`. Something like this
```Javascript
content: ['./app/**/*.{js,ts,jsx,tsx}',
          './styles/**/*.{css,scss,sass}']
```

And inside `layout.tsx` at the `app` level directory this file should be imported.
``` JavaScript
import './globals.css'
```
## Using classes
To define specific style for each React Component, add the `className=` attribute to the HTML you want to change. Here you can use special `Tailwind CSS` instruction to define better style.

## Deployment with Firebase
You need to be careful about 2 things:
- The correct path inside `tailwind.config.js` in the `content`. This should point to the `app` directory.
- When you install Tailwind CSS you are inside your `hosting` directory and not the root since this is the root of the Next.js web application.
  
**DISCLAIMER**: Emulators are really inconsistent when building Tailwind. 
- For best results try running `next build` and `next start` to see the frontend. And `firebase deploy` to test the whole system instead of using the emulators.
- <del> It appears that running `next build` and after that starting the emulators fixes some problems.</del>
- If we do not run `next build` before starting the emulators (potentially deleting the previous build from `firebase deploy`) it seems to work consistently.
- Works best if we run  `firebase emulators:start` from the `hosting` directory.

## Extracting Tailwind CSS into classes
To extract `Tailwind CSS` from the inline into a different, modular and reusable classes, we can remove it from within the `HTML` go into `global.css`.
In `global.css` you can create your class by using `@apply` and `@layer` directives to create a custom `CSS` class.

Example:
```CSS
@layer components {
  .btn {
    @apply bg-blue-500 hover:bg-blue-600 active:bg-blue-700 focus:outline-none focus:ring focus:ring-blue-300 rounded-full text-white px-4;
  }
}
```
Here you can use the `btn` class as a usual `CSS` class inside your HTML.

**However,** this is ill-advised. Better to keep the `Tailwind CSS` inside the `HTML` as good practice.
**Uses**: 
- **Highly Reusable Components**: When you have components like buttons, form inputs, and other elements reused throughout your site with very consistent styling, extracting those styles using `@apply` can improve maintainability.
- **Framework Integration**: If you're using a framework like React, Vue, etc., the component-based architecture naturally encourages styles to live alongside component logic.

## Tailwind CSS classes and components

Here we will discuss and detail different classes and components like: grids, flexbox, colors, background and meta-components like hover, focus etc.

In this section `*` will be used as a placeholder for numbers.

### Grid
- to set a `div`/section to be a grid: `grid`
- to set the number of cols in a gird: `grid-cols-*`
- to set the distance between all the rows and columns: `gap-*`
  - Use the `gap-x-*` and `gap-y-*` utilities to change the gap between columns and rows independently.

#### Grid-span
- Use the `col-span-*` utilities to make an element span n columns.
- Use the `col-start-*` and `col-end-*` utilities to make an element start or end at the nth grid line.
- Use the `grid-rows-*` utilities to create grids with n equally sized rows.
- Use the `row-span-*` utilities to make an element span n rows.
- Use the `row-start-*` and `row-end-*` utilities to make an element start or end at the nth grid line.

### Flexbox
- Use the `basis-*` utilities to set the initial size of flex items.
  - It can be either a fraction on how much space it occupies or number of pixels
  - `basis-4` or `basis-1/4`(this means this flex element occupies one 4th of the space)

#### Flexbox Direction
- Use `flex-row` to position flex items horizontally in the same direction as text. (horizontally)
- Use `flex-row-reverse` to position flex items horizontally in the opposite direction. (still horizontally, but now we start from the end).
- Use `flex-col` to position flex items vertically.
- Use `flex-col-reverse` to position flex items vertically in the opposite direction.

#### Flex wrap
How to behave if we have more items than there is space.
- Use `flex-nowrap` to prevent flex items from wrapping, causing inflexible items to overflow the container if necessary.
- Use `flex-wrap` to allow flex items to wrap.
- Use `flex-wrap-reverse` to wrap flex items in the reverse direction.

#### Flex
- Use `flex-initial` to allow a flex item to shrink but not grow, taking into account its initial size.
- Use `flex-1` to allow a flex item to grow and shrink as needed, ignoring its initial size.
- Use `flex-auto` to allow a flex item to grow and shrink, taking into account its initial size.
- Use `flex-none` to prevent a flex item from growing or shrinking.

#### Flex Grow
- Use `grow` to allow a flex item to grow to fill any available space.
- Use `grow-0` to prevent a flex item from growing.

#### Flex Shrink
- Use `shrink` to allow a flex item to shrink if needed.
- Use `shrink-0` to prevent a flex item from shrinking.

#### Order
- Use the `order-*` utilities to render flex and grid items in a different order than they appear in the DOM.
  - You can use negative values, prefix the class name with a dash to convert it to a negative value.

### Padding
- To control the padding use `p-*`

#### Alignment:

**IMPORTANT**:
- justify = main axis
- align = cross axis
- place = both axis

**IMPORTANT**:
- content = whole content is placed
- items = items are placed inside the cells
- self = one item is placed inside the cell

**THIS GOES FOR ONLY CONTAINERS (BOTH GRID AND FLEXBOX)**
- Use **justify content** to align items along the main axis.
  - `justify-center` to center the items.
  - `justify-start` to align items to the start. Basically, putting them at the beginning of the container.
  - `justify-end` to align items to the end. Basically, putting them at the end of the container.
  - `justify-between` to distribute items evenly. The first item is at the start, the last item is at the end, and the rest of the items are evenly distributed.
  - `justify-around` to distribute items evenly with equal space around them. `justify-evenly` can also do this.
  - `justify-stratch` to stretch the items to fill space on the main axis.


- Use **justify items** to align ALL items inside a **container cell** along main axis (basically to align all the items with respect to the cell they are located in).
  - `justify-items-center` to center the items at the start of their cells.
  - `justify-items-end` to align items to the end of their cells.
  - `justify-items-center` to center the items in their cells.
  - `justify-items-stretch` to stretch the items to fill the cells.


- Use **align content** to align items along the cross axis. This is used for multi-row grids and flexbox.
  - `content-start`  to pack rows in a container against the start of the cross axis.
  - `content-center` to pack rows in a container in the center of the cross axis.
  - `content-end` to pack rows in a container against the end of the cross axis.
  - `content-between`  to distribute rows in a container such that there is an equal amount of space between each line.
  - `content-around` to distribute rows in a container such that there is an equal amount of space around each line.
  - `content-evenly` similar to `content-around` but the space is distributed evenly.
  - `content-stretch` to stretch the rows, **across the cross-axis**, to fill the container.


- Use **align items** to align items along the cross axis. 
  - Syntax is `items-*`.


- Use `place-content` to align items along both axes.
  - `place-items` and `place-self` appear here also.

**THIS GOES FOR THE ITEM INSIDE THE CONTAINER**

Everything here aligns the items inside the flexbox/grid cell with respect to the flexbox/grid cell.

- Use `justify-self-*` to align a single item along the inline axis. It works exactly like `justify-items-*` but for a single item.
- Use `align-self-*` to align a single item along the cross axis. It works exactly like `align-items-*` but for a single item.
- Use `place-self` to align a single item along both axes.
