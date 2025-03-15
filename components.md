# Basic Components

## Folder Layouts

In Node and React (which uses Node), you have access to an `import` keyword, which is what allows you to access everything in the app while still keeping your workspace compartmentalized. For each component, you'll want to create a folder. 

```csharp
src/
|-- components/
|   |-- ComponentName/
|      |-- ComponentName.jsx
|      |-- ComponentName.module.scss
|      |-- index.jsx
|      |-- content.js
|      |-- imgs/
|          |-- # component-related images
```

### ComponentName

The name of the folder should be the name of the component. Note that the naming convention in React is capitalizing the first letter of components, as well as maintaining the camelCase conventions for the rest of JavaScript.

### ComponentName.jsx

This is where the actual component is written. This is the file that most closely represents traditional HTML.

### ComponentName.module.scss

The styling for your components goes here. You can still write it like typical CSS, but by making it SASS, you can use variables and mixins from your sass folder, and by making it a module, you can make the styles in that file completely contained to just the specific component (no styling or class name conflicts).

### content.js

Components are designed to be reused, but with different images and text values. This is the file where you can create multiple JavaScript objects with all those varying values.

### imgs/

If you have images that are only relevant to this particular component, you can store them directly inside the component folder for ease of access and organization.

### index.jsx

This file exists purely to help facilitate importing the component down the line.

## Importing Internally

The perfect component to demonstrate this is a Hero component:

+ The Hero is reused in most, if not all pages
+ Each page will have different text and a different image
+ It's very simple and straightforward

Once you make your `Hero` folder, the first thing you'll want to set up is your `content.js` file. Our hero will have a title, subtitle, hero image, and call-to-action. If we know we'll have a home, auto, and marine page, we just create a home, auto, and marine object:

```js
import homeHero from "./imgs/homepage-hero.png";
import autoHero from "./imgs/auto-hero.png";
import marineHero from "./imgs/marine-hero.png";

const homePage = {
    heading: "Welcome to Website.com",
    subheading: "We sell cool stuff you should buy",
    hero: {
        src: homeHero,
        alt: "SEO stuff goes here"
    },
    cta: {
        text: "Learn More",
        target: "/products"
    }
}

const autoPage = {
    heading: "We do Car Stuff",
    subheading: "Car stuff is really neat",
    hero: {
        src: autoHero,
        alt: "SEO stuff goes here"
    },
    cta: {
        text: "Hit the road",
        target: "/contact-us"
    }
}

const marinePage = {
    heading: "We do Boat Stuff",
    subheading: "Boat stuff is really cool",
    hero: {
        src: marineHero,
        alt: "SEO stuff goes here"
    },
    cta: {
        text: "Brave the high seas",
        target: "/contact-us"
    }
}

export { homePage, autoPage, marinePage };
```

At the top of the page, we've taken our home, auto, and marine hero images from our `/imgs` folder and saved them as variables. Then we made an object for each of the pages, and finally, we `exported` all of our objects as one single object.

Once we have our content ready, we make the actual component in `Hero.jsx`:

```jsx
import { Link } from "react-router-dom";
// I'll explain this later, but this mostly replaces the <a> tag in React
import styles from "./Hero.module.scss";
// I'll explain this later, but it's how you style your component

const Hero = ({ page }) => {
    return (
        <header className={styles.header}>
            <h1 className={styles.heading}>
                {page.heading}
            </h1>
            
            <p className={styles.subheading}>
                {page.subheading}
            </p>
            
            <div className={styles.hero}>
                <img src={page.hero.src} alt={page.hero.alt} />
            </div>
            
            <Link to={page.cta.target}>
                {page.cta.text}
            </Link>
        </header>
    )
}

export default Hero;
```

Here, **page** represents the object from `content.js` that you want to use. So for the home page, you'd want to use the homePage object, the auto page, the autoPage object, and so on. In JSX (the part of the code that looks like HTML), anything placed in `{}` will execute JavaScript and display the result as text. So if you use the **marinePage** object as a parameter, then the **\<h1>** will say "We do Boat Stuff", because that's what **marinePage.heading** says.

