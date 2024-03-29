## PWA (Progressive Web App)

#### What is PWA?
[Progeressive Web App](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) is a functionality that can make webapps act like native apps in the Apple Store or Google Store. 

Webapp is still going to be hosted on the web, but by adding PWA functionality to it, we can enable them to work offline, access to push notifications, and the ability to be added to the user's home screen for quick access. 


#### How does it work?

PWA works with the help of [service workers](https://learn.microsoft.com/en-us/microsoft-edge/progressive-web-apps-chromium/how-to/service-workers). So basically, when the user opens your app in the browser, PWA's Service Worker gets installed. The service worker then runs in parallel with your app and can continue doing work even when your app is not running. Service workers are responsible for intercepting, modifying, and responding to network requests.

### How do I add PWA functionality to a React.js or Next.js app? 
**1.** Install the service worker. The two most common ones are [workbox](https://www.npmjs.com/package/workbox), [next-pwa](https://www.npmjs.com/package/next-pwa) , next-pwa is the most recent one, published in 2022.

```
npm i next-pwa 
```

**2.** Create a configuration file at ```/public/manifest.json```

The keyword ```manifest``` for naming is required. The ```manifest.json``` file is a key component of PWA. It provides metadata and configuration information about the application, allowing browsers and devices to understand and present the PWA appropriately.

You can use this [page](https://www.simicart.com/manifest-generator.html/) to create a custom ```manifest.json``` file with auto-customized icons to various sizes. You will need to upload your icon file.

Sample ```manifest.json``` file: 
```json
{
    "theme_color": "#49111C",
    "background_color": "#fff",
    "display": "standalone",
    "id": "/",
    "scope": "/",
    "start_url": "/",
    "name": "Food Communication",
    "short_name": "FoodCom",
    "description": "A platform to request for custom catering service in Korea",
    "icons": [
        {
            "src": "/manifest/icon-192x192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "/manifest/icon-256x256.png",
            "sizes": "256x256",
            "type": "image/png"
        },
        {
            "src": "/manifest/icon-384x384.png",
            "sizes": "384x384",
            "type": "image/png"
        },
        {
            "src": "/manifest/icon-512x512.png",
            "sizes": "512x512",
            "type": "image/png"
        }
    ]
}
```
**3.** Add the link to manifest.json file in the ```_document.tsx``` or ```_document.js```
   ```html
       <Head>
          <link rel="manifest" href="/manifest.json" />
       </Head>
   ```

### and that should be it!
Simply run ```npm run build```
followed by ```npm run start``` to check if your application is working offline as well.

#### Keep in Mind
While working on your React project in the development environment using ```npm run dev```, you might not be able to fully experience all the Progressive Web App (PWA) functionality. To fully test your PWA features, you should  `npm run build` your project and see in hte production mode. However, you can still check if your PWA is functioning correctly by inspecting the 'Application' section in Chrome DevTools.


![Chrome-Dev Tools/Application](https://github.com/abroroo/til/blob/main/PWA/pwaCheck-Applications.png?raw=true)








