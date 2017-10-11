# Web Animation Workshop 

## Essentials of CSS Animation w/ Val

- CSS animation is fundamental to the rest of what we'll be doing the rest of the day
- It can often be the simplest answer to get things done
- The thing about CSS animation is that we have a bunch of things that sound like they can do the same thing. There may be times you may have to say "we have to animate the transition to transform and translate..."

### CSS Transforms w/ Val

- Spoiler Alert: This doesn't make anything move.
- It allows you to modify the coordinate space of the CSS visual formatting space
- They are all in one property (i.e., `translate`, `rotate`, `scale`, `perspective`, etc.) and most importantly, **the order matters because it changes the end result**
- The `perspective` property requires a pixel
    - Lower numbers make the effect  more drastic it is
    - Higher numbers make it much flatter
    - Recommends 800px to 1000px as a starting point
    - It should generally be the first thing you define in a `transform`
    - You can also set it on the parent container and then manipulate the children separately

### CSS Transitions w/ Val

- Transitions are animations.
- The minimum you need for a transition:
    1. Point A
    2. Point B
    3. Duration
- Shows interesting technique of setting just transition time (with no properties defined i.e., `.box { transition: 1s }`) on the parent element to impact the rest of the children
    - Granted, this is a little dangerous from a performance perspective; but just interesting to note
- You can make the transitions asymmetrical by adding a second `transition` state
    - **Counter-intuitive point:** *The Point B transition is the one that executed first especially on things like hover because that state gets set immediately.*
- For better readability, use comma separated values

### CSS Animations w/ Val

