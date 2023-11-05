## PWA (Progressive Web App)

#### What is PWA?
[Progeressive Web App](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps) is a functionality that can make webapps act like native apps in the Apple Store or Google Store. Your webapp is still going to be hosted on the web, but by adding PWA functionality to it, we can enable them to work offline, giving users a smooth experience regardless of their network connection or device.

#### How does it work?

PWA works with the help of [service workers](https://learn.microsoft.com/en-us/microsoft-edge/progressive-web-apps-chromium/how-to/service-workers). So basically, when the user accesses your app, PWA's Service Worker is installed. The service worker then runs in parallel with your app and can continue doing work even when your app is not running. Service workers are responsible for intercepting, modifying, and responding to network requests.

#### How do I add PWA functionality to a Next.js app? 
1. Install the service worker. The two most common ones are [workbox](https://www.npmjs.com/package/workbox), [next-pwa](https://www.npmjs.com/package/next-pwa) , next-pwa is the most recent one, released in 2022.

```
npm i next-pwa 
```

2. Create a configuration file at ```/public/manifest.json```

The keyword ```manifest``` for naming is required. The ```manifest.json``` file is a key component of a Progressive Web Application (PWA). It provides metadata and configuration information about the application, allowing browsers and devices to understand and present the PWA appropriately.

You can use this [page](https://www.simicart.com/manifest-generator.html/) to create a custom ```manifest.json``` file with auto-customized icons to various sizes. You will need to upload your icon file.

3. Add to the link to manifest.json file in the ```_document.tsx``` or ```_document.js```
   ```
       <Head>
          <link rel="manifest" href="/manifest.json" />
       </Head>
   ```

### and that should be it!
Now you can check if your pwa is working at chrome dev tools ```Application``` section 


