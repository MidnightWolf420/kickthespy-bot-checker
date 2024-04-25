# Kick The Spy Bot Checker

This tool allows you to check for spy bots on Discord servers using a JSON array of server IDs and names.

## Instructions

To extract Discord server IDs and names using the browser console:

1. Open [Discord](https://discord.com/channels/@me) in a web browser and log in to your account.
2. Wait for Discord to fully load.
3. Press `F12` (or `Ctrl + Shift + J` on Windows/Linux or `Cmd + Option + J` on macOS) to open the browser's developer tools.
4. Go to the "Console" tab within the developer tools.
5. Copy and paste the following JavaScript code into the console:

```javascript
var servers = Array.from(document.querySelectorAll("div[aria-label=Servers] > div")).map(server => {
	let serverIcon = server.querySelector("img");
	if (serverIcon) {
		let serverDiv = serverIcon.parentNode;
		let server = {
			name: serverDiv.getAttribute("aria-label").replace(/\d{1,} mentions?, /gi, "").trim(),
			id: serverDiv.getAttribute("data-list-item-id").replace("guildsnav___", "")
		};
		return server;
	} else {
		return null;
	}
}).filter(server => server != null);
console.log(JSON.stringify(servers, null, 2));
navigator.clipboard.writeText(JSON.stringify(servers, null, 2)).then(() => {
	console.log("Server list successfully copied to clipboard");
}).catch((error) => {
	console.error("Unable to copy server list to clipboard, Try copying it manually");
});
```
6. Go to https://midnightwolf420.github.io/kickthespy-bot-checker/ and paste the json array received from the previous step in the text area.
7. Press "Check For Bots".
