
# Chapter 4

## How to Optimize Actions with Calculations?

- **Separate Logic from Events**: Keep your main code separate from bussiness logic.
- **Do not use Global Variables**: Pass needed values as arguments instead.
- **Don’t Modify Objects Directly**: Copy data, change the copy, and return it.
- **Use Arguments for Inputs**: Functions should take inputs and return outputs.



<img src="https://github.com/user-attachments/assets/8597540a-f34a-4da9-a86f-88d663e47a1d" alt="image" width="600"/>

<img src="https://github.com/user-attachments/assets/3800dcac-67be-4ea4-beca-0d483ca0d763" alt="image" width="600"/>



Make your functions simple by having them just take input and return output, turning actions into calculations.


## Aplication at work:

There is a hook that filters out allowed routes for a user based on `accessibleRoutes` list it gets from the server. 

```typescript
export const useTenantNav = () => {
  const { accessibleRoutePathList } = useTenant();
  const rawNavConfig = navConfig[0] || {};
  const { items: navList } = rawNavConfig;

  const filteredParentItems = navList.filter((navItem) => {
    const { path } = navItem;
    return isMatchRoute(accessibleRoutePathList, path, true);
  });
  const newItems = filteredParentItems
    .map((items) => {
      const { children } = items;
      const newChildren = children?.filter((child) => {
        const { path } = child;
        return isMatchRoute(accessibleRoutePathList, path);
      });
      return { ...items, children: newChildren };
    })
    .filter((i) => i?.children?.length !== 0);

  return [{ ...rawNavConfig, items: newItems }];
};

```


So I've tried  to apply functional programming principles, trying to trun above action into smaller actions or calculations as possible. 

so filtering parent routes becomes : 

```typescript
const getParentRoutes = (navList: NavList[], accessibleRoutes: string[]): NavList[] => {
  //Filters out main menu items you can access
  return navList.filter((navItem) => {
    const { path } = navItem;
    return isMatchRoute(accessibleRoutes, path, true);
  });
};

```

filtering out sub  routes become:

```typescript
const getAccessibleSubRoutes = (item: NavItem, accessibleRoutes: string[]): NavChildren[] => {
  //Filters out sub-items within a menu item that you can access.
  const { children } = item;
  const newChildren = children?.filter((child: any) => {
    const { path } = child;
    return isMatchRoute(accessibleRoutes, path);
  });
  return { ...item, children: newChildren };
};

```

and finaling generating list of allowed routes :

```typescript
const getAccessibleRoutes = (children: NavChildren[], accessibleRoutes: string[]): NavList[] => {
  //Ensures each menu item has only the accessible sub-items and removes those with none.
  return children
    .map((item) => getAccessibleSubRoutes(item, accessibleRoutes))
    .filter((item) => item?.children?.length !== 0);
};
```
