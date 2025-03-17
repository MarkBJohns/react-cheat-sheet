# React Helmet

`Helmet` is a package that allows you to dynamically change the \<head> tag of your **index.html** file the same way you're dynamically changing the \<body> tag. The simplest way to set this up is to create a \<Helmet /> component for each of the pages, and put them together. So if we have an "About Us" page, we can wrap all of the body content into a component:

```jsx
// src/components/AboutUs/Content

import { Hero, aboutUsPage } from "@/components/Hero";
import { FAQs, aboutUsFAQ } from "@/components/FAQs";

const Content = () => {
    return (
        <main>
            <Hero page={aboutUsHero} />
            <FAQs page={aboutUsFAQ} />
        </main>
    )
}

export default Content;
```

And then create a dedicated Helmet component for the webpage's head:

```jsx
// src/components/AboutUs/AboutUsHelmet

import { Helmet } from "react-helmet-async";

const AboutUsHelmet = () => {
    return (
        <Helmet>
            <title>Icon Golf Cart of Tampa Bay | About Us</title>
            <meta name="description" content="Learn about the company and so on and on etc" />
            <link rel="canonical" href="https://icon-golfcarts.com/about-us" />
        </Helmet>
    )
}

export default AboutUsHelmet;
```

Our component for the webpage will then include both the content, and the Helmet:

```jsx
// src/components/AboutUs

import { Content } from "../Content";
import { AboutUsHelmet } from "../AboutUsHelmet";

const AboutUs = () => {
    return (
        <>
          <AboutUsHelmet />
          <Content />
        </>
    )
}

export default AboutUs;
```

To write the Helmet, you don't need to understand any React, outside of knowing how to set up and import a component. The content of the Helmet will be exactly the same as it would be in a standard html file.

The standard practice will be:

```jsx
import { Helmet } from "react-helmet-async";

const PageNameHelmet = () => {
    return (
        <Helmet>
            {/* write exactly what you would in an html file */}
        </Helmet>
    )
}

export default PageNameHelmet;
```

And I'll just plug it into the final page from there.
