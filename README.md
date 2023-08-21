# Cross-Domain Reference Linking

This repository demonstrates a pattern for selecting a reference from one window (or an iframe) and then updating the value in the parent window. Two methods are showcased:

1. Direct usage of `window.opener` to update the parent window.
2. A more secure and flexible approach using iframes and the `postMessage()` method, which works across different domains.


## Why Would You Want This?
This approach provides a good UX for letting you easily connect resources between two different web pages or systems. By utilizing methods like `postMessage()`, you can ensure data is transferred securely between domains, and provide an integrated user experience without the constraints of cross-domain restrictions.

This was inspired by Django Admin which uses a similar approach.

## Main takeaways

1. **Cross-Origin Restrictions**: When dealing with content from different origins (domains, protocols, or ports), the browser imposes strict limitations due to the **Same-Origin Policy**. It ensures that potentially harmful actions cannot be taken by malicious websites. This means that a page from one origin cannot directly access properties or invoke methods on a window from another origin.

2. **Window.opener Vulnerabilities**: Directly using `window.opener` can expose a potential vulnerability known as **tab-nabbing**. A malicious page could potentially redirect the opener page to a harmful site. Always be cautious about the web content and avoid using it for different domains.

3. **Using postMessage()**: The `postMessage()` method provides a way to securely communicate between windows or iframes of different origins. It's a safer alternative to directly using `window.opener`, especially when dealing with different domains.


## File Structure

```
├── index.html          # Parent window for direct `window.opener` usage.
├── other.html          # Child window for direct `window.opener` usage.
└── with-iframe
    ├── index.html      # Parent window using iframes and `postMessage()`.
    └── other.html      # iframe content for the `postMessage()` approach.
```

## Setup and Running

1. Clone this repository:
   ```
   git clone https://github.com/rix1/cross-domain-reference-linking.git
   cd cross-domain-reference-linking
   ```

2. Run the server from the root directory (you can use any other HTTP server of your choice)
   ```
   npx http-server .
   ```

3. To simulate the cross-domain scenario for the iframe example, open a new terminal/tab and change the port:
   ```
   npx http-server . --port 3031
   ```

## Using the Cross-Domain Iframe Example

1. Navigate to `with-iframe/index.html` in your code editor.
2. Update the `OTHER_SERVICE_ADDRESS` to point to the address where your second server (or domain) is running (should be printed after step 3). This will be the source of your iframe.

## Testing

1. For the direct `window.opener` example, open `index.html` in a browser.
2. For the cross-domain iframe example, open `with-iframe/index.html` in a browser.

You should be able to select a reference in the child window or iframe, and see that reference reflected in the parent window.
