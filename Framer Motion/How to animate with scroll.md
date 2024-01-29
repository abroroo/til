## How to animate objects with scrolling data of the page 

How to make two divs move on the x-axis while user scrolls vertically 

I did something like this in my portfolio website:

![Scroll Animation Demo](https://github.com/abroroo/til/blob/main/Framer%20Motion/scrollDemo.gif?raw=true)

I wanted to share how to do it with framer motion because it's very easy

You basically need these two methods `useScroll` and `useTransform`

> `useScroll` returns four motion values:
>  - `scrollX/Y`: The absolute scroll position, in pixels.
>  - `scrollXProgress/YProgress`: The scroll position between the defined offsets, as a value between 0 and 1.


> `useTransform` helps to transform one range of values into another range of values.
> - `useTransform(valueToBeConverted, fromThisRange, toThisRange)`
> - Ex: `const visualValue = useTransform(temperature, [0, 100], [0, 1])`
> - - when `temperature` is 60 `visualValue` is 0.6 



### Now let's see how we can use these methods
- _Code Snippets are in Typescript_

First you need to reference to the element, once this element is visibale on the page, it should trigger animation of the two divs we want to move on the x-axis 

Then get vertical scroll data with `useScroll`

```typescript
   // enterance of this element to the view should trigger animation of two divs on the x-axis
  const experRef = useRef<HTMLElement>(null)

   // dynamically returns value of vertical scroll in real time Ex: 553 pixels from the top of the page
  const { scrollY } = useScroll();

```


We also need to get width and height of the user's device, since we want this type of range as an output of  `useTransform`. Rememeber we will use this range of values to animate divs on the x-axis by passing it to the `style={{ x: valueFromUseTransform }}` of the divs

```typescript

  const [screenWidth, setScreenWidth] = useState(0);
  const [screenHeight, setScreenHeight] = useState(0);

  useEffect(() => {
    if (typeof window !== "undefined") {
      setScreenWidth(window.innerWidth);
      setScreenHeight(window.innerHeight);
    }
  }, []);

```

 - `skillsStart` is a value we want to start moving divs on the x-axis
 - `skillsEnd` is a value we want to finish moving divs on the x-axis

```typescript
    // the distance from the top of the page to the top of the `experRef` element.
  const skillsStart = experRef.current?.offsetTop || 0;

   // the distance from the top of the page to the bottom of the `experRef` element.
  const skillsEnd = skillsStart + (experRef.current?.offsetHeight || 0);

```


Now lets pass these values to `useTransform` which will give a value that we can use to move divs on the x-axis

For example 
> when `skillsStart = 200`
>  - `skillsEnd = 600`
>  - screenWidth = 1200

- Convert `scrollY` (300) from the range [200, 600] to the range [-1200, 1200]
- 
```typescript
   // get positive value to move div to the right 
  const divX = useTransform(scrollY, [skillsStart, skillsEnd], [-screenWidth, screenWidth]);

   // get negative value to move div to the left
  const div2_X = useTransform(scrollY, [skillsStart, skillsEnd], [screenWidth, -screenWidth]);


```

Then just pass `divX` and `div2_X` values to `x` property of the divs


```jsx
<motion.p className='absolute top-2 left-0  bg-[#fff]' style={{ x:divX }}>
  Javascript * Python * NodeJS * PostgreSQL
</motion.p>

<motion.p className='absolute left-20 top-[96px] bg-[#fff42d]' style={{ x: div2_X }}>
  ReactJS * NextJS * Typescript * MongoDB
</motion.p>

```


This will move above given two divs to the opposite directions on x-axis as user scrolls the page 
