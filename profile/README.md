# Adding developer CSS for Flair Themes

- Retrieve the store hash from the customer control panel URL
- Create a repo using the store hash as a name
- Add the client name to the repo description to identify it in the future
- Push a file named `custom.css` to the main branch for store CSS
- Push a file named `checkout.css` for checkout and order confirmation CSS
- Enable Developer Custom CSS in the global theme options panel in theme editor for appropriate files
- Note that stencil helpers do not work in these files

## Aditional notes

### Limit customer involvement in a support ticket

- Store hash can be retrieved without the customers involvement. View the source code of their live site and find a CDN URL. Locate the hash in the path, which starts with `/s-`. The hash follows the hyphen.

```
<link rel="dns-prefetch preconnect" href="https://cdn11.bigcommerce.com/s-4yo3xyp5" crossorigin>
```

- In this case, we can add hotfixes for a customer and ask them to enable developer css in their theme editor.

### JS Delivr cache

- CSS should be tested locally and pushed all at once to the repo, before it is called by JS Delivr to the frontend. JS Delivr has a long cache time (over 7 days) so any changes made to the file will take a while to come through
- You can attempt to purge the cache manually by locating the JS Delivr path to the custom CSS file in the page source code and opening the file in a new browser tab.

```
<link href="https://cdn.jsdelivr.net/gh/flair-themes/xxxxxxx/custom.css?c=5591492" rel="stylesheet">
```

- Remove the querystring from the end of the URL in the addres bar
- Replace the subdomain `cdn` with `purge` and hit enter

```
https://purge.jsdelivr.net/gh/flair-themes/xxxxxxx/custom.css
```

- You will receive a success message in the browser window to show which caches have been purged

```
{
  "id": "A53G6bo76aXGdNit",
  "status": "finished",
  "timestamp": "2022-08-23T08:56:23.199Z",
  "paths": {
    "/gh/flair-themes/xxxxxxx/custom.css": {
      "throttled": false,
      "providers": {
        "fastly": true,
        "bunny": true,
        "cloudflare": true,
        "gcore": true,
        "quantil": true
      }
    }
  }
}
```
