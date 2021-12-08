[comment]: # (Brainstorming ideas for blog articles) 
[comment]: # (Images will not be rendered in Markdown this is just to give reference to the proposed image) 

# Design Tools for Rapid Prototyping 
## Figma and Design Assets
There are a number of advantages to be gained by effectively prototyping/wireframing in front-end software development. Prototyping your design and functionality can be a vital tool in ensuring that feedback is gathered early and often, which helps to build better products faster. Rapid prototyping allows for a visual to make sure all development/teams or other parties are all on the same page. Having the ability to catch problems, pain-points, points of interest, etc, before the development process takes place is important in ensuring a cost and time efficient development cycle.

The Rapid Prototyping Feedback Loop:
1. *Build what you're testing*
2. *Test it on users, internal teams, or small focus groups* 
3. *Adjust design/functional elements to reflect feedback* 
4. *Repeat the process.* 

One such tool for rapid prototyping is [Figma](https://www.figma.com/). Figma is a digital design and prototyping tool. It is a UI/UX design tool that can be used to create websites, apps, or smaller user interface components that can be integrated into other projects. Figma's collaborative cloud features make it a great tool for working with small and large teams, that require real-time input during the design and development process. Figma contains a few unique features that make prototyping really efficient: 
* **Built in Commenting:** Comments can be made on any design element or design space. Team members can be tagged, comments can be marked as resolved, and they can be integrated into third party business communication platforms like Slack. 
* **Embedded CSS Styles:** Figma components and design elements have auto-generated CSS properties, which aid in integrating figma designs into front-end projects extremely quick and easy. 
* **Version Control:** Version history ensures that updates can be made to designs without the fear of revising changes. It's similar to Github version control as older design sketches can be quickly reverted to or altered to fit design needs. 
* **Cloud-based Collaboration:** Small teams and large teams can easily collaborate on design elements in real time. Whether designs need to be approved by the end-user or internally, figma design files can be accessed online through the cloud or worked on from a desktop/workstation locally. 
* **Components:** Similar to other UI/UX tools, Figma allows for components to live at the heart of your designs. Easily exportable and editable, components ensure that the appropriate design elements are grouped together. The ability to edit certain elements at the individual level or components as a whole makes design changes quick and efficient. 
* **Constraints:** Components can be constrained to a particular predefined style or can be detached to allow full customization. The ability to copy components and design elements from other figma files and embed them in new projects puts re-usability at the forefront of design in Figma. 
* **Libraries:** You can share and update collections of components across projects. 
* **Community Files and Figma Plugins:** Figma has a wide variety of plugins, templates and other user-generated content available for use in it's Figma Community Hub. Similar to forking repositories in Github, you can easily incorporate other community members designs into your own projects.

![figma-workflow](https://res.cloudinary.com/dzmc7doja/image/upload/v1637623092/blogsite-content/blogarticle3-figmaprototyping/figma-workflow.webp)

## Collaboration 
When working with small or large teams it is important to effectively communicate design specifications and collaborate on design decisions. When working in a solo capacity it is important to communicate layout, style, and branding choices to the end-user as often as possible. Figma was built from the ground-up to make sharing designs and cross-platform collaboration an integral part of the platform. Every Figma Design file has a "Share" button that allows you to send design assets and grant permissions for viewing and editing the design file. 
 
![figma-share](https://res.cloudinary.com/dzmc7doja/image/upload/v1638299684/blogsite-content/blogarticle3-figmaprototyping/figma-share.png)

Co-editing through figma is also extremely viable because of it's cross-platform compatibility. Not only does figma function as a stand-alone desktop application, it also works as a web application that allows authorized users to view, edit, comment and design from any device/operating system. 

## CSS Integration 
The "Inspect" tab in Figma, provides CSS snippets that can be utilized in front-end stylesheets. CSS properties in Figma are auto generated as you edit design files. Depending on how you utilize components and elements in Figma, these CSS snippets can make certain design aspects (i.e. borders, box-shadows, gradients, font-families, etc.) much easier to import into your code. Figma also offers several options for its auto generated snippets: Swift for iOS, CSS for web, and XML for Android.

![figma-inspect](https://res.cloudinary.com/dzmc7doja/image/upload/v1638341317/blogsite-content/blogarticle3-figmaprototyping/figma-inspect.png)

## Components and Design Practices
Figma allows designers to create components - which are essentially reusable elements that help create and manage consistent designs across projects. You can create components from any layer or object you've created. These could be buttons, icons, layouts, etc. There are two aspects to a component: 

1. A **Main Component** defines the properties of the Component 
2. An **Instance** is a copy of the Component you can reuse in designs. Instances are linked to the main component and receive any updates made to the *Main Component* 

You can create components to use within a single file. Or, you can use the Team Library to share components and Styles across files and projects. There are a number of different design paradigms that can be employed during the design part of the development life-cycle. Figma **[Docs](https://help.figma.com/hc/en-us)** goes into detail about suitable practices for working with design elements in app. In order to maintain a fast workflow, there are a couple key design practices for structuring figma components that you should implement immediately:

#### ↘️ Clear Naming Conventions and Consistent File Naming
Use clear naming conventions and frames to organize components - this makes it easy to find and reuse components in the asset panel, swap out related components, and increases usability. Use naming convents that provide context about the function and state of the component. 

```
EXAMPLE - FORWARD SLASH NAMING

* Input/Field/Text - Active
* Input/Field/Text - Default 
* Input/Field/Text - Disabled
* Input/Field/Text - Feedback 
* Input/Field/Text - Filled 
* Input/Field/Text - View Only
```

Keep re-usability at the foreground of your design practices in Figma is made easy by using *Frame Containers*. These are useful in showing relationships across grouped elements on a particular page. Having your design files organized in this manner makes your design development files modular and potentially applicable to other design projects. Frames are also integral in creating interactions (i.e. creating gifs and animated renders), which allow for visual use-case scenarios of product designs.

![figma](https://res.cloudinary.com/dzmc7doja/image/upload/v1638811726/blogsite-content/blogarticle3-figmaprototyping/figma-frames.png)

#### ↘️ Using Components to Control Variation 
Figma allows a wide array of customization in how you control variation among master components and instances. There is a lot of detail in the Figma **[Docs](https://help.figma.com/hc/en-us/articles/360038662654-Guide-to-Components-in-Figma)**, however an important concept to note is when to use variations verses individually crafted components. It's best to use variants when dealing with multiple versions of similar components that share the same properties -- such as state, size, color, toggle state, etc. 

![figma-variants](https://res.cloudinary.com/dzmc7doja/image/upload/v1638813481/blogsite-content/blogarticle3-figmaprototyping/figma-variants.png)

## Libraries 
Components and Styles can be shared to your team via the Team Library. Team Library allows you to access all saved styles across all the team files and projects - which ultimately improves efficiency and maintains consistency. 


## Community Files

## References
* Career Foundry: [Rapid Prototyping](https://careerfoundry.com/en/blog/ux-design/rapid-prototyping-guide/) 
