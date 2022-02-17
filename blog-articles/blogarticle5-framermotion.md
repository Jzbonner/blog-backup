[comment]: # (react animation library blog article - mention and link github/webdevelopment-essentials/js/framer-motion notes)

# Modern Animations with `framer-motion`
Web animation can be used to attract attention, encourage better engagement, and communicate clearly and effecively. Web animation should be smooth, meaningful and support the visitor's journey. CSS and JavaScript are the building blocks to web animation, however recently, animation libraries have attempted to make working with animations easier and geared towards rapid prototyping.  

## Framer Motion 
[Framer Motion](https://www.framer.com/motion/) is a production ready animation library for React. It utilizes the power of the [Framer](https://www.framer.com/) prototyping tool and is fully open source. The advantages of Framer Motion include: 
1. It uses server-side rendering 
2. It has CSS variable support
3. You can easily unmount animations 
4. It has built in accessibility options

### The `motion` component
Is a React Component built-into the `framer-motion` library. It will primarily be used to handle animations for HTML and SVG elements on the front end. The `motion` component is DOM optimized for 60fps animations and gesture support. Using the `motion` component and allows you to:<br /><br /> 
📌 Declaratively or imperatively animate components <br />
📌 Animate throughout React trees via variants <br />
📌 Respond to gestures with animations <br />
📌 Add drag, pan, hover and tap gestures 

Standard HTML elements can easily be converted to framer-motion elements by appending the `motion` keyword. For example when working with HTML `div` elements you can convert it to a motion component by changing it to `<motion.div></motion.div>`. You will then have access to the `animate` property that can be used to create simple animations and transitions or more customized and complex animation sequences.  

### The `animate` property 
For simple animations (i.e. changing the vertical or horizontal position, changing the opacity, or changing the scale of an element) you can set values directly on the `animate` prop.

```javascript
<motion.div animate={{ opacity: 0.8 }}>
  <img src="some-image"/>
</motion.div>
```
You can customize the animation property by utilizing the transition property on motion elements. By default, Motion will create an appropriate animation based on the types of value being animated. Physical properties are typically animated using react spring's physic engine and other animations with the tween composition engine. These transitions can be catered to your needs by setting a specific transition value, i.e.: 

```javascript
<motion.div 
  animate={{ x: 50 }}
  transition={{ ease: "easeOut", duration: 2 }}
/>
```

When a component mounts it automatically animates the values declared in the `animate` property, if they're different different from those defined in `style` or `initial`. You can however set the `initial` prop to `false` to use the value in `animate` as the component's mounted state to disable mount animations. This method is also applicable for server-side rendering.

Values in `animate` can also be set as a series of keyframes, which will animate through each value in sequence. Keyframes in framer motion are similar to that in CSS, however there syntax is array based instead of using `from` and `to` pairs. Keyframe animations will start with the first value in the array and iterate through the remaining indexed values in sequence. The transition property does allow for you to set custom timing values for all sequenced keyframes, refer to the example below: 

```javascript 
<motion.div 
  initial={{x: 10}}
  animate={{x: [null, 50, 100]}} // null is used to maintain the initial motion property as a starting point
  transition={{duration: 2, times: [0, 0.5, 1]}}
/>
```

### Variants 
Inline animation properties are useful for simple animation sequences but at times you may need to employ more complex sequencing or embedd a number of animations based on a user event. If this is the case then `variants` will help you achieve this. **Variants** are sets of predefined target objects and are passed into motion components via the `variants` prop. Variants can be referred to by label, wherever you set an animation target. 

```javascript 
const variants = {
    hidden: {opacity: 0, x: -100},
    visible: {opacity: 1, x: 0},
}

<motion.div 
  initial="hidden"
  animate="visible"
  variants={variants}
/>
```

Variants also allow for `propagation`. Essentially, if a motion component has children elements then variants will flow down through the component heirarchy. These changes in variant will flow down untila child component defines its own `animate` property. Refer to the following example: 

```javascript
const list = {
    hidden: {opacity: 0},
    visible: {opacity: 1},
}

const items = {
    hidden: {opacity: 0, x: -100},
    visible: {opacity: 1, x: 0},
}

return (
<motion.ul 
  initial="hidden"
  animate="visible"
  variants={list}
>
  <motion.li variants={item}>
  <motion.li variants={item}>
  <motion.li variants={item}>
</motion.ul>
)
```

Inline framer motion animations declared using the `animate` property are executed simultaneously. However when using `variants` in tandem with the `transition` property you gain access to extra `transition` props such as `when`, `delayChildren`, `before/afterChildren` and `staggerChildren`, which let's parents orchestrate the execution of child animations. Refer to the example below: 

```javascript 
const list = {
  visible: {
      opacity: 1, 
      transition: {
          when: "beforeChildren",
          staggerChildren: 0.3,
      },
  },
  hidden: {
      opacity: 0,
      transition: {
          when: "afterChildren",
      },
  },
}
```

Typically in React-based environments you may have to `map()` through an array to create a new group of rendered components. The animations for these rendered components can be still be controlled via the use of **dynamic variants**. Each variant can be defined as a function that resolves when a variant is accessed. These variant functions are defined in a single argument, which can be set in a component's `custom` prop. 

```javascript
const variants = {
    visible: i => ({
        opacity: 1, 
        transition: {
            delay: i * 0.3,
        }
    }),
    hidden: {
        opacity: 0,
    }
}

return items.map((item, i) => (
  <motion.li
    custom={i}
    animate="visible"
    variants={variants}
  />
))
```

### Component Animation Controls 
Declarative animations are will work for most use case scenarios but at times a higher level of complexity is required to create sequenced or event driven animations. For these cases you can use the `useAnimation()` react hook to create a set of imperative **Animation Controls** with a `start` and `stop` method. These controls can then be passed to one or more motion components via the `animate` prop. Animations can be started with the `start` method, which either accepts a `TargetandTransition` or if the component it's provided to has a variants property set, a variant label. The `start` method returns a promise, so it can be used to sequence animations using `await` and `then`. Refer to the code snippet below: 

```javascript 
const menuControls = useAnimation() 
const itemControls = useAnimation()

const sequence = async() => {
    await menuControls.start({ x: 0 })
    return await itemControls.start({ opacity: 0 })
}
```

### Layout Animations 
A motion component can automatically animate between different layouts that occur as result of a re-render by setting the `layout` prop to true. 

```javascript 
<motion.div layout />
```

Any layout change will be animated, for example: 
* Reordering a list 
* A style set on the component itself, for example change in `width` or `position` 
* A change in the parent's layout 
* Or any other chaneg in the component's layout

In the example below you can see how the `data-is-on` property is used in tandem with the useState hook to trigger a layout animation once the component is re-rendered. 

```javascript 
//the code below can be used to animate a switch via framer-motion layout property and the useState react hook
//styles.css 
html,
body {
  min-height: 100vh;
  padding: 0;
  margin: 0;
}

* {
  box-sizing: border-box;
}

body {
  background: linear-gradient(250deg, #7b2ff7, #f107a3);
  background-repeat: no-repeat;
  display: flex;
  justify-content: center;
  align-items: center;
}

.App {
  font-family: sans-serif;
  text-align: center;
}

.switch {
  width: 160px;
  height: 100px;
  background-color: rgba(255, 255, 255, 0.4);
  display: flex;
  justify-content: flex-start;
  border-radius: 50px;
  padding: 10px;
  cursor: pointer;
}

.switch[data-isOn="true"] {
  justify-content: flex-end;
}

.handle {
  width: 80px;
  height: 80px;
  background-color: white;
  border-radius: 40px;
}

// app.js
import React from "react";
import { useState } from "react";
import { motion } from "framer-motion";
import "./styles.css";

const spring = {
  type: "spring",
  stiffness: 700,
  damping: 30
};

export default function App() {
  const [isOn, setIsOn] = useState(false);

  const toggleSwitch = () => setIsOn(!isOn);

  return (
    <div className="switch" data-isOn={isOn} onClick={toggleSwitch}>
      <motion.div className="handle" layout transition={spring} />
    </div>
  );
}
```
