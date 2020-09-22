# Chris Learns PWA's 

## Web app manifest 

* Makes the website installable 
* looks and feels like a native app

## Installing Manifest

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

### Name

This is the long name of the app. 


### Short Name

the short name is what will show below the app icon

### Start Url 

Where the app starts on the website

### Scope

What pages should be included in the app. "." would be all 

### Background and Theme Colors 

These colors are set for the app icon, splash screen etc.

### Description 

When ever the browser needs a description, it will use this. the user WILL see it. 

### Dir and Lang

The direction and language of your app. 

### Orientation

which orientation is prefered 

### Icons 

The icons for your app. 

### Related Applications

You can specify native apps. 



