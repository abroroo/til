When have a list with filters, and you want to keep active filters even if user refreshes the page or shares the link.

In React, we often do it using "state." But if the page reloads, this state resets, and we forget which filters were applied.

To fix this, we can use the URL (the web address) to remember the state.

Here's how we can do it:

1. **Sync State with URL:** When the user searches for something, we update the URL to include this searchString. This way, the URL always shows what's currently filtered or being searched.

2. **Initialize State from URL:** When the page loads, we check the URL to see which filters should be applied. This ensures that if we shares the URL or refreshes the page, the correct filtered list is shown.

By using the URL to store the current state, our app becomes more reliable and user-friendly. Users can bookmark or share specific views, and everything stays in sync, even after a page reload.

This helps to get rid of react states, reducing re-rendering dependency of React page. 

![image](https://github.com/user-attachments/assets/3813032f-f7cf-47b5-9fd8-cc92db0739c9)


#### For example 

This code below which uses `search` state:

```typescript

export default function Page() {
  let [search, setSearch] = useState(''); 
  let { data } = useQuery({ 
    queryKey: ['people', search],
    queryFn: async () => {
      let res = await fetch(`/api/people?search=${search}`); 
      let data = await res.json();

      return data;
    }, 
  });

  return (
    <>
...
        <Input
          value={search} 
          onChange={(e) => setSearch(e.target.value)} 
          placeholder="Find someone..."
        />
 
... // show data.map(item)
          
    </>
  );
}

```

can be replaced with simple variable:

```typescript

export default function Home() {
  let searchParams = useSearchParams();
  let search = searchParams.get('search') ?? '';
  
  let { data } = useQuery({
    queryKey: ['people', search],
    queryFn: async () => {
      let res = await fetch(`/api/people?search=${search}`);
      let data = await res.json();

      return data as Response;
    },
   
  });

  return (
    <>
      {/* ... */}
      
      <Input
        value={search}
        onChange={(e) => {
          let search = e.target.value;
          
          if (search) {
            router.push(`${pathname}?search=${search}`);
          }
        }}
        placeholder="Find someone..."
      />
    </>
  );
}

```

With this way of storing `search` text in the URL, we can get rid of react state. Now even on refresh page will still render filtered list. Also iti s good use cass s for backward and forward button of the browser. So if onClick to list itme you get redirected to item detail, apress back backward button you still get filtered list with last search string. 

