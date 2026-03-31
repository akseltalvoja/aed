---
title: How to Sign Private Firefox Extensions
feed: show
date: 2026-03-10
---

If you build custom Firefox extensions for your own personal use, you'll quickly notice a problem: Firefox doesn't let you install unsigned extensions permanently. If you load them temporarily via `about:debugging`, they vanish the second you close the browser.

To get around this, you have to package and cryptographically sign your extension using Mozilla's `web-ext` tool. Here is how to set up the workflow so you can sign and update plugins directly from your terminal.

### Step 1: Install Node.js and web-ext
The `web-ext` command-line tool runs on Node.js. 
1. If you don't have Node.js installed, download it from [nodejs.org](https://nodejs.org/).
2. Open your terminal and install `web-ext` globally by running:
   ```bash
   npm install --global web-ext
   ```

### Step 2: Get Mozilla API Keys
To sign the plugin, Mozilla needs to verify your developer account.
1. Go to the [Mozilla Add-ons Developer Hub.](https://addons.mozilla.org/en-US/developers/addon/api/key/)
2. Log in with your Firefox account.
3. Generate a new set of API credentials. You will get an Issuer (API Key) and a Secret (API Secret). Keep these safe!

### Step 3: Sign you Extension
Now you are ready to build your .xpi file.
1. Ensure your manifest.json has an explicit ID set in the browser_specific_settings block, otherwise signing will fail:
```json
"browser_specific_settings": {
    "gecko": {
        "id": "your-unique-id@example.com"
    }
}
```
2. Open your terminal, navigate to your extension's folder, and run:
```bash
web-ext sign --api-key=YOUR_API_KEY --api-secret=YOUR_API_SECRET --channel=unlisted
```
*(Make sure to use --channel=unlisted so it doesn't get published to the public Firefox add-on store!)*

### Step 4: Install It
Once the command finishes, web-ext will create a new folder called web-ext-artifacts inside your project directory.

Inside that folder is an .xpi file. Simply drag and drop that file into an open Firefox window, and it will permanently install your custom extension.

### Updating your Plugin later
Whenever you want to make changes to your code, simply:
1. Bump the "version" number in your manifest.json (e.g., from 1.0.0 to 1.0.1).
2. Run the exact same web-ext sign command again.
3. Drag the newly generated .xpi file into Firefox to update it!

---

*"The best tools are the ones you build for yourself." — Unknown* 