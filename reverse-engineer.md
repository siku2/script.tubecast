---
---

I tried for days to setup an emulator to inspect the network traffic of the YouTube TV app but I never got it working.
Amongst many other issues the app is using (encrypted, of course) [QUIC](https://en.wikipedia.org/wiki/QUIC) which means using a simple http MITM doesn't work.

For a much better experience look no further than your browser: Youtube Leanback.
Youtube Leanback was canned a few months ago, it now forwards to the normal [youtube.com](https://youtube.com) website but by using a custom user agent it's still possible to get the old app.


## Firefox

1. Open a new tab
2. Open the Responsive Design Mode (**Ctrl + Shift + M**)
3. Open the settings in the top-right corner and tick "Show user agent" 
4. Enter a TV user agent like `Mozilla/5.0 (SMART-TV; Linux; Tizen 4.0.0.2) AppleWebkit/605.1.15 (KHTML, like Gecko)`
5. Go to [youtube.com/tv](https://youtube.com/tv). It should actually load the app now.
6. Open the Network Monitor (**Ctrl + Shift + E**)
(You may also close the Responsive Design Mode again to get a better overview).

Now you can monitor the requests.
You may want to filter for XHR requests only and look out for the requests with urls containing `/bind`.