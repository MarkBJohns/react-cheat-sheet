# Nested Components

Remember our **sayHello()** function:

```js
const sayHello = () => console.log("Hello world");
```

We're creating a function, called **sayHello**, which executes another function, **console.log()**. Functions calling other functions is a common practice, and it's what React relies on, given that components are just fancy functions that create JSX elements.

Previously we showed unique page components: **\<HomePage />**, **\<AutoPage />**, **\<MarinePage />**, and so on. All of these are components, which each take in the **\<Hero />** component. But we can also add components to Hero, say, a **\<Navbar />**. Then let's say we want our cta elements to have specific styles and behaviors we wrap in a dedicated component, say **\<CTA>**. Once all those components are created, our Hero might look something like:

```jsx
import Navbar from "../Navbar/Navbar";
import Button from "../Button/Button";
import styles from "./Hero.module.scss";

const Hero = ({ page }) => {
    return (
        <header className={styles.header}>
            <Navbar />
            
            <h1 className={styles.heading}>
                {page.heading}
            </h1>
            
            <p className={styles.subheading}>
                {page.subheading}
            </p>
            
            <div className={styles.hero}>
                <img src={page.hero.src} alt={page.hero.alt} />
            </div>
            
            <CTA target={page.cta.target}>
                {page.cta.text}
            </CTA>
        </header>
    )
}

export default Hero;
```

Now when another component imports `Hero`, they're importing all the other components with it automatically. This helps you build standalone components that can be easily slotted into any other page section, and if there are any issues or revisions you want to make (such as adding, removing, or editing a Navbar link), you only have  to do it one time in the `Navbar.jsx` file, and it updates everywhere on the website.

## Mapping Components

Often you'll have components that are meant to be small cards or containers, and these are one of the places where React shines.

```js
const cardOne = {
    hero: {
        src: cardOneHero,
        alt: "SEO stuff"
    },
    title: "Card One",
    price: 100
}

const cardTwo = {
    hero: {
        src: cardTwoHero,
        alt: "SEO stuff"
    },
    title: "Card Two",
    price: 175
}

const cardThree = {
    hero: {
        src: cardThreeHero,
        alt: "SEO stuff"
    },
    title: "Card Three",
    price: 225
}

export { cardOne, cardTwo, cardThree };
```

```jsx
const Card = ({ hero, title, price }) => {
    return (
        <div className={styles.card}>
            <div className={styles.hero}>
                <img src={hero.src} alt={hero.alt} />
            </div>
            
            <h3 className={styles.title}> { title } </h3>
            
            <p className={styles.price}> ${ price } </p>
        </div>
    )
}

export default Card;
```

Our card is a small component we'll want to reuse over and over, so we can do something like:

```jsx
import { cardOne, cardTwo, cardThree } from "./content";
import Card from "./Card/Card";
import styles from "./CardContainer.module.scss";

const CardContainer = () => {
    return (
        <section className={styles.container}>
            <Card 
                hero={cardOne.hero} 
                title={cardOne.title}
                price={cardOne.price}
            />
            
            <Card 
                hero={cardTwo.hero} 
                title={cardTwo.title}
                price={cardTwo.price}
            />
            
            <Card 
                hero={cardThree.hero} 
                title={cardThree.title}
                price={cardThree.price}
            />
        </section>
    )
}

export default CardContainer;
```

This works, but it's messy, and the more cards you add, the harder it is to maintain. To get around this, we can revisit the **map()** method.

```js
const numbers = [1, 2, 3, 4, 5];

const quadruple = (nums) => nums.map(x => multiplyNumbers(x, 4));

quadruple(numbers);
// [4, 8, 12, 16, 20]
```

Remember how mapping works, you run a function on each item in an array, then return a new array with the result of each of those functions, and remember that components are themselves functions.

```js
const cards = [
    {
        hero: {
            src: cardOneHero,
            alt: "SEO stuff"
        },
        title: "Card One",
        price: 100
    },
    {
        hero: {
            src: cardTwoHero,
            alt: "SEO stuff"
        },
        title: "Card Two",
        price: 175
    },
    {
        hero: {
            src: cardThreeHero,
            alt: "SEO stuff"
        },
        title: "Card Three",
        price: 225
    }
];

export default cards;
```

Update the content file to export all the cards as an array, instead of as objects. This allows us to map the Card component onto each of our objects.

```jsx
import cards from "./content";
import Card from "./Card/Card";
import styles from "./CardContainer.module.scss";

const CardContainer = () => {
    return (
        <section className={styles.container}>
            {cards.map((card, id) => (
                <Card 
                    hero={card.hero} 
                    title={card.title}
                    price={card.price}
                    key={id} 
                />
            ))}
        </section>
    )
}

export default CardContainer;
```

Remember that the **map** function give you access to the index of the array if you want to use it. With React, it's best practice to always include a unique key for each component you make while mapping data, as this lets React better distinguish one component from another. We can do this by combining the standard index value that **map** give us, along with the standard **key** attribute that React gives us.

By combining your card data into an array, you get access to the **map** method, allowing you to make the list of cards as long as you want without ever having to go back and update `CardContainer.jsx`.
