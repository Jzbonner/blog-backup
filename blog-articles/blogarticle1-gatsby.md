[comment]: # (Brainstorming ideas for blog articles) 
[comment]: # (Images will not be rendered in Markdown this is just to give reference to the proposed image) 

# Gatsby.js and MarkdownX
###  *Markdown "greater than sign" WordPress*

![cms](https://res.cloudinary.com/dzmc7doja/image/upload/c_scale,w_450/v1623739172/blogsite-content/blogarticle1-gatsby/cms.png) 

Content management is an important aspect of web development. Content management systems like WordPress, Drupal, and Joomla have been highly effective in providing document management, digital asset management, and record retention. However, with the ever changing landscape of front-end technologies and the rise of Headless CMS it has become more apparent that these legacy systems have their drawbacks. Certain enterprise environments still call for these heavy and resource intensive technologies, but recent trends have seen a shift towards lightweight-template based alternatives. 

Before diving head deep into WordPress alternatives like Pico and Grav or Headless CMS solutions like Strapi and GraphCMS, you may be able to take advantage of a local-file solution that provides lightweight rendering and is no more resource intensive than your front-end framework of choice - enter Gatsby.js and MarkdownX. 

### #Gatsby.js
There are a number of things that can be said regarding the ease of use of static site generators. Although not applicable to all websites/web applications, static site generators like Gatsby, provide speed, search engine optimization, and security right out the box. One of the central ideas of Gatsby is that HTML content is statically generated using React DOM server-side APIs. Said HTML content can then be enhanced with client-side JavaScript via the `ReactDOM.hydrate()` method, which allows for app-like features in Gatsby generated sites. 
    
Although technically just a static site generator, Gatsby.js - at its core, contains all the functionality needed to create data enabled web applications through a sourced filesystem or through sourced data providers (i.e. Headless CMSs, private APIs, or relational/non-relational databases). 

### #Filesystem and Markdown 
Gatsby's allows users to create file nodes directly from the filesystem, through the use of the `gastsby-source-filesystem` plugin. Adding the plugin to your `gatsby-config.js` and refreshing the Gatsby development environment will enable the GraphiQL viewer for your local-host development server.

*example of gatsby-config.js*
```javascript
module.exports = {
  siteMetadata: {
    title: `Your Site Name`,
  },
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `src`,
        path: `${__dirname}/src/`,
      },
    },
  ],
```

*GraphiQL Explorer*: `http://localhost:8000/___graphql`

Markdown is a lightweight markup language that you can use to add formatting elements to plaintext text documents. In the context of web development, Markdown can be used to make local content management an embedded service. MarkdownX (MDX) is a variation of the Markdown format that allows you to combine Markdown with JSX (a syntax extension to JavaScript). It combines the readability of Markdown with the expressivity of JSX. MDX is highly useful in content-driven sites: like interactive blogs, documentation sites for design systems, or dynamically extensive webpages that require quick run-times. 

*example of MarkdownX (.mdx)* 
```markdown
import { Chart } from '../components/chart'

# Here’s a chart

The chart is rendered inside our MDX document.

<Chart />
```

The benefits of MarkdownX in JSX environments includes: 
* Fast with no runtime compilation 
* Extensible 
* Element to React component mapping
* React component import/export
* Customizable layouts

### #Getting up and running with the Gatsby MDX Plugin
Depending on whether your starting a brand new Gatsby project or working on an existing development project the installation process will change slightly. The core plugins needed to integrate with markdownx and gatsby.js are `gatsby-source-filesystem` and `gatsby-plugin-mdx`. 

#### Gatsby Source Filesystem 
> is a Gatsby source plugin for sourcing data into your Gatsby application from your local filesystem. The plugin creates Files nodes from files. The various "transformer" plugins can transform File nodes into various other types of data. 

*Reference*: [Gatsby Source Filesystem](https://www.gatsbyjs.com/plugins/gatsby-source-filesystem/)

*Install gatsby-source-filesystem via Node Package Manager (npm)*: `npm install gatsby-source-filesystem`

#### Gatsby MDX Plugin 
> `gatsby-plugin-mdx` is the official integration for using MDX with Gatsby

*Reference*: [Gatsby MDX Plugin](https://www.gatsbyjs.com/plugins/gatsby-plugin-mdx/)
 
If you're starting a brand new Gatsby project there are a number of boiler-plate/starter-code templates that will help you get up and running with MarkdownX: 

*Gatsby-cli command for cloning the MDX starter repo* 
```shell
gatsby new my-mdx-starter https://github.com/gatsbyjs/gatsby-starter-mdx-basic
```
*Reference*: [Gatsby MarkdownX Starter](https://github.com/gatsbyjs/gatsby-starter-mdx-basic)

If you already have a working Gatsby development environment and decide to integrate MDX, you'll need to add MDX as dependencies: 

```shell
npm install gatsby-plugin-mdx @mdx-js/mdx @mdx-js/react 
``` 

After installing your dependencies to your Gatsby environment be sure to add those plugin modules to your `gatsby-config.js` 

```javascript
module.exports = {
  plugins: [
    // ....
    `gatsby-plugin-mdx`,
  ],
}
```
Be sure to restart the development environment by running `gatsby develop` to enable the plugin.  

### #MarkdownX, GraphQL, and Frontmatter 
Gatsby.js comes prepackaged with a query language known as GraphQL. GraphQL provides a complete and understandable description of the data in your API, which makes it easier to evolve APIs over time and enables powerful developer tools. 

> GraphQL queries access not just the properties of one resource but also smoothly follow references between them. While typical REST APIs require loading from multiple URLs, GraphQL APIs get all the data your app needs in a single request. Apps using GraphQL can be quick even on slow mobile network connections.

*Reference*: [GraphQL](https://graphql.org/)

In MarkdownX files you can include a set of key/value pairs that provide additional data for specific pages in the GraphQL data layer. That "additional data" is known as `frontmatter` and is denoted by triple dashes at the start and end of the block. 

```markdown
---
title: Example Frontmatter Title
example_boolean: true
---

# Markdown Content Here
```

After initializing an MDX file with frontmatter you can then use GraphQL to query for this data in your JSX files; or reference this frontmatter in the scope of your MarkdownX files. See examples below: 

*example of GraphQL query for frontmatter data* 
```graphql
query {
  allMdx {
    edges {
      node {
        frontmatter {
          title
          path
          date(formatString: "MMMM DD, YYYY")
        }
      }
    }
  }
}
```

*example of referencing frontmatter data in JSX blocks within the MDX file* 
```markdown
---
title: Example Title
author: Example Author
---

<h1>{props.pageContext.frontmatter.title}</h1>
<span>{props.pageContext.frontmatter.author}</span>

# Additional Markdown content here
```

### #Lastly, Importing JSX Components via MDX and Shortcodes
Extensibility, is what makes MarkdownX a compelling case for a local-data-filesystem. Although other headless CMS's provide you with a more intuitive GUI, MarkdownX allows you to use React based components directly in your MarkdownX files to add functionality such as data visualizations, call-to-action buttons and other UI/UX elements. You can either directly `import` these React components into the MDX file or use shortcodes via the `MDXProvider` to create globally available components that can be used throughout all of your MarkdownX files.

*Reference*: [MDXProvider](https://www.gatsbyjs.com/plugins/gatsby-plugin-mdx/#mdxprovider)

*example of using imports for components in MDX files*
```markdown
---
title: Importing Functionality via JSX Components
---

import { Underline } from "./src/styles/underline"

# Markdown Content Unstyled

<Underline>This statement would be underlined because of the imported JSX component</Underline>
```
* Note: If you would like to include frontmatter metadata and import components, the frontmatter needs to appear at the top of the file and then imports can follow.

*example of using shortcodes to create global components*
```javascript
/*The following code is what you might find in a layouts.js file in your Gatsby project*/
import React from "react"
import { MDXProvider } from "@mdx-js/react"
import { Underline } from "./src/styles"
import { Strikethrough } from "./src/styles"
import { Bold } from "./src/styles" 

const shortcodes = { Underline, Strikethrough, Bold }

export default function Layout({ children }) {
  return (
    <MDXProvider components={shortcodes}>{children}</MDXProvider>
    )
}
```
*exmaple of MarkdownX that uses globally available shortcode*
```markdown
---
title: Importing Functionality via JSX Components
---

# Markdown Content Unstyled

<Underline>This statement would be <Bold>underlined</Bold> because of the imported JSX component</Underline>
```

All MDX components passed into the `components` prop of the `MDXProvider` are then made available as shortcodes to all MDX documents that are nested in the project directory. Utilizing the `MDXProvider` component means that your layout-specific jsx file must be referenced in your `gatsby-config.js`. The `gatsby-plugin-mdx` plugin allows users to set a `defaultLayouts` module-export that references a key/value pair for the directory of the specified layout. You can also set `options.defaultLayouts.default` if you want to use a specific layout for any MDX files that don't adhere to the default `layout.js` file. 

*example gatsby-config.js that uses the defaultLayouts option in the `gatsby-plugin-mdx` module to define a layout specific markdownx style and a default markdownx style*
```javascript
// gatsby-config.js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `pages`,
        path: `${__dirname}/src/pages/`,
      },
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `posts`,
        path: `${__dirname}/src/posts/`,
      },
    },
    {
      resolve: "gatsby-plugin-page-creator",
      options: {
        path: `${__dirname}/src/posts`,
      },
    },
    {
      resolve: `gatsby-plugin-mdx`,
      options: {
        defaultLayouts: {
          posts: require.resolve("./src/components/posts-layout.js"),
          default: require.resolve("./src/components/layout.js"),
        },
      },
    },
  ],
}
```
*example of post-layouts.js for posts-specific markdownx files*
```javascript
import React from "react"
import { MDXProvider } from "@mdx-js/react"
import { Underline } from "./src/styles/Underline"
import { Bold } from "./src/styles/Bold" 

const shortcodes = { Underline, Bold }

export default function Layout({ children }) {
  return (
    <MDXProvider components={shortcodes}>{children}</MDXProvider>
    )
}
```
*example of layouts.js for default markdownx files*
```javascript
import React from "react"
import { MDXProvider } from "@mdx-js/react"
import { Strikethrough } from "./src/styles/Strikethrough"
import { Italic } from "./src/styles/Italic"

const shortcodes = { Strikethrough, Italic }

export default function Layout({ children }) {
  return (
    <MDXProvider components={shortcodes}>{children}</MDXProvider>
    )
}
```

The designation between layouts is applied based on the configuration of the `options` key in your `gatsby-source-filesystem` module-export.

### #Conclusion 
Utilizing MarkdownX in your Gatsby.js projects really caters to rapid website development. The ability to opt out of using a headless CMS and instead use a local-filesystem data source - with JSX functionality embedded - allows developers to create dynamically rendered webpages with extensibility, customization and blazingly fast load times. Take a look at the links below for a deeper dive into Gatsby.js and MarkdownX. 

#### **Important Links for Gatsby**
📌 Documentation for [mdx-js](https://github.com/mdx-js/mdx) <br/>
📌 Documentation for [Gatsby.js](https://www.gatsbyjs.com/docs/) <br/>
📌 Documentation for [GraphQL](https://www.gatsbyjs.com/docs/graphql/) <br/>
📌 Documentation for [Gatsby MDX Plugin](https://www.gatsbyjs.com/plugins/gatsby-plugin-mdx/) <br/>
📌 Documentation for [Gatsby  Markdown Syntax](https://www.gatsbyjs.com/docs/reference/markdown-syntax/) <br/>
