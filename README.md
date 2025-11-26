# lossless-ui

High-fidelity music streaming UI built with SvelteKit and Tailwind.

## API: [https://github.com/sachinsenal0x64/hifi](https://github.com/sachinsenal0x64/hifi)



## Downloads

- Track downloads now bundle title, album, artist, ISRC, track/disc numbers, release year, and artwork so files stay organized in local libraries.
- Artist pages include a "Download Discography" control plus one-click album download buttons. Progress and errors surface inline while requests are processed.
- FFmpeg WASM assets stream from the official CDN on demand. If the browser cannot load FFmpeg (for example older or restricted environments), downloads gracefully fall back to the original stream without metadata injection.



## Development Notes

- Some requests are proxied through the first-party SvelteKit route at `/api/proxy` so the browser can call the API without CORS errors.
- API responses are cached in Redis when the following environment variables are present:
  - `REDIS_URL` (preferred) or `REDIS_HOST`/`REDIS_PORT`/`REDIS_PASSWORD`/`REDIS_USERNAME`
  - Optional tuning knobs:
    - `REDIS_CACHE_TTL_SECONDS` (default 300)
    - `REDIS_CACHE_TTL_SEARCH_SECONDS` (default 300)
    - `REDIS_CACHE_TTL_TRACK_SECONDS` (default 120)
    - `REDIS_CACHE_MAX_BODY_BYTES` (default 200000)
- Cached responses are stored only for safe GET requests without `Authorization`, `Cookie`, or `Range` headers. Responses larger than `REDIS_CACHE_MAX_BODY_BYTES`, non-text/JSON payloads, 4xx/5xx statuses, and responses with `Cache-Control: no-store|private` are never cached.
- Install dependencies with `npm install` after updating `package.json`.

## Todo
