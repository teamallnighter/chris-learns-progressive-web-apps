# Chris Learns PWA's 

## Manifest.json

[01 Start](https://github.com/teamallnighter/chris-learns-progressive-web-apps/tree/main/app-manifest-01--start)

[02 Adding Properties](https://github.com/teamallnighter/chris-learns-progressive-web-apps/tree/main/app-manifest-02--added-properties)

[03 Final manifest.json](https://github.com/teamallnighter/chris-learns-progressive-web-apps/tree/main/app-manifest-02--added-properties)


### Web app manifest 

* Makes the website installable 
* looks and feels like a native app

### Installing Manifest

Create a manifest.json file 
add this to your head

```html
<link rel="manifest" href="/manifest.json">
```

```json
{
  "name": "Instagram as Progressive Web App",
  "short_name": "PWAGram",
  "icons": [
    {
      "src": "/src/images/icons/app-icon-48x48.png",
      "type": "image/png",
      "sizes": "48x48"
    },
    {
      "src": "/src/images/icons/app-icon-96x96.png",
      "type": "image/png",
      "sizes": "96x96"
    },
    {
      "src": "/src/images/icons/app-icon-144x144.png",
      "type": "image/png",
      "sizes": "144x144"
    },
    {
      "src": "/src/images/icons/app-icon-192x192.png",
      "type": "image/png",
      "sizes": "192x192"
    },
    {
      "src": "/src/images/icons/app-icon-256x256.png",
      "type": "image/png",
      "sizes": "256x256"
    },
    {
      "src": "/src/images/icons/app-icon-384x384.png",
      "type": "image/png",
      "sizes": "384x384"
    },
    {
      "src": "/src/images/icons/app-icon-512x512.png",
      "type": "image/png",
      "sizes": "512x512"
    }
  ],
  "start_url": "/index.html",
  "scope": ".",
  "display": "standalone",
  "orientation": "portrait-primary",
  "background_color": "#fff",
  "theme_color": "#3f51b5",
  "description": "A simple Instagram Clone, implementing a lot of PWA love.",
  "dir": "ltr",
  "lang": "en-US"
}
```

#### Name

This is the long name of the app. 


#### Short Name

the short name is what will show below the app icon

#### Start Url 

Where the app starts on the website

#### Scope

What pages should be included in the app. "." would be all 

#### Background and Theme Colors 

These colors are set for the app icon, splash screen etc.

#### Description 

When ever the browser needs a description, it will use this. the user WILL see it. 

#### Dir and Lang

The direction and language of your app. 

#### Orientation

which orientation is prefered 

#### Icons 

The icons for your app. 

#### Related Applications

You can specify native apps. 


### Using Chrome to check your PWA

go to developers tools 

Click 'Applications' 

#### Emulating devices

[Android Studio](https://developer.android.com/studio)

[Apple Emulator](https://developer.apple.com/documentation/xcode/running_your_app_in_the_simulator_or_on_a_device)




## Service Workers

Srrvices workers run on their own thread. 

A service worker is a background process and will continue to run even if you close the app


### Service Workers Listenable Events

* Fetch 
* Push Notifications
* Notification Interactions

### Registering a Service Worker

```javascript

self.addEventListener('install', function(event) {
  console.log('[Service Worker] Installing Service Worker ...', event);
});

self.addEventListener('activate', function(event) {
  console.log('[Service Worker] Activating Service Worker ...', event);
  return self.clients.claim();
});

self.addEventListener('fetch', function(event) {
  console.log('[Service Worker] Fetching something ....', event);
  event.respondWith(fetch(event.request));
});
```

## Service Worker 

### What is a service worker?

> A service worker is a type of web worker. It's essentially a JavaScript file that runs separately from the main browser thread, intercepting network requests, caching or retrieving resources from the cache, and delivering push messages.

#### Registering the service worker 

```javascript
var deferredPrompt;

if ('serviceWorker' in navigator) {
  navigator.serviceWorker
    .register('/sw.js')
    .then(function () {
      console.log('Service worker registered!');
    });
}
```

#### Adding an install prompt 

We have to wait three seconds before the install prompt is allowed to come up. 

```javascript
window.addEventListener('beforeinstallprompt', function(event) {
  console.log('beforeinstallprompt fired');
  event.preventDefault();
  deferredPrompt = event;
  return false;
});

setTimeout(function() {
  console.log('This is executed once the timer is done!');
}, 3000);

console.log('This is executed right after setTimeout()');
```

### Using Fetch

```javascript
var deferredPrompt;

if (!window.Promise) {
  window.Promise = Promise;
}

if ('serviceWorker' in navigator) {
  navigator.serviceWorker
    .register('/sw.js')
    .then(function () {
      console.log('Service worker registered!');
    })
    .catch(function(err) {
      console.log(err);
    });
}

window.addEventListener('beforeinstallprompt', function(event) {
  console.log('beforeinstallprompt fired');
  event.preventDefault();
  deferredPrompt = event;
  return false;
});

var promise = new Promise(function(resolve, reject) {
  setTimeout(function() {
    //resolve('This is executed once the timer is done!');
    reject({code: 500, message: 'An error occurred!'});
    //console.log('This is executed once the timer is done!');
  }, 3000);
});

var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://httpbin.org/ip');
xhr.responseType = 'json';

xhr.onload = function() {
  console.log(xhr.response);
};

xhr.onerror = function() {
  console.log('Error!');
};

xhr.send();

fetch('https://httpbin.org/ip')
  .then(function(response) {
    console.log(response);
    return response.json();
  })
  .then(function(data) {
    console.log(data);
  })
  .catch(function(err) {
    console.log(err);
  });

fetch('https://httpbin.org/post', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Accept': 'application/json'
  },
  mode: 'cors',
  body: JSON.stringify({message: 'Does this work?'})
})
  .then(function(response) {
    console.log(response);
    return response.json();
  })
  .then(function(data) {
    console.log(data);
  })
  .catch(function(err) {
    console.log(err);
  });

// promise.then(function(text) {
//   return text;
// }, function(err) {
//   console.log(err.code, err.message)
// }).then(function(newText) {
//   console.log(newText);
// });

promise.then(function(text) {
  return text;
}).then(function(newText) {
  console.log(newText);
}).catch(function(err) {
  console.log(err.code, err.message);
});

console.log('This is executed right after setTimeout()');
```

## Caching 

With the service worker our PWA can pre cache content

### The Cahce API

With the cache API we can store information on the browser BUT we control it. 