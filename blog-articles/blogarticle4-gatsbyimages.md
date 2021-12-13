[comment]: # (Refer to this site for further details - https://www.gatsbyjs.com/plugins/gatsby-plugin-image/)

# Responsive Images and High Performance: gatsby-plugin-image
## Gatsby Plugin Layer
Gatsby's plugin layer makes implementing Node.js packages using the Gatsby API quick and efficient. Gatsby's plugins allow for a wide array of functionality, such as: 
1. **Integrations or "Source Plugins":** these plugins pull data into Gatsby's GraphQL layer and make it available to query from other React components. 
2. **Progressive Image Handling:** for working with static and dynamic images 
3. **Analytic Library Integrations:** like Google Analytics, Segment, Hotjar, etc. 
4. **Performance Enhancements for CSS Libraries:** pre-parsing for CSS stylesheets rendered from Sass, styled-components, emotion, etc. 
5. **And a lot of other functionality:** like SEO, caching, sitemaps, RSS Feeds, etc.  

Gatsby comes with a vast plugin ecosystem that makes implementing Node.js packages using Gatsby API quick and efficient. One particular use case for Gatsby Plugins is handling and managing responsive images.

![gatsby-plugin](https://res.cloudinary.com/dzmc7doja/image/upload/v1639295870/blogsite-content/blogarticle4-gatsbyimage/graphql-datalayer.png)

## Image Handling in Gatsby 
Gatsby Image refers to the original Gatsby component that works with Gatsby's GraphQL query layer to easily generate optimized images. It is built around using `gatsby-plugin-sharp` to handle image transformations. With the focus of UI/UX playing an important role in SEO scores and Search Engine Page Rank, serving responsive images has become a requirement for most developers. In the past if you wanted to work with static images they had to be imported into Gatsby's GraphQL Layer, now however, `gatsby-plugin-image` makes working with images - whether as static components or as dynamic components using the GraphQL Layer - a breeze. Refer to the following use cases: 
1. If the image comes from a remote source, then you'll want to do all image handling through the GraphQL Layer 
2. If the image is part of a collection, like the cover of a blog post, working with the GraphQL Layer is easier now with `gatsby-plugin-image`
3. If the image is a status page illustration, the image of a section or something only lasting a short time on screen, then handling that image as a static component with inline styles is the recommended method

### Inline Image Handling
If you are using an image that will be the same each time a component is used, such as a log or front page hero image, you can use the `StaticImage` component. The image can be a local file in your project directory or an image hosted on a remote server. Any remote images are downloaded and resized at build time. 

```javascript
// Example of using a StaticImage component in an example .jsx file
import { StaticImage } from "gatsby-plugin-image" 

export function MaterialDesign() {
  return (
  <StaticImage 
    src="https://res.cloudinary.com/dzmc7doja/image/upload/v1631255646/portfolio-site/material-design-grey.jpg" 
    alt="MaterialBackground-Grey"
    className="material-design"
    layout="constrained"
  />
  )
}
```

### GraphQL Configuration for Image Handling 
If you need to have dynamic images (i.e. they are hosted on a cloud server or being pulled from a CMS) you can load them via GraphQL and display them using the `GatsbyImage` component. Plugins in Gatsby will often be used in tandem with each other to provide enhanced function and use, here are a number of plugins that work with `gatsby-plugin-image`: 
* `gatsby-source-filesytem` - a plugin for sourcing data into your Gatsby web-application from your local filesystem 
* `gatsby-plugin-sharp` - a plugin that exposes several image processing functions built on the **[Sharp Image Processing Library](https://github.com/lovell/sharp)**
* `gatsby-transform-sharp` - a plugin used to manipulate images using GraphQL queries 

```javascript
// src/gatsby-config.js
{
  resolve: `gatsby-source-filesystem`,
  options: {
    path: `${__dirname}/src/images`,
    name: 'images',
  },
  `gatsby-plugin-sharp`,
  `gatsby-transformer-sharp`,
  `gatsby-plugin-image`,
},
```

`gatsby-plugin-image`, and the above plugins, can be added to your **gatsby-config.js** file to provide three distinctive options for rendered responsive images: 

```javascript
// example of GraphQL page query 
export const pageQuery = graphql`
  query {
    image: file(relativePath: { eq: "image.jpg" }) {
      childImageSharp {
          gatsbyImageData(
            quality: 90
            width: 200
            layout: CONSTRAINED
          )
        }
      }
    }
  }
`
```

1. Images with fixed width - this option should be used when a specific image size is needed across all device types (`FIXED`)
2. Images that stretch across their fluid parent container - this option makes the image dependent upon it's parent element container size, which effectively sets a min-width size to that of the container width (`FULL_WIDTH`)
3. Images that stretch across their container but are limited to a max-width - this option allows for responsive images to adjust their size up until a certain point regardless of the parent element container (`CONSTRAINED`)

Aside from image types `gatsby-plugin-image` also allows you to set fallback options for rendered images using the *Sharp* image processing API. 
1. `BLURRED`: (default) a blurred image encoded as a base64 data URI
2. `TRACED_SVG`: a low resolution traced SVG of the rendered image 
3. `DOMINANT_COLOR`: a solid color, calculated from the dominant color of the image 
4. `NONE`: no placeholder






