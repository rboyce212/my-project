# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in your browser.

The page will reload when you make changes.\
You may also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can't go back!**

If you aren't satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you're on your own.

You don't have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn't feel obligated to use this feature. However we understand that this tool wouldn't be useful if you couldn't customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `npm run build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)


---
Code Splitting
---
---

Instead of downloading the entire app before users can use it, code splitting allows you to split your code into small chunks which you can then load on demand.

This project setup supports code splitting via [dynamic `import()`](https://2ality.com/2017/01/import-operator.html#loading-code-on-demand). Its [proposal](https://github.com/tc39/proposal-dynamic-import) is in stage 4. The `import()` function-like form takes the module name as an argument and returns a [`Promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) which always resolves to the namespace object of the module.

Here is an example:

#### `moduleA.js`

```js
const moduleA = 'Hello';

export { moduleA };
```

#### `App.js`

```js
import React, { Component } from 'react';

class App extends Component {
  handleClick = () => {
    import('./moduleA')
      .then(({ moduleA }) => {
        // Use moduleA
      })
      .catch(err => {
        // Handle failure
      });
  };

  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Load</button>
      </div>
    );
  }
}

export default App;
```

This will make `moduleA.js` and all its unique dependencies as a separate chunk that only loads after the user clicks the 'Load' button. For more information on the chunks that are created, see the [production build](production-build.md) section.

You can also use it with `async` / `await` syntax if you prefer it.

### With React Router

