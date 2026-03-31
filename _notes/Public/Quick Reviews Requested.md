---
title: Quick Reviews Requested
feed: show
date: 2026-03-10
---

I got tired of constantly checking GitHub to see if anyone needed my review on a pull request. Instead of manually clicking through menus, I spent a little time automating it. 

This is a custom Firefox extension that puts a badge on your toolbar. Clicking the badge instantly opens (or switches to) your pending reviews.

### The Code
The plugin is super lightweight. It only requires two files (plus a couple of simple icon images).

**`manifest.json`**
```json
{
    "manifest_version": 2,
    "name": "Quick Reviews Requested",
    "version": "1.2.0",
    "description": "Shows a live count of pending GitHub reviews on the icon and opens the list with one click.",
    "browser_action": {
        "default_icon": {
            "16": "favicon-16x16.png",
            "32": "favicon-32x32.png"
        },
        "default_title": "Go to reviews"
    },
    "permissions":[
        "tabs",
        "https://github.com/*" 
    ],
    "background": {
        "scripts": ["background.js"],
        "persistent": false
    },
    "browser_specific_settings": {
        "gecko": {
            "id": "review-plugin@example.com"
        }
    }
}
```
---

**`background.js`**
```javascript
const targetUrl = "https://github.com/pulls?q=is%3Aopen+review-requested%3A%40me";

chrome.browserAction.onClicked.addListener(() => {
  chrome.tabs.query({}, (tabs) => {
    const existingTab = tabs.find(tab => {
      if (!tab.url || !tab.url.startsWith("https://github.com/pulls")) return false;
      try {
        const urlObj = new URL(tab.url);
        const q = urlObj.searchParams.get("q");
        return q && q.includes("review-requested:@me");
      } catch (e) {
        return false;
      }
    });

    if (existingTab) {
      // If the tab exists, focus its window, make it the active tab, and refresh it
      chrome.windows.update(existingTab.windowId, { focused: true }, () => {
        chrome.tabs.update(existingTab.id, { active: true }, () => {
          chrome.tabs.reload(existingTab.id);
        });
      });
    } else {
      // If the tab doesn't exist, open a new one
      chrome.tabs.create({ url: targetUrl });
    }
  });
});
```

### How to use it

If you just want to test this out temporarily:
1. Save the code above into files named manifest.json and background.js in a new folder.
2. Open Firefox and type about:debugging into the URL bar.
3. Click "This Firefox" -> "Load Temporary Add-on" and select your manifest.json.

Note: Temporary add-ons disappear when you close the browser. If you want to permanently install your own private extensions, check out my guide on [[How to Sign Private Firefox Extensions]]

---

*"Efficiency is intelligent laziness." — David Dunham*