Note the "default" at your exporting line. When you export data from your .js and .jsx files, you want to only export one thing. It's why we wrapped the `content.js` objects into a single object before exporting it. So if there's only one thing to export, we use "default" to make sure React knows exactly what it's supposed to extract from each file.

> I'll show you what to do about scss in person because it's really annoying to set up and I don't want to type it all up right now

Finally, the `index.jsx` is the final filter between your component folder and the rest of your workspace. Throughout the project, when you import data, you'll be importing from the folder itself, not a specific file, so the `index.jsx` file of each folder helps organize what you want to be accessible. For this Hero folder, we'll want to be able to access the content objects, as well as the Hero component:

```jsx
import { homePage, autoPage, marinePage } from "./content";
import Hero from "./Hero";

export { homePage, autoPage, marinePage, Hero };
```

## Importing Externally

Each webpage will be a component, which will be full of other components. Notably for this example, each page will have a Hero component. This is why we created the content objects, and why we wrote our Hero full of variables. We don't have to rewrite any code, and we don't even have to copy/paste anything, we can just call Hero like a function (because it technically is) with new parameters to make a completely new Hero section.

```jsx
// HomePage/HomePage.jsx

import styles from "./HomePage.module.scss";
import { Hero, homePage } from "../Hero";

const HomePage = () => {
    return (
        <main className={styles.homePage}>
            <Hero page={homePage} />
        </main>
    )
}

export default HomePage;
```

```jsx
// AutoPage/AutoPage.jsx

import styles from "./AutoPage.module.scss";
import { Hero, autoPage } from "../Hero";

const AutoPage = () => {
    return (
        <main className={styles.autoPage}>
            <Hero page={autoPage} />
        </main>
    )
}

export default AutoPage;
```

```jsx
// MarinePage/MarinePage.jsx

import styles from "./MarinePage.module.scss";
import { Hero, marinePage } from "../Hero";

const MarinePage = () => {
    return (
        <main className={styles.marinePage}>
            <Hero page={marinePage} />
        </main>
    )
}

export default MarinePage;
```

When we want to make our home page hero, we import the Hero component, and the homePage content. When we want to make our auto page hero, we import the Hero component and the autoPage object. Even though it took longer to make the Hero component than it would have to make it in HTML, we can now make as many Hero pages as we want, and all we need to do is upload another image and write another JavaScript object.

## Route Formatting

When importing, you'll want to write the path to the file or folder you're getting the content from:

> + **"/"**- starting the path with just a slash
>   + This begins the path at the `public` folder. You don't need to use the import keyword if you're using a public resource, you can just declare it directly:
>   ```jsx
>   const logo = "/logo.png";
>   ```
>
> + **"@/"** - starting the path with `@`
>   + This is a shortcut to go all the way back to the src folder, useful for if you're very deeply nested.
>   ```jsx
>   import { HomePage } from "@/components/Homepage";
>   ```
>
> + **"./"** - starting the path with a single period
>   + This starts the path in the same directory as the file you're importing into, you'll use this the most often when importing `content.js` files and SCSS modules
>   ```jsx
>   import styles from "./ComponentName.module.scss";
>   ```
>
> + **"../"** - starting the path with double periods
>   + This starts the path one step back from the current directory. This can be stacked to go backwards one folder at a time, but if there are too many steps, it's better to just use @ and start from the beginning
>   ```jsx
>   import Navbar from "../Navbar/Navbar";
>   ```
>

## File Types in Imports

You may have noticed that some import strings included file types at the end while others didn't. If you're importing from a JavaScript file, JSX file, or a folder (which doesn't even have a file type), you don't need to include a file type, because that's the default file type in React. If you want to import another file type, such as an image or stylesheet, you do need to include the file type in the import:

```jsx
import content from "./content"; // JavaScript file
import styles from "./ComponentName.module.scss"; // stylesheet
import Navbar from "../Navbar/Navbar"; // JSX file
import homeHero from "./imgs/homepage-hero.png"; // image file
```
