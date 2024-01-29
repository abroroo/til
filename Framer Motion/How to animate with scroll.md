## How to animate objects with scrolling data of the page 

How to make two divs move on the x-axis while user scrolls vertically 

I did something like this in my portfolio website:

![Scroll Animation Demo](https://github.com/abroroo/til/blob/main/Framer%20Motion/scrollDemo.gif?raw=true)

I wanted to share how to do it with framer motion because it's very easy

You basically need these two methods `useScroll` and `useTransform`

> `useScroll` is used to create scroll-linked animations, like progress indicators and parallax effects.
>
> `useScroll` returns four motion values:
>  - `scrollX/Y`: The absolute scroll position, in pixels.
>  - `scrollXProgress/YProgress`: The scroll position between the defined offsets, as a value between 0 and 1.


In typescript it looks something like this: 

First you need to reference to the element, once this element is visibale on the page, it should trigger animation of the two divs we want to move on the x-axis 

Then get vertical scroll data with `useScroll`

```typescript
   // enterance of this element to the view should trigger animation of two divs on the x-axis
  const experRef = useRef<HTMLElement>(null)

   // dynamically returns value of vertical scroll in real time Ex: 553 pixels from the top of the page
  const { scrollY } = useScroll();

```




```typescript

  const [screenWidth, setScreenWidth] = useState(0);
  const [screenHeight, setScreenHeight] = useState(0);
  const skillsStart = experRef.current?.offsetTop || 0;
  const skillsEnd = skillsStart + (experRef.current?.offsetHeight || 0);

  useEffect(() => {
    if (typeof window !== "undefined") {
      setScreenWidth(window.innerWidth);
      setScreenHeight(window.innerHeight);
    }
  }, []);

```





```typescript
  const rocketX = useTransform(scrollY, [skillsStart, skillsEnd], [-screenWidth, screenWidth]);
  const rocketY = useTransform(scrollY, [skillsStart, skillsEnd], [screenHeight, -screenHeight]);


  const rocketX2 = useTransform(scrollY, [skillsStart, skillsEnd], [screenWidth, -screenWidth]);
  const rocketY2 = useTransform(scrollY, [skillsStart, skillsEnd], [-screenHeight, screenHeight]);

```






```jsx
<motion.p className='absolute top-2 left-0  bg-[#fff]' style={{ x:rocketX,  rotate: 0 }}>
  Javascript * Python * NodeJS * PostgreSQL
</motion.p>

<motion.p className='absolute left-20 top-[96px] bg-[#fff42d]' style={{ x: rocketX2,  rotate: 0, }}>
  ReactJS * NextJS * Typescript * MongoDB
</motion.p>

```
