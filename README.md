# dev-tool-font-changer
Chrome Development Tools Font Changer

1. Enable `#enable-devtools-experiments` flag in `chrome://flags` section.
2. Open Chorme Devtools and check `Settings > Experiments > Allow custom UI themes`.
3. Create the following four files in a dedicated folder.

    3.1. `devtools.html`
	
	```html
	<html>
	<head></head>
	<body><script src="devtools.js"></script></body>
	</html>
	```
	
	3.2. `devtools.js`
	
	```javascript
	var x = new XMLHttpRequest();
	x.open('GET', 'style.css');
	x.onload = function() {
		chrome.devtools.panels.applyStyleSheet(x.responseText);
	};
	x.send();
	```
	
	3.3. `style.css`
	
	```css
	/*
	try replacing .platform-linux with .platform-mac in the stylesheet. For more information, check the official source of these styles in Chromium for reference
	*/
	:host-context(.platform-linux) .monospace,
	:host-context(.platform-linux) .source-code,
	.platform-linux .monospace,
	.platform-linux .source-code {
		font-size: 11px !important;
		font-family: Consolas, monospace !important;
	}
	
	.monospace,
	.source-code {
		font-size: 11px !important;
		font-family: Consolas, monospace !important;
	}
	
	::shadow .monospace,
	::shadow .source-code {
		font-size: 11px !important;
        font-family: Consolas, monospace !important;
	}
	```
	
	3.4. `manifest.json`
	
	```javascript
    {
        "name": "Custom Chrome Devtools Theme",
        "version": "1.0.0",
        "description": "A customized theme for Chrome Devtools.",
        "devtools_page": "devtools.html",
        "manifest_version": 2
	}
	```

4. Open Chrome Extensions tab, click `Load expanded extension` and point to the folder containing all four files.
