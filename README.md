# SKY Mesh Control Center

An installable Progressive Web App for a SKY Fiber Mesh network.

## Current build: 0.1
- Responsive dashboard for desktop, tablet, and mobile
- Wi-Fi, devices, mesh, network, and settings screens
- PWA manifest and offline service worker
- Demo mode clearly separates sample UI from live router data
- Router admin address can be saved locally in the browser

## Deploy with GitHub Pages
1. Open this repository on GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Select branch **main** and folder **/(root)**, then Save.
5. Wait for GitHub Pages to publish the site. Open the Pages URL over HTTPS.
6. On iPhone, open the site in Safari → Share → Add to Home Screen. On Android, use the browser menu → Install app / Add to Home screen.

## Important: router integration is not connected yet
The app currently runs in Demo Mode. It does not scan the LAN, read connected devices, change Wi-Fi settings, or authenticate to the router. A GitHub Pages site is hosted on HTTPS and browsers restrict direct requests to private HTTP router interfaces. Before live integration, identify the exact router model and firmware and test its supported local API. If needed, use a small local companion service on the home network. Never put router admin credentials in public frontend code.

Router address currently planned: `http://192.168.55.254`.
