[comment]: # (Refer to this site for further details - https://www.gatsbyjs.com/plugins/gatsby-plugin-image/)

# Responsive Images and High Performance: gatsby-plugin-image
## Gatsby Plugin Layer
Gatsby's plugin layer encompasses a vast plugin ecosystem that makes implementing Node.js packages using Gatsby API quick and efficient. Gatsby plugins come in a wide array of varieties, including: 
1. **Inegrations or "Source Plugins":** these plugins pull data into Gatsby's GraphQL layer and make it available to query from other React components. 
2. **Progressive Image Handling:** for working with static and dynamic images 
3. **Analytic Library Integrations:** like Google Analytics, Segment, Hotjar, etc. 
4. **Performance Enhancements for CSS Libraries:** pre-parsing for CSS stylesheets rendered from Sass, styled-components, emotion, etc. 
5. **And a lot of other functionality:** like SEO, caching, sitemaps, RSS Feeds, etc.  

Gatsby comes with a vast plugin ecosystem that makes implementing Node.js packages using Gatsby API quick and efficient. One particular use case for Gatsby Plugins is handling and managing responsive images.

## The Original vs The New
Gatsby Image refers to the original Gatsby component that works with Gatsby's GraphQL query layer to easily generate optimized images. It is built around using `gatsby-plugin-sharp` to handle image transformations. With the focus of UI/UX playing an important role in SEO scores and Search Engine Page Rank, serving responsive images has become a requirement for most developers. In the past if you wanted to work with static images they had to be imported into Gatsby's GraphQL Layer, now however, `gatsby-plugin-image` makes working with images - whether as static components or as dynamic components using the GraphQL Layer - a breeze. Refer to the following use cases: 
1. If the image comes from a remote source, then you'll want to do all image handling through the GraphQL Layer 
2. If the image is part of a collection, like the cover of a blog post, working with the GraphQL Layer is easier now with `gatsby-plugin-image`
3. If the image is a status page illustration, the image of a section or something only lasting a short time on screen, then handling that image as a static component with inline styles is the recommended method