If you are using React Router check out [this tutorial](https://reactjs.org/docs/code-splitting.html#route-based-code-splitting)

Also check out the [Code Splitting](https://reactjs.org/docs/code-splitting.html) section in React documentation.


---
Analyzing the Bundle Size
---
---

[Source map explorer](https://www.npmjs.com/package/source-map-explorer) analyzes
JavaScript bundles using the source maps. This helps you understand where code
bloat is coming from.

To add Source map explorer to a Create React App project, follow these steps:

```sh
npm install --save source-map-explorer
```

Alternatively you may use `yarn`:

```sh
yarn add source-map-explorer
```

Then in `package.json`, add the following line to `scripts`:

```diff
   "scripts": {
+    "analyze": "source-map-explorer 'build/static/js/*.js'",
     "start": "react-scripts start",
     "build": "react-scripts build",
     "test": "react-scripts test",
```

Then to analyze the bundle run the production build then run the analyze
script.

```sh
npm run build
npm run analyze
```


---
Making a Progressive Web App
---
---

The production build has all the tools necessary to generate a first-class
[Progressive Web App](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps),
but **the offline/cache-first behavior is opt-in only**.

Starting with Create React App 4, you can add a `src/service-worker.js` file to
your project to use the built-in support for
[Workbox](https://developers.google.com/web/tools/workbox/)'s
[`InjectManifest`](https://developers.google.com/web/tools/workbox/reference-docs/latest/module-workbox-webpack-plugin.InjectManifest)
plugin, which will
[compile](https://developers.google.com/web/tools/workbox/guides/using-bundlers)
your service worker and inject into it a list of URLs to
[precache](https://developers.google.com/web/tools/workbox/guides/precache-files).

If you start a new project using one of the PWA [custom
templates](https://create-react-app.dev/docs/custom-templates/), you'll get a
`src/service-worker.js` file that serves as a good starting point for an
offline-first service worker:

```sh
npx create-react-app my-app --template cra-template-pwa
```

The TypeScript equivalent is:

```sh
npx create-react-app my-app --template cra-template-pwa-typescript
```

If you know that you won't be using service workers, or if you'd prefer to use a
different approach to creating your service worker, don't create a
`src/service-worker.js` file. The `InjectManifest` plugin won't be run in that
case.

In addition to creating your local `src/service-worker.js` file, it needs to be
registered before it will be used. In order to opt-in to the offline-first
behavior, developers should look for the following in their
[`src/index.js`](https://github.com/cra-template/pwa/blob/master/packages/cra-template-pwa/template/src/index.js)
file:

```js
// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://cra.link/PWA
serviceWorkerRegistration.unregister();
```

As the comment states, switching `serviceWorker.unregister()` to
`serviceWorker.register()` will opt you in to using the service worker.

#### Why Opt-in?

Offline-first Progressive Web Apps are faster and more reliable than traditional
web pages, and provide an engaging mobile experience:

- All static site assets that are a part of your `webpack` build are cached so
  that your page loads fast on subsequent visits, regardless of network
  connectivity (such as 2G or 3G). Updates are downloaded in the background.
- Your app will work regardless of network state, even if offline. This means
  your users will be able to use your app at 10,000 feet and on the subway.
- On mobile devices, your app can be added directly to the user's home screen,
  app icon and all. This eliminates the need for the app store.

However, they [can make debugging deployments more
challenging](https://github.com/facebook/create-react-app/issues/2398).

The
[`workbox-webpack-plugin`](https://developer.chrome.com/docs/workbox/modules/workbox-webpack-plugin/)
is integrated into production configuration, and it will take care of compiling
a service worker file that will automatically precache all of your
`webpack`-generated assets and keep them up to date as you deploy updates. The
service worker will use a [cache-first
strategy](https://developers.google.com/web/fundamentals/instant-and-offline/offline-cookbook/#cache-falling-back-to-network)
for handling all requests for `webpack`-generated assets, including [navigation
requests](https://developers.google.com/web/fundamentals/primers/service-workers/high-performance-loading#first_what_are_navigation_requests)
for your HTML, ensuring that your web app is consistently fast, even on a slow
or unreliable network.

Note: Resources that are not generated by `webpack`, such as static files that are
copied over from your local
[`public/` directory](https://github.com/cra-template/pwa/tree/master/packages/cra-template-pwa/template/public/)
or third-party resources, will not be precached. You can optionally set up Workbox
[routes](https://developers.google.com/web/tools/workbox/guides/route-requests)
to apply the runtime caching strategy of your choice to those resources.

#### Customization

Starting with Create React App 4, you have full control over customizing the
logic in this service worker, by creating your own `src/service-worker.js` file,
or customizing the one added by the `cra-template-pwa` (or
`cra-template-pwa-typescript`) template. You can use [additional
modules](https://developers.google.com/web/tools/workbox/modules) from the
Workbox project, add in a push notification library, or remove some of the
default caching logic. The one requirement is that you keep `self.__WB_MANIFEST`
somewhere in your file, as the Workbox compilation plugin checks for this value
when generating a manifest of URLs to precache. If you would prefer not to use
precaching, you can assign `self.__WB_MANIFEST` to a variable that will be
ignored, like:

```js
// eslint-disable-next-line no-restricted-globals
const ignored = self.__WB_MANIFEST;

// Your custom service worker code goes here.
```

#### Offline-First Considerations

If you do decide to opt-in to service worker registration, please take the
following into account:

1. After the initial caching is done, the [service worker lifecycle](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle)
   controls when updated content ends up being shown to users. In order to guard against
   [race conditions with lazy-loaded content](https://github.com/facebook/create-react-app/issues/3613#issuecomment-353467430),
   the default behavior is to conservatively keep the updated service worker in the "[waiting](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle#waiting)"
   state. This means that users will end up seeing older content until they close (reloading is not
   enough) their existing, open tabs. See [this blog post](https://jeffy.info/2018/10/10/sw-in-c-r-a.html)
   for more details about this behavior.

1. Users aren't always familiar with offline-first web apps. It can be useful to
   [let the user know](https://developers.google.com/web/fundamentals/instant-and-offline/offline-ux#inform_the_user_when_the_app_is_ready_for_offline_consumption)
   when the service worker has finished populating your caches (showing a "This web
   app works offline!" message) and also let them know when the service worker has
   fetched the latest updates that will be available the next time they load the
   page (showing a "New content is available once existing tabs are closed." message). Showing
   these messages is currently left as an exercise to the developer, but as a
   starting point, you can make use of the logic included in [`src/serviceWorkerRegistration.js`](https://github.com/cra-template/pwa/blob/master/packages/cra-template-pwa/template/src/serviceWorkerRegistration.js), which
   demonstrates which service worker lifecycle events to listen for to detect each
   scenario, and which as a default, only logs appropriate messages to the
   JavaScript console.

1. Service workers [require HTTPS](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers#you_need_https),
   although to facilitate local testing, that policy
   [does not apply to `localhost`](https://stackoverflow.com/questions/34160509/options-for-testing-service-workers-via-http/34161385#34161385).
   If your production web server does not support HTTPS, then the service worker
   registration will fail, but the rest of your web app will remain functional.

1. The service worker is only enabled in the [production environment](deployment.md),
   e.g. the output of `npm run build`. It's recommended that you do not enable an
   offline-first service worker in a development environment, as it can lead to
   frustration when previously cached assets are used and do not include the latest
   changes you've made locally.

1. If you _need_ to test your offline-first service worker locally, build
   the application (using `npm run build`) and run a standard http server from your
   build directory. After running the build script, `create-react-app` will give
   instructions for one way to test your production build locally and the [deployment instructions](deployment.md) have
   instructions for using other methods. _Be sure to always use an
   incognito window to avoid complications with your browser cache._

1. By default, the generated service worker file will not intercept or cache any
   cross-origin traffic, like HTTP [API requests](integrating-with-an-api-backend.md),
   images, or embeds loaded from a different domain. Starting with Create
   React App 4, this can be customized, as explained above.

#### Progressive Web App Metadata

The production build has all the tools necessary to generate a first-class
[Progressive Web App](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps),
but **the offline/cache-first behavior is opt-in only**.

Starting with Create React App 4, you can add a `src/service-worker.js` file to
your project to use the built-in support for
[Workbox](https://developers.google.com/web/tools/workbox/)'s
[`InjectManifest`](https://developers.google.com/web/tools/workbox/reference-docs/latest/module-workbox-webpack-plugin.InjectManifest)
plugin, which will
[compile](https://developers.google.com/web/tools/workbox/guides/using-bundlers)
your service worker and inject into it a list of URLs to
[precache](https://developers.google.com/web/tools/workbox/guides/precache-files).

If you start a new project using one of the PWA [custom
templates](https://create-react-app.dev/docs/custom-templates/), you'll get a
`src/service-worker.js` file that serves as a good starting point for an
offline-first service worker:

```sh
npx create-react-app my-app --template cra-template-pwa
```

The TypeScript equivalent is:

```sh
npx create-react-app my-app --template cra-template-pwa-typescript
```

If you know that you won't be using service workers, or if you'd prefer to use a
different approach to creating your service worker, don't create a
`src/service-worker.js` file. The `InjectManifest` plugin won't be run in that
case.

In addition to creating your local `src/service-worker.js` file, it needs to be
registered before it will be used. In order to opt-in to the offline-first
behavior, developers should look for the following in their
[`src/index.js`](https://github.com/cra-template/pwa/blob/master/packages/cra-template-pwa/template/src/index.js)
file:

```js
// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://cra.link/PWA
serviceWorkerRegistration.unregister();
```

As the comment states, switching `serviceWorker.unregister()` to
`serviceWorker.register()` will opt you in to using the service worker.

## Why Opt-in?

Offline-first Progressive Web Apps are faster and more reliable than traditional
web pages, and provide an engaging mobile experience:

- All static site assets that are a part of your `webpack` build are cached so
  that your page loads fast on subsequent visits, regardless of network
  connectivity (such as 2G or 3G). Updates are downloaded in the background.
- Your app will work regardless of network state, even if offline. This means
  your users will be able to use your app at 10,000 feet and on the subway.
- On mobile devices, your app can be added directly to the user's home screen,
  app icon and all. This eliminates the need for the app store.

However, they [can make debugging deployments more
challenging](https://github.com/facebook/create-react-app/issues/2398).

The
[`workbox-webpack-plugin`](https://developer.chrome.com/docs/workbox/modules/workbox-webpack-plugin/)
is integrated into production configuration, and it will take care of compiling
a service worker file that will automatically precache all of your
`webpack`-generated assets and keep them up to date as you deploy updates. The
service worker will use a [cache-first
strategy](https://developers.google.com/web/fundamentals/instant-and-offline/offline-cookbook/#cache-falling-back-to-network)
for handling all requests for `webpack`-generated assets, including [navigation
requests](https://developers.google.com/web/fundamentals/primers/service-workers/high-performance-loading#first_what_are_navigation_requests)
for your HTML, ensuring that your web app is consistently fast, even on a slow
or unreliable network.

Note: Resources that are not generated by `webpack`, such as static files that are
copied over from your local
[`public/` directory](https://github.com/cra-template/pwa/tree/master/packages/cra-template-pwa/template/public/)
or third-party resources, will not be precached. You can optionally set up Workbox
[routes](https://developers.google.com/web/tools/workbox/guides/route-requests)
to apply the runtime caching strategy of your choice to those resources.

## Customization

Starting with Create React App 4, you have full control over customizing the
logic in this service worker, by creating your own `src/service-worker.js` file,
or customizing the one added by the `cra-template-pwa` (or
`cra-template-pwa-typescript`) template. You can use [additional
modules](https://developers.google.com/web/tools/workbox/modules) from the
Workbox project, add in a push notification library, or remove some of the
default caching logic. The one requirement is that you keep `self.__WB_MANIFEST`
somewhere in your file, as the Workbox compilation plugin checks for this value
when generating a manifest of URLs to precache. If you would prefer not to use
precaching, you can assign `self.__WB_MANIFEST` to a variable that will be
ignored, like:

```js
// eslint-disable-next-line no-restricted-globals
const ignored = self.__WB_MANIFEST;

// Your custom service worker code goes here.
```

## Offline-First Considerations

If you do decide to opt-in to service worker registration, please take the
following into account:

1. After the initial caching is done, the [service worker lifecycle](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle)
   controls when updated content ends up being shown to users. In order to guard against
   [race conditions with lazy-loaded content](https://github.com/facebook/create-react-app/issues/3613#issuecomment-353467430),
   the default behavior is to conservatively keep the updated service worker in the "[waiting](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle#waiting)"
   state. This means that users will end up seeing older content until they close (reloading is not
   enough) their existing, open tabs. See [this blog post](https://jeffy.info/2018/10/10/sw-in-c-r-a.html)
   for more details about this behavior.

1. Users aren't always familiar with offline-first web apps. It can be useful to
   [let the user know](https://developers.google.com/web/fundamentals/instant-and-offline/offline-ux#inform_the_user_when_the_app_is_ready_for_offline_consumption)
   when the service worker has finished populating your caches (showing a "This web
   app works offline!" message) and also let them know when the service worker has
   fetched the latest updates that will be available the next time they load the
   page (showing a "New content is available once existing tabs are closed." message). Showing
   these messages is currently left as an exercise to the developer, but as a
   starting point, you can make use of the logic included in [`src/serviceWorkerRegistration.js`](https://github.com/cra-template/pwa/blob/master/packages/cra-template-pwa/template/src/serviceWorkerRegistration.js), which
   demonstrates which service worker lifecycle events to listen for to detect each
   scenario, and which as a default, only logs appropriate messages to the
   JavaScript console.

1. Service workers [require HTTPS](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers#you_need_https),
   although to facilitate local testing, that policy
   [does not apply to `localhost`](https://stackoverflow.com/questions/34160509/options-for-testing-service-workers-via-http/34161385#34161385).
   If your production web server does not support HTTPS, then the service worker
   registration will fail, but the rest of your web app will remain functional.

1. The service worker is only enabled in the [production environment](deployment.md),
   e.g. the output of `npm run build`. It's recommended that you do not enable an
   offline-first service worker in a development environment, as it can lead to
   frustration when previously cached assets are used and do not include the latest
   changes you've made locally.

1. If you _need_ to test your offline-first service worker locally, build
   the application (using `npm run build`) and run a standard http server from your
   build directory. After running the build script, `create-react-app` will give
   instructions for one way to test your production build locally and the [deployment instructions](deployment.md) have
   instructions for using other methods. _Be sure to always use an
   incognito window to avoid complications with your browser cache._

1. By default, the generated service worker file will not intercept or cache any
   cross-origin traffic, like HTTP [API requests](integrating-with-an-api-backend.md),
   images, or embeds loaded from a different domain. Starting with Create
   React App 4, this can be customized, as explained above.

## Progressive Web App Metadata

The default configuration includes a web app manifest located at
[`public/manifest.json`](https://github.com/cra-template/pwa/blob/master/packages/cra-template-pwa/template/public/manifest.json), that you can customize with
details specific to your web application.

When a user adds a web app to their homescreen using Chrome or Firefox on
Android, the metadata in [`manifest.json`](https://github.com/cra-template/pwa/blob/master/packages/cra-template-pwa/template/public/manifest.json) determines what
icons, names, and branding colors to use when the web app is displayed.
[The Web App Manifest guide](https://developers.google.com/web/fundamentals/engage-and-retain/web-app-manifest/)
provides more context about what each field means, and how your customizations
will affect your users' experience.

Progressive web apps that have been added to the homescreen will load faster and
work offline when there's an active service worker. That being said, the
metadata from the web app manifest will still be used regardless of whether or
not you opt-in to service worker registration.
 
---
Advanced Configuration
---
---

You can adjust various development and production settings by setting environment variables in your shell or with [.env](adding-custom-environment-variables.md#adding-development-environment-variables-in-env).

> Note: You do not need to declare `REACT_APP_` before the below variables as you would with custom environment variables.

| Variable                  | Development | Production | Usage                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| :------------------------ | :---------: | :--------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| BROWSER                   |   ✅ Used   | 🚫 Ignored | By default, Create React App will open the default system browser, favoring Chrome on macOS. Specify a [browser](https://github.com/sindresorhus/open#app) to override this behavior, or set it to `none` to disable it completely. If you need to customize the way the browser is launched, you can specify a node script instead. Any arguments passed to `npm start` will also be passed to this script, and the url where your app is served will be the last argument. Your script's file name must have the `.js` extension.                                                                                                                                      |
| BROWSER_ARGS              |   ✅ Used   | 🚫 Ignored | When the `BROWSER` environment variable is specified, any arguments that you set to this environment variable will be passed to the browser instance. Multiple arguments are supported as a space separated list. By default, no arguments are passed through to browsers.                                                                                                                                                                                                                                                                                                                                                                                               |
| HOST                      |   ✅ Used   | 🚫 Ignored | By default, the development web server binds to all hostnames on the device (`localhost`, LAN network address, etc.). You may use this variable to specify a different host.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| PORT                      |   ✅ Used   | 🚫 Ignored | By default, the development web server will attempt to listen on port 3000 or prompt you to attempt the next available port. You may use this variable to specify a different port.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| HTTPS                     |   ✅ Used   | 🚫 Ignored | When set to `true`, Create React App will run the development server in `https` mode.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| WDS_SOCKET_HOST           |   ✅ Used   | 🚫 Ignored | When set, Create React App will run the development server with a custom websocket hostname for hot module reloading. Normally, `webpack-dev-server` defaults to `window.location.hostname` for the SockJS hostname. You may use this variable to start local development on more than one Create React App project at a time. See [webpack-dev-server documentation](https://webpack.js.org/configuration/dev-server/#devserversockhost) for more details.                                                                                                                                                                                                              |
| WDS_SOCKET_PATH           |   ✅ Used   | 🚫 Ignored | When set, Create React App will run the development server with a custom websocket path for hot module reloading. Normally, `webpack-dev-server` defaults to `/ws` for the SockJS pathname. You may use this variable to start local development on more than one Create React App project at a time. See [webpack-dev-server documentation](https://webpack.js.org/configuration/dev-server/#devserversockpath) for more details.                                                                                                                                                                                                                                       |
| WDS_SOCKET_PORT           |   ✅ Used   | 🚫 Ignored | When set, Create React App will run the development server with a custom websocket port for hot module reloading. Normally, `webpack-dev-server` defaults to `window.location.port` for the SockJS port. You may use this variable to start local development on more than one Create React App project at a time. See [webpack-dev-server documentation](https://webpack.js.org/configuration/dev-server/#devserversockport) for more details.                                                                                                                                                                                                                          |
| PUBLIC_URL                |   ✅ Used   |  ✅ Used   | Create React App assumes your application is hosted at the serving web server's root or a subpath as specified in [`package.json` (`homepage`)](deployment.md#building-for-relative-paths). Normally, Create React App ignores the hostname. You may use this variable to force assets to be referenced verbatim to the url you provide (hostname included). This may be particularly useful when using a CDN to host your application.                                                                                                                                                                                                                                  |
| BUILD_PATH                | 🚫 Ignored  |  ✅ Used   | By default, Create React App will output compiled assets to a `/build` directory adjacent to your `/src`. You may use this variable to specify a new path for Create React App to output assets. BUILD_PATH should be specified as a path relative to the root of your project.                                                                                                                                                                                                                                                                                                                                                                                          |
| CI                        |   ✅ Used   |  ✅ Used   | When set to `true`, Create React App treats warnings as failures in the build. It also makes the test runner non-watching. Most CIs set this flag by default.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| REACT_EDITOR              |   ✅ Used   | 🚫 Ignored | When an app crashes in development, you will see an error overlay with clickable stack trace. When you click on it, Create React App will try to determine the editor you are using based on currently running processes, and open the relevant source file. You can [send a pull request to detect your editor of choice](https://github.com/facebook/create-react-app/issues/2636). Setting this environment variable overrides the automatic detection. If you do it, make sure your systems [PATH](<https://en.wikipedia.org/wiki/PATH_(variable)>) environment variable points to your editor’s bin folder. You can also set it to `none` to disable it completely. |
| CHOKIDAR_USEPOLLING       |   ✅ Used   | 🚫 Ignored | When set to `true`, the watcher runs in polling mode, as necessary inside a VM. Use this option if `npm start` isn't detecting changes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| GENERATE_SOURCEMAP        | 🚫 Ignored  |  ✅ Used   | When set to `false`, source maps are not generated for a production build. This solves out of memory (OOM) issues on some smaller machines.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| INLINE_RUNTIME_CHUNK      | 🚫 Ignored  |  ✅ Used   | By default, Create React App will embed the runtime script into `index.html` during the production build. When set to `false`, the script will not be embedded and will be imported as usual. This is normally required when dealing with CSP.                                                                                                                                                                                                                                                                                                                                                                                                                           |
| IMAGE_INLINE_SIZE_LIMIT   |   ✅ Used   |  ✅ Used   | By default, images smaller than 10,000 bytes are encoded as a data URI in base64 and inlined in the CSS or JS build artifact. Set this to control the size limit in bytes. Setting it to `0` will disable the inlining of images.                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| FAST_REFRESH              |   ✅ Used   | 🚫 Ignored | When set to `false`, disables experimental support for Fast Refresh to allow you to tweak your components in real time without reloading the page.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| TSC_COMPILE_ON_ERROR      |   ✅ Used   |  ✅ Used   | When set to `true`, you can run and properly build TypeScript projects even if there are TypeScript type check errors. These errors are printed as warnings in the terminal and/or browser console.                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| ESLINT_NO_DEV_ERRORS      |   ✅ Used   | 🚫 Ignored | When set to `true`, ESLint errors are converted to warnings during development. As a result, ESLint output will no longer appear in the error overlay.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| DISABLE_ESLINT_PLUGIN     |   ✅ Used   |  ✅ Used   | When set to `true`, [eslint-webpack-plugin](https://github.com/webpack-contrib/eslint-webpack-plugin) will be completely disabled.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| DISABLE_NEW_JSX_TRANSFORM |   ✅ Used   |  ✅ Used   | When set to `true`, disables the [new JSX transform](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html) introduced in React 17 and backported to React 16.14.0, 15.7.0, and 0.14.10. New projects will use a version of React that supports this by default but you may need to disable it in existing projects if you can't upgrade React.                                                                                                                                                                                                                                                                                                     |


---
Deployment
---
---

`npm run build` creates a `build` directory with a production build of your app. Set up your favorite HTTP server so that a visitor to your site is served `index.html`, and requests to static paths like `/static/js/main.<hash>.js` are served with the contents of the `/static/js/main.<hash>.js` file. For more information see the [production build](production-build.md) section.

## Static Server

For environments using [Node](https://nodejs.org/), the easiest way to handle this would be to install [serve](https://github.com/vercel/serve) and let it handle the rest:

```sh
npm install -g serve
serve -s build
```

The last command shown above will serve your static site on the port **3000**. Like many of [serve](https://github.com/vercel/serve)’s internal settings, the port can be adjusted using the `-l` or `--listen` flags:

```sh
serve -s build -l 4000
```

Run this command to get a full list of the options available:

```sh
serve -h
```

## Other Solutions

You don’t necessarily need a static server in order to run a Create React App project in production. It also works well when integrated into an existing server side app.

Here’s a programmatic example using [Node](https://nodejs.org/) and [Express](https://expressjs.com/):

```javascript
const express = require('express');
const path = require('path');
const app = express();

app.use(express.static(path.join(__dirname, 'build')));

app.get('/', function (req, res) {
  res.sendFile(path.join(__dirname, 'build', 'index.html'));
});

app.listen(9000);
```

The choice of your server software isn’t important either. Since Create React App is completely platform-agnostic, there’s no need to explicitly use Node.

The `build` folder with static assets is the only output produced by Create React App.

However this is not quite enough if you use client-side routing. Read the next section if you want to support URLs like `/todos/42` in your single-page app.

## Serving Apps with Client-Side Routing

If you use routers that use the HTML5 [`pushState` history API](https://developer.mozilla.org/en-US/docs/Web/API/History_API#Adding_and_modifying_history_entries) under the hood (for example, [React Router](https://github.com/ReactTraining/react-router) with `browserHistory`), many static file servers will fail. For example, if you used React Router with a route for `/todos/42`, the development server will respond to `localhost:3000/todos/42` properly, but an Express serving a production build as above will not.

This is because when there is a fresh page load for a `/todos/42`, the server looks for the file `build/todos/42` and does not find it. The server needs to be configured to respond to a request to `/todos/42` by serving `index.html`. For example, we can amend our Express example above to serve `index.html` for any unknown paths:

```diff
 app.use(express.static(path.join(__dirname, 'build')));

-app.get('/', function (req, res) {
+app.get('/*', function (req, res) {
   res.sendFile(path.join(__dirname, 'build', 'index.html'));
 });
```

If you’re using [Apache HTTP Server](https://httpd.apache.org/), you need to create a `.htaccess` file in the `public` folder that looks like this:

```
    Options -MultiViews
    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^ index.html [QSA,L]
```

It will get copied to the `build` folder when you run `npm run build`.

If you’re using [Apache Tomcat](https://tomcat.apache.org/), you need to follow [this Stack Overflow answer](https://stackoverflow.com/a/41249464/4878474).

Now requests to `/todos/42` will be handled correctly both in development and in production.

On a production build, and when you've [opted-in](making-a-progressive-web-app.md#why-opt-in),
a [service worker](https://developers.google.com/web/fundamentals/primers/service-workers/) will automatically handle all navigation requests, like for
`/todos/42`, by serving the cached copy of your `index.html`. This
service worker navigation routing can be configured or disabled by
[`eject`ing](available-scripts.md#npm-run-eject) and then modifying the
[`navigateFallback`](https://github.com/GoogleChrome/sw-precache#navigatefallback-string)
and [`navigateFallbackWhitelist`](https://github.com/GoogleChrome/sw-precache#navigatefallbackwhitelist-arrayregexp)
options of the `SWPrecachePlugin` configuration.

When users install your app to the homescreen of their device the default configuration will make a shortcut to `/index.html`. This may not work for client-side routers which expect the app to be served from `/`. Edit the web app manifest at `public/manifest.json` and change `start_url` to match the required URL scheme, for example:

```js
  "start_url": ".",
```

## Building for Relative Paths

By default, Create React App produces a build assuming your app is hosted at the server root.

To override this, specify the `homepage` in your `package.json`, for example:

```js
  "homepage": "http://mywebsite.com/relativepath",
```

This will let Create React App correctly infer the root path to use in the generated HTML file.

**Note**: If you are using `react-router@^4`, you can root `<Link>`s using the `basename` prop on any `<Router>`.

More information [here](https://reacttraining.com/react-router/web/api/BrowserRouter/basename-string).

For example:

```js
<BrowserRouter basename="/calendar"/>
<Link to="/today"/> // renders <a href="/calendar/today">
```

### Serving the Same Build from Different Paths

> Note: this feature is available with `react-scripts@0.9.0` and higher.

If you are not using the HTML5 `pushState` history API or not using client-side routing at all, it is unnecessary to specify the URL from which your app will be served. Instead, you can put this in your `package.json`:

```js
  "homepage": ".",
```

This will make sure that all the asset paths are relative to `index.html`. You will then be able to move your app from `http://mywebsite.com` to `http://mywebsite.com/relativepath` or even `http://mywebsite.com/relative/path` without having to rebuild it.

## Customizing Environment Variables for Arbitrary Build Environments

You can create an arbitrary build environment by creating a custom `.env` file and loading it using [env-cmd](https://www.npmjs.com/package/env-cmd).

For example, to create a build environment for a staging environment:

1. Create a file called `.env.staging`
1. Set environment variables as you would any other `.env` file (e.g. `REACT_APP_API_URL=http://api-staging.example.com`)
1. Install [env-cmd](https://www.npmjs.com/package/env-cmd)
   ```sh
   $ npm install env-cmd --save
   $ # or
   $ yarn add env-cmd
   ```
1. Add a new script to your `package.json`, building with your new environment:
   ```json
   {
     "scripts": {
       "build:staging": "env-cmd -f .env.staging npm run build"
     }
   }
   ```

Now you can run `npm run build:staging` to build with the staging environment config.
You can specify other environments in the same way.

Variables in `.env.production` will be used as fallback because `NODE_ENV` will always be set to `production` for a build.

## [AWS Amplify](https://console.amplify.aws)

The AWS Amplify Console provides continuous deployment and hosting for modern web apps (single page apps and static site generators) with serverless backends. The Amplify Console offers globally available CDNs, custom domain setup, feature branch deployments, and password protection.

1. Login to the Amplify Console [here](https://console.aws.amazon.com/amplify/home).
1. Connect your Create React App repo and pick a branch. If you're looking for a Create React App+Amplify starter, try the [create-react-app-auth-amplify starter](https://github.com/swaminator/create-react-app-auth-amplify) that demonstrates setting up auth in 10 minutes with Create React App.
1. The Amplify Console automatically detects the build settings. Choose Next.
1. Choose _Save and deploy_.

If the build succeeds, the app is deployed and hosted on a global CDN with an amplifyapp.com domain. You can now continuously deploy changes to your frontend or backend. Continuous deployment allows developers to deploy updates to their frontend and backend on every code commit to their Git repository.

## [Azure](https://azure.microsoft.com/)

Azure Static Web Apps creates an automated build and deploy pipeline for your React app powered by GitHub Actions. Applications are geo-distributed by default with multiple points of presence. PR's are built automatically for staging environment previews.

1. Create a new Static Web App [here](https://ms.portal.azure.com/#create/Microsoft.StaticApp).
1. Add in the details and connect to your GitHub repo.
1. Make sure the build folder is set correctly on the "build" tab and create the resource.

Azure Static Web Apps will automatically configure a GitHub Action in your repo and begin the deployment.

See the [Azure Static Web Apps documentation](https://aka.ms/swadocs) for more information on routing, APIs, authentication and authorization, custom domains and more.

## [Firebase](https://firebase.google.com/)

Install the Firebase CLI if you haven’t already by running `npm install -g firebase-tools`. Sign up for a [Firebase account](https://console.firebase.google.com/) and create a new project. Run `firebase login` and login with your previous created Firebase account.

Then run the `firebase init` command from your project’s root. You need to choose the **Hosting: Configure and deploy Firebase Hosting sites** and choose the Firebase project you created in the previous step. You will need to agree with `database.rules.json` being created, choose `build` as the public directory, and also agree to **Configure as a single-page app** by replying with `y`.

```sh
    === Project Setup

    First, let's associate this project directory with a Firebase project.
    You can create multiple project aliases by running firebase use --add,
    but for now we'll set up a default project.

    ? What Firebase project do you want to associate as default? Example app (example-app-fd690)

    === Database Setup

    Firebase Realtime Database Rules allow you to define how your data should be
    structured and when your data can be read from and written to.

    ? What file should be used for Database Rules? database.rules.json
    ✔  Database Rules for example-app-fd690 have been downloaded to database.rules.json.
    Future modifications to database.rules.json will update Database Rules when you run
    firebase deploy.

    === Hosting Setup

    Your public directory is the folder (relative to your project directory) that
    will contain Hosting assets to uploaded with firebase deploy. If you
    have a build process for your assets, use your build's output directory.

    ? What do you want to use as your public directory? build
    ? Configure as a single-page app (rewrite all urls to /index.html)? Yes
    ✔  Wrote build/index.html

    i  Writing configuration info to firebase.json...
    i  Writing project information to .firebaserc...

    ✔  Firebase initialization complete!
```

IMPORTANT: you need to set proper HTTP caching headers for `service-worker.js` file in `firebase.json` file or you will not be able to see changes after first deployment ([issue #2440](https://github.com/facebook/create-react-app/issues/2440)). It should be added inside `"hosting"` key like next:

```json
{
  "hosting": {
    ...
    "headers": [
      {"source": "/service-worker.js", "headers": [{"key": "Cache-Control", "value": "no-cache"}]}
    ]
    ...
```

Now, after you create a production build with `npm run build`, you can deploy it by running `firebase deploy`.

```sh
    === Deploying to 'example-app-fd690'...

    i  deploying database, hosting
    ✔  database: rules ready to deploy.
    i  hosting: preparing build directory for upload...
    Uploading: [==============================          ] 75%✔  hosting: build folder uploaded successfully
    ✔  hosting: 8 files uploaded successfully
    i  starting release process (may take several minutes)...

    ✔  Deploy complete!

    Project Console: https://console.firebase.google.com/project/example-app-fd690/overview
    Hosting URL: https://example-app-fd690.firebaseapp.com
```

For more information see [Firebase Hosting](https://firebase.google.com/docs/hosting).

## [GitHub Pages](https://pages.github.com/)

> Note: this feature is available with `react-scripts@0.2.0` and higher.

### Step 1: Add `homepage` to `package.json`

**The step below is important!**<br/>

**If you skip it, your app will not deploy correctly.**

Open your `package.json` and add a `homepage` field for your project:

```json
  "homepage": "https://myusername.github.io/my-app",
```

or for a GitHub user page:

```json
  "homepage": "https://myusername.github.io",
```

or for a custom domain page:

```json
  "homepage": "https://mywebsite.com",
```

Create React App uses the `homepage` field to determine the root URL in the built HTML file.

### Step 2: Install `gh-pages` and add `deploy` to `scripts` in `package.json`

Now, whenever you run `npm run build`, you will see a cheat sheet with instructions on how to deploy to GitHub Pages.

To publish it at [https://myusername.github.io/my-app](https://myusername.github.io/my-app), run:

```sh
npm install --save gh-pages
```

Alternatively you may use `yarn`:

```sh
yarn add gh-pages
```

Add the following scripts in your `package.json`:

```diff
  "scripts": {
+   "predeploy": "npm run build",
+   "deploy": "gh-pages -d build",
    "start": "react-scripts start",
    "build": "react-scripts build",
```

The `predeploy` script will run automatically before `deploy` is run.

If you are deploying to a GitHub user page instead of a project page you'll need to make one
additional modification:

1. Tweak your `package.json` scripts to push deployments to **main**:

```diff
  "scripts": {
    "predeploy": "npm run build",
-   "deploy": "gh-pages -d build",
+   "deploy": "gh-pages -b main -d build",
```

### Step 3: Deploy the site by running `npm run deploy`

Then run:

```sh
npm run deploy
```

### Step 4: For a project page, ensure your project’s settings use `gh-pages`

Finally, make sure **GitHub Pages** option in your GitHub project settings is set to use the `gh-pages` branch:

<img src="https://i.imgur.com/HUjEr9l.png" width="500" alt="gh-pages branch setting" />

### Step 5: Optionally, configure the domain

You can configure a custom domain with GitHub Pages by adding a `CNAME` file to the `public/` folder.

Your CNAME file should look like this:

```
mywebsite.com
```

### Notes on client-side routing

GitHub Pages doesn’t support routers that use the HTML5 `pushState` history API under the hood (for example, React Router using `browserHistory`). This is because when there is a fresh page load for a url like `http://user.github.io/todomvc/todos/42`, where `/todos/42` is a frontend route, the GitHub Pages server returns 404 because it knows nothing of `/todos/42`. If you want to add a router to a project hosted on GitHub Pages, here are a couple of solutions:

- You could switch from using HTML5 history API to routing with hashes. If you use React Router, you can switch to `hashHistory` for this effect, but the URL will be longer and more verbose (for example, `http://user.github.io/todomvc/#/todos/42?_k=yknaj`). [Read more](https://reacttraining.com/react-router/web/api/Router) about different history implementations in React Router.
- Alternatively, you can use a trick to teach GitHub Pages to handle 404s by redirecting to your `index.html` page with a custom redirect parameter. You would need to add a `404.html` file with the redirection code to the `build` folder before deploying your project, and you’ll need to add code handling the redirect parameter to `index.html`. You can find a detailed explanation of this technique [in this guide](https://github.com/rafrex/spa-github-pages).

### Troubleshooting

#### "/dev/tty: No such a device or address"

If, when deploying, you get `/dev/tty: No such a device or address` or a similar error, try the following:

1. Create a new [Personal Access Token](https://github.com/settings/tokens)
2. `git remote set-url origin https://<user>:<token>@github.com/<user>/<repo>` .
3. Try `npm run deploy` again

#### "Cannot read property 'email' of null"

If, when deploying, you get `Cannot read property 'email' of null`, try the following:

1. `git config --global user.name '<your_name>'`
2. `git config --global user.email '<your_email>'`
3. Try `npm run deploy` again

## [Heroku](https://www.heroku.com/)

Use the [Heroku Buildpack for Create React App](https://github.com/heroku/heroku-buildpack-nodejs).

You can find instructions in [Deploying React with Zero Configuration](https://blog.heroku.com/deploying-react-with-zero-configuration).

### Resolving Heroku Deployment Errors

Sometimes `npm run build` works locally but fails during deploy via Heroku. Following are the most common cases.

#### "Module not found: Error: Cannot resolve 'file' or 'directory'"

If you get something like this:

```
remote: Failed to create a production build. Reason:
remote: Module not found: Error: Cannot resolve 'file' or 'directory'
MyDirectory in /tmp/build_1234/src
```

It means you need to ensure that the lettercase of the file or directory you `import` matches the one you see on your filesystem or on GitHub.

This is important because Linux (the operating system used by Heroku) is case sensitive. So `MyDirectory` and `mydirectory` are two distinct directories and thus, even though the project builds locally, the difference in case breaks the `import` statements on Heroku remotes.

#### "Could not find a required file."

If you exclude or ignore necessary files from the package you will see a error similar this one:

```
remote: Could not find a required file.
remote:   Name: `index.html`
remote:   Searched in: /tmp/build_a2875fc163b209225122d68916f1d4df/public
remote:
remote: npm ERR! Linux 3.13.0-105-generic
remote: npm ERR! argv "/tmp/build_a2875fc163b209225122d68916f1d4df/.heroku/node/bin/node" "/tmp/build_a2875fc163b209225122d68916f1d4df/.heroku/node/bin/npm" "run" "build"
```

In this case, ensure that the file is there with the proper lettercase and that’s not ignored on your local `.gitignore` or `~/.gitignore_global`.

## [Netlify](https://www.netlify.com/)

**To do a manual deploy to Netlify’s CDN:**

```sh
npm install netlify-cli -g
netlify deploy
```

Choose `build` as the path to deploy.

**To setup continuous delivery:**

With this setup Netlify will build and deploy when you push to git or open a pull request:

1. [Start a new netlify project](https://app.netlify.com/signup)
2. Pick your Git hosting service and select your repository
3. Click `Build your site`

**Support for client-side routing:**

To support `pushState`, make sure to create a `public/_redirects` file with the following rewrite rules:

```
/*  /index.html  200
```

When you build the project, Create React App will place the `public` folder contents into the build output.

## [Vercel](https://vercel.com)

[Vercel](https://vercel.com/home) is a cloud platform that enables developers to host Jamstack websites and web services that deploy instantly, scale automatically, and requires no supervision, all with zero configuration. They provide a global edge network, SSL encryption, asset compression, cache invalidation, and more.

### Step 1: Deploying your React project to Vercel

To deploy your React project with a [Vercel for Git Integration](https://vercel.com/docs/git-integrations), make sure it has been pushed to a Git repository.

Import the project into Vercel using the [Import Flow](https://vercel.com/import/git). During the import, you will find all relevant [options](https://vercel.com/docs/build-step#build-&-development-settings) preconfigured for you with the ability to change as needed.

After your project has been imported, all subsequent pushes to branches will generate [Preview Deployments](https://vercel.com/docs/platform/deployments#preview), and all changes made to the [Production Branch](https://vercel.com/docs/git-integrations#production-branch) (commonly "master" or "main") will result in a [Production Deployment](https://vercel.com/docs/platform/deployments#production).

Once deployed, you will get a URL to see your app live, such as the following: https://create-react-app-example.vercel.app/.

### Step 2 (optional): Using a Custom Domain

If you want to use a Custom Domain with your Vercel deployment, you can **Add** or **Transfer in** your domain via your Vercel [account Domain settings.](https://vercel.com/dashboard/domains)

To add your domain to your project, navigate to your [Project](https://vercel.com/docs/platform/projects) from the Vercel Dashboard. Once you have selected your project, click on the "Settings" tab, then select the **Domains** menu item. From your projects **Domain** page, enter the domain you wish to add to your project.

Once the domain has been added, you will be presented with different methods for configuring it.

### Deploying a fresh React project

You can deploy a fresh React project, with a Git repository set up for you, with the following Deploy Button:

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/import/git?s=https%3A%2F%2Fgithub.com%2Fvercel%2Fvercel%2Ftree%2Fmaster%2Fexamples%2Fcreate-react-app)

### Vercel References:

- [Example Source](https://github.com/vercel/vercel/tree/master/examples/create-react-app)
- [Official Vercel Guide](https://vercel.com/guides/deploying-react-with-vercel-cra)
- [Vercel Deployment Docs](https://vercel.com/docs)
- [Vercel Custom Domain Docs](https://vercel.com/docs/custom-domains)

## [Render](https://render.com)

Render offers free [static site](https://render.com/docs/static-sites) hosting with fully managed SSL, a global CDN and continuous auto deploys from GitHub.

Deploy your app in only a few minutes by following the [Create React App deployment guide](https://render.com/docs/deploy-create-react-app).

Use invite code `cra` to sign up or use [this link](https://render.com/i/cra).

## [S3](https://aws.amazon.com/s3) and [CloudFront](https://aws.amazon.com/cloudfront/)

See this [blog post](https://medium.com/@omgwtfmarc/deploying-create-react-app-to-s3-or-cloudfront-48dae4ce0af) on how to deploy your React app to Amazon Web Services S3 and CloudFront. If you are looking to add a custom domain, HTTPS and continuous deployment see this [blog post](https://medium.com/dailyjs/a-guide-to-deploying-your-react-app-with-aws-s3-including-https-a-custom-domain-a-cdn-and-58245251f081).

## [Surge](https://surge.sh/)

Install the Surge CLI if you haven’t already by running `npm install -g surge`. Run the `surge` command and log in you or create a new account.

When asked about the project path, make sure to specify the `build` folder, for example:

```sh
       project path: /path/to/project/build
```

Note that in order to support routers that use HTML5 `pushState` API, you may want to rename the `index.html` in your build folder to `200.html` before deploying to Surge. This [ensures that every URL falls back to that file](https://surge.sh/help/adding-a-200-page-for-client-side-routing).

## Publishing Components To npm

Create React App doesn't provide any built-in functionality to publish a component to npm. If you're ready to extract a component from your project so other people can use it, we recommend moving it to a separate directory outside of your project and then using a tool like [nwb](https://github.com/insin/nwb#react-components-and-libraries) to prepare it for publishing.


---
## `npm run build` fails to minify
---
---

Before `react-scripts@2.0.0`, this problem was caused by third party `node_modules` using modern JavaScript features because the minifier couldn't handle them during the build. This has been solved by compiling standard modern JavaScript features inside `node_modules` in `react-scripts@2.0.0` and higher.

If you're seeing this error, you're likely using an old version of `react-scripts`. You can either fix it by avoiding a dependency that uses modern syntax, or by upgrading to `react-scripts@>=2.0.0` and following the migration instructions in the changelog.
