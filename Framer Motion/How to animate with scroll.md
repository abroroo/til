## How to animate objects in realtion to scoll of the page 

How to make two divs move on the x-axis with user scrolling data in real time

I did something like this in my portfolio website:

![Scroll Animation Demo](https://github.com/abroroo/til/blob/main/Framer%20Motion/scrollDemo.gif?raw=true)

I wanted to share how to do it with framer motion because it's very easy




```jsx
<motion.p className='absolute top-2 left-0  bg-[#fff]' style={{ x:rocketX,  rotate: 0 }}>
  Javascript * Python * NodeJS * PostgreSQL
</motion.p>

<motion.p className='absolute left-20 top-[96px] bg-[#fff42d]' style={{ x: rocketX2,  rotate: 0, }}>
  ReactJS * NextJS * Typescript * MongoDB
</motion.p>

```
