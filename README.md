To reproduce the problem with vite-imagetools:

- `pnpm install`
- `pnpm build`
- `pnpm preview`

The second test logo will not be loaded, because vite-imagetools (currently) writes the transformed image to disk with url-encoded filename (which is also wrong), but the web server will look for a file with the url decoded.

The main reason for vite-imagetools doing this is because vite does not url-encode asset urls when they are written to html or js output (I assume). I already have a PR in the vite-imagetools repository to remove this behavior and output files unencoded, and maintainers have signaled to me that it will be accepted if vite will provide the url-encoding, which in their opinion is also the correct place to do it.
