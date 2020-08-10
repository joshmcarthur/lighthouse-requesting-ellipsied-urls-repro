# Reproduces Lighthouse issue requesting malformed URLs

https://github.com/GoogleChrome/lighthouse/issues/11244

1. Start a static server. I used `python3 -m http.server` which starts a server
   on port 8000. Make sure it's an option that logs incoming requests. 
2. Run `bash audit.sh [hostname]` where `[hostname]` is the URL. e.g. `bash
   audit.sh http://localhost:8000`
3. Check each of the requests for image.jpg. At least one will be malformed, ending
   in `%E2%80%A6` (an ellipsis character).

The test page includes two images, one of which has a long URL with a failing
audit against it. If you run an audit and watch your server requests, you'll see
a request for the image, but with the query string truncated with an ellipsis
character.

