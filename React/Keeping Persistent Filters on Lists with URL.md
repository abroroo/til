### Keeping Persistent Filters on Lists with URL  

I've read an interesting article about using the page URL to maintain persistent filters on lists. I use lists often at work, so this method of keeping filters persistent grabbed my attention. I'd recommend reading the [article](https://buildui.com/posts/how-to-control-a-react-component-with-the-url).  

Here’s my take on it:  

When we have a list with filters, we want to keep active filters even if the user refreshes the page or shares the link.  

In React, we often do this using **state**, but if the page reloads, the state resets, and we lose the applied filters.  

To fix this, we can use the **URL** (the web address) to store the filters and make them persistent.

#### Here's how we can do it:

  - Instead of using React state for filters, we put them in the URL.
  
  - When the page loads, we read filters from the URL so the right data is shown.
  
  - Now, filters stay even after a refresh, and we can share the link with the same filtered results.
  
  
  This also reduces unnecessary re-renders since we’re not relying on React state.

![image](https://github.com/user-attachments/assets/3813032f-f7cf-47b5-9fd8-cc92db0739c9)


#### For example 

#### Loses filters on refresh:

```typescript

export default function Page() {
  let [search, setSearch] = useState('');

  let { data } = useQuery({
    queryKey: ['people', search],
    queryFn: async () => {
      let res = await fetch(`/api/people?search=${search}`);
      return res.json();
    },
  });

  return (
    <>
      <Input
        value={search}
        onChange={(e) => setSearch(e.target.value)}
        placeholder="Find someone..."
      />
      {/* Render list */}
    </>
  );
}


```
Here, when we refresh, the search disappears because state resets.


#### Filters persist after refresh:

```typescript

export default function Home() {
  let searchParams = useSearchParams();
  let search = searchParams.get('search') ?? '';

  let { data } = useQuery({
    queryKey: ['people', search],
    queryFn: async () => {
      let res = await fetch(`/api/people?search=${search}`);
      return res.json();
    },
  });

  return (
    <>
      <Input
        value={search}
        onChange={(e) => {
          let search = e.target.value;
          router.push(`${pathname}?search=${search}`);
        }}
        placeholder="Find someone..."
      />
      {/* Render list */}
    </>
  );
}


```
Now, the search text stays in the URL, so even after a refresh, we see the same filtered list

It's also useful for the browser's **back and forward buttons**. If we click on a list item and navigate to its details, pressing the **back button** will return us to the filtered list with the last search still applied.

