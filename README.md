# iOS 12 Safari audio bug

We noticed a weird issue for a couple of our mp3 voice recordings, that it played the sound twice, and we tracked down the problem to only occur in Safari on iOS, and it seems to only show if the file is served from a CDN supporting [HTTP range headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Range_requests) (for example GitHub pages), if served without range header support (with `python -m SimpleHTTPServer 8000` for example), it seems to work.

We first thought the files were corrupt or otherwise damaged, but looking at the files in an audio editor or looking at their metadata in `ffmpeg` or `file` doesn't seem to hint at any issues, also the `<audio/>`-tag events for both the files seems to be the same, and they're all recorded in the same batch too.

This repo contains a simple [html page](index.html) ([online](https://possan.github.io/ios12-safari-bug/)) that shows the problem.

We've seen this bug on latest iOS 12 at the time of writing (12.4, UA: `Mozilla/5.0 (iPhone; CPU iPhone OS 12_4 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.1.2 Mobile/15E148 Safari/604.1`) both on device and even in iOS Simulator, this bug does not seem to be there anymore on the first iOS 13 release.