- The minimum you need for an animation:
    1. `A named set of keyframes to assign
    2. `animation-name` - user designated name (which can pretty much be anything)
    3. `animation-duration` - the length of the animation
    - Optional
        1. `animation-delay` - how long the animation is delayed for
        2. `animation-iteration-count`: how many times the animation happens 
        3. `animation-direction`: which direction the animation goes
        4. `animation-fill-mode`: fills in the time outside the animation (at either end)
        5. `animation-timing-function`: this determines the cubic-bezier and takes the usual properties of `ease`, `ease-in-out`, etc.
- Why is this better than CSS Transitions?
    - You can define multiple stages of your animations
    - It seems to allow much more granularity with animations
    - You can have multiple `@keyframes`
- Tip: Remember that it is `@keyframes` and **NOT** `@keyframe`
- There is a shorthand to consider:
    - `animation: ${name} ${duration} ${delay} ${iteration-count} ${direction}`
        - **Pro Tip:** Even though there is no specific order required, at least start with the animation name. And decide on a convention with your team.
- You can define stages in your `@keyframes` with percentages and/or keywords.
    - **Pro Tip**: You can do floats with the percentages!
    - **Pro Tip**: It's best to pick one or the other for consistency (i.e., `from` == `0%` and `to` == `100%`)
    - Example:
        ```
        @keyframes move {
            0% { ... }
            10% { ... }
            100% { ... }
        }
        ```
- The default timing function transition in CSS animation is `ease` and not linear like everywhere else
    - **Pro Tip**: When you use ease, it's going to try and use it as a global ease. Instead, try setting `animation-timing-function: linear` on the global and then define specific timing functions for the various frames
- Handy properties you can animate but were probably not aware of...
    - `z-index`
    - `transform-origin`
    - `animation-timing-function`

### CSS Variables w/ Val

- AKA CSS Custom Properties
- Why they're a big deal...
    - They follow the CSS cascade (custom properties)
    - You can easily modify values with JavaScript
- Example
    ```
    transform: translate(calc(var(--mouse-x) * 1px - var(--radius)/2))
    ```
- This can make `@keyframes` much more dynamic because changing them after they're in your CSS file.
- **That means multiple elements can use the same keyframes but have DIFFERENT animations!!!!**

## Basics of TweenMax & TimelineMax w/ Sarah

### Introduction

- GreenSock is a company that makes TweenMax and TimelineMax. In other words, they are products but are still referenced as GreenSock as a whole in converstaion
- GSAP performs as well if not better than some native technologies
    - It's not that they're not leveraging native technologies
    - They are just doing it in clever ways and paying attention to exactly what they're animating
- Painting is one of the most expensive aspects of rendering, but GSAP's painting is really really low in comparison
- Visual benchmarks are important because it is a separate benchmark from straight up performance benchmarks like FPS
- Like it a lot because it helps a lot with workflow and cross-browser consistency
- The issue with CSS animations:
    - Sequencing animations is a manual process of delays and is not very sustainable
    - Adjusting timing of an animation is so critical to the workflow and this becomes very expensive
    - Basic coding workflow of having your animation be far from the element you're applying it to (i.e., scrolling down to your keyframe, then back up to the styles, then back down...)
- **Pro Tip**: Opacity and transform are the most performant and best bang for buck when it comes to animation on the web
- Killer workflow features:
    - Simple syntax
    - Timelines
    - Nested timelines
    - Draggable
    - And more (found in slides)
- Syntax
    - Think of the actions (i.e., `to`, `from`, etc.) as sentences
        - "Hey Tween[Max/Lite], grab this element and go ${action} ..."
    - `fromTo` is good at the beginning of an animation because when you need the animation to restart from a certain position
    - Stagger is amazing!!! For a cool example, check out this [SVG with Cycle Stagger CodePen by Sarah](https://codepen.io/sdras/pen/XmmjQb)
- Timeline
    - This is one of the primary features she loves
    - It makes things so easy to change things that would normally make you want to shoot yourself if you did it in raw CSS
    - **Pro Tip**: The industry standard for the timeline variable is `tl`
    - The primary difference between the two different Timelines is that TimelineMax allows you to loop while TimelineLite does not
    - You can nest timelines as well!
- **Pro Tip**: In order to avoid momentary display due to HTML/CSS rendering before JS does its thing, set the visibility to hidden on the animated elements to start (and then set back to visible with TweenMax/TweenLite)
- Percentage based transforms are cool! And unfortunately will never be part of the CSS animation spec, so it's a GreenSock specific thing!
- The animations are fully responsive
- **Pro Tip**: While you normally want to keep styles in CSS, this can become disjointed with team members because they don't know you need X styles for the animation. So Sarah recommends using the `TweenMax/TweeLite.set()` functionality to explicity associate the necessary styles directly with the animation to prevent any accidental code deletion!
- For frameworks, she wraps the animation in a component that only kicks off once the component is mounted. AWESOME!
- Animating Text
    - Split Text
        - A plugin that breaks text into characters, words, or lines and has no dependencies (not even TweenMax)
        - Support back to IE 8
        - **Big Plus:** Even though there are tons of open-source, it is what she recommends because it honors natural line breaks
- How would we turn a many element scene from day to night?
    - **Pro Tip:** Recommends HSLA for colors in animation

## Theory: Classic Animation Principles Worth Stealing

- "The 12 Principles of Animation" was created by Disney
    - They are related concepts to help your animation become more life-like or simply communicate more effectively
- The Principles We'll Cover Today
    - Timing & Spacing
    - Follow Through & Overlapping Action
    - Anticipation
    - Squash & Stretch
    - Staging
    - Arcs
    - Exaggeration

### Timing & Spacing

- It used to be just called "Timing," but nowadays it's more commonly referred as "Timing & Spacing"
- **Pro Tip:** If you only have room for one animation principle to remember, this is the one!
- The only way to get good at it though is to practice it
- Timing (aka `duration`): The amount of time it takes for an action to happen aka the duration
- Spacing (aka `easing`): The changes in speed over the uration of the action's timing
- The reason it matters is because:
    - It makes animated objects appear to obey the laws of physics
    - Establishes the mood, emotion and reaction
- Had an awesome example of triangles and circles communicating a narrative
- Even though cubic-bezier curves seem complicated, just remember that all you're doing is determining how fast something is going over a certain span of time. Definitely use the cubic-bezier tool for designing a custom one though!

### Follow Through & Overlapping Action

- Follow Through
    - Not everything comes to a stop at once
    - Helps give the impression that something is obeying the laws of physics
    - Different parts of the "body" move at different rates 
- Overlapping Action
    - Actions don't wait for the one before it to finish before starting
    - Movements tend to overlap in time

### Anticipation

- This is the reverse of follow through in that there is a little hesitation before the main movement
- Setting up, preparing or getting ready for the main movement
- Using opposite movement in order to draw attention to it and make it more weightier
- Very often used for exits 
- Often coupled with follow throughs

### Arcs

- Organic movements typically don't follow straight lines of motion
- Very hard to do in interfaces because the most efficient calculation computers can do is a straight-line action
- Fun thing to check out: Browsers implement different animations for downloading items

### Exaggeration

- The "truth" but more extreme
- Actions are made bigger and more drastic for greater effect and impact
- Great example of Mickey Mouse pulling this huge hammer out of his pocket which could not have possibly fit in his pocket, but it draws the correct attention and delivers the message clearly of what the animator wants you to focus on without being off putting

### Squash & Stretch

- Gives the illusion of weight and flexibility of an object
- Objects tend to change shape as they move depending on inertia and the elasticity of what they're made of
- Important to maintain the volume of the object
- Gives the illusion of the element being some natural material
- Cool example of a drippy hamburger menu on a site for Animal

### Staging

- It's classically defined as a way to make a scene clear, but this should already be our focus as UI designers / developers. 
- Instead, think of it more as directing the audience's attention, and making it clear what is of greatest importance in a scene
- Examples of..
    - Dark Sky app loading with the black circle being staged and then turned into the temperature when it's done loading
    - A Plus Icon rotating to the right to take your attention out into the menu that expands out after clicking it. Love this example!
- When motion design on the screen follows real life, it makes the experience that much better

## SVG Animation

## Memorable Quotes

> "Why does it work like this? I'm sure there's a reason, but I'm going to yell about it anyways." - Val Head

> "They don't pay me. I'm just a developer that found a tool I like." - Sarah Drasner on GreenSock

> "Animation cannot fix your bad design." - Val Head

## My Exercises

- [Dancing Robot CodePen](https://codepen.io/BenCodeZen/pen/ZXRMqG?editors=1100)
- [GreenSock Boxes](https://codepen.io/BenCodeZen/pen/MEXzGq?editors=0110)

## Presentation Notes

- Great use of multiple screen capture GIFs in a single slide in order to slow the differences between different browsers
- Great use of the zoom animation in order to make text more visible
- Phenomenal CodePen where she has the code for the animation appear as the relative animation happens which is great for context
- Hilarious use of GIF for "how I feel when I live code, but I'll do it anyways..."
- Great use of progressing through code by showing the manual way and then layering on the benefits with each iteration and how it solves X pain point
- The use of hover effect as "poking turtles" was cute

## Resources

- [WebAnimationWorkshops Resources Repo](https://github.com/WebAnimationWorkshops/workshop-resources)
---
- [CSS Transform - MDN Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)
- [Matrix Animation Tool by Eric Meyes](http://meyerweb.com/eric/tools/matrix/)
- [BounceJS](http://bouncejs.com/)
- [CSS Animation - MDN Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/animation)
- [Cubic Bezier Tool](http://cubic-bezier.com/#.17,.67,.83,.67)
---
- [GreenSock Ease Visualizer](https://greensock.com/ease-visualizer)
---
- [The Illusion of Life by Ollie Johnston](https://www.amazon.com/Illusion-Life-Disney-Animation/dp/0786860707)
- [The Animator's Suvival Kit by Richard Williams](https://www.amazon.com/Animators-Survival-Kit-Richard-Williams/dp/0571202284)
- [The 12 Principles of Animation Tumblr](http://the12principles.tumblr.com/)
- [The 10 Principles of Motion Design GIF](http://designtaxi.com/news/389419/Animator-Uses-GIF-To-Explain-The-10-Principles-Of-Motion-Design/)
- [Animated Triangles and Circle Narrative Example](https://www.youtube.com/watch?v=n9TWwG4SFWQ)