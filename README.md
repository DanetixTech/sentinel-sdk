<p align="center">
  <a href="https://danetix.com">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://danetix.com/logo-white.svg">
      <source media="(prefers-color-scheme: light)" srcset="https://danetix.com/logo-dark.svg">
      <img src="https://danetix.com/logo-dark.svg" alt="Danetix" width="260">
    </picture>
  </a>
</p>

<h3 align="center">Device Intelligence SDK</h3>

<p align="center">
  Generates a stable device identifier that persists across sessions, tabs, and browsing modes.
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/@danetix/sentinel"><img src="https://img.shields.io/npm/v/@danetix/sentinel.svg" alt="npm"></a>
  <a href="https://www.npmjs.com/package/@danetix/sentinel"><img src="https://img.shields.io/npm/dm/@danetix/sentinel.svg" alt="downloads"></a>
  <a href="https://www.npmjs.com/package/@danetix/sentinel"><img src="https://img.shields.io/bundlephobia/minzip/@danetix/sentinel" alt="size"></a>
</p>

---

## Get Started

Create a free account at **[danetix.com](https://danetix.com)** to get your API key.

### NPM

```bash
npm install @danetix/sentinel
```

```js
import Sentinel from '@danetix/sentinel'

// Initialize at application startup
const stl = Sentinel.start({
  apiKey: 'your-api-key',
  endpoint: 'https://your-domain.com/ingest'
})

// Get the device identifier when you need it
const result = await stl.get()
console.log(result.deviceId) // → "Abs2d8F0gTk9l..."
```

### CDN

```html
<script>
  const stlPromise = import('https://your-domain.com/stl.esm.min.js')
    .then(S => S.start({
      apiKey: 'your-api-key',
      endpoint: '/ingest'
    }))

  stlPromise
    .then(stl => stl.get())
    .then(result => console.log(result.deviceId))
</script>
```

---

## Caching

Enable caching to avoid redundant requests in single-page applications:

```js
const stl = Sentinel.start({
  apiKey: 'your-api-key',
  endpoint: '/ingest',
  cache: {
    ttl: 300,                  // seconds
    location: 'sessionStorage' // or 'memory' (default), 'localStorage'
  }
})
```

```js
await stl.get()                        // → server request
await stl.get()                        // → instant (cached)
await stl.get({ ignoreCache: true })   // → force fresh request
stl.clearCache()                       // → invalidate manually
```

---

## API Reference

### `Sentinel.start(options)`

Returns a `SentinelInstance`.

| Parameter | Type | Required | Description |
|:----------|:-----|:---------|:------------|
| `apiKey` | `string` | Yes | Your API key |
| `endpoint` | `string` | Yes | Ingest endpoint URL |
| `cache.ttl` | `number` | — | Cache lifetime in seconds |
| `cache.location` | `string` | — | `'memory'` \| `'localStorage'` \| `'sessionStorage'` |

### `stl.get(options?)`

Returns `Promise<Result>`.

| Parameter | Type | Description |
|:----------|:-----|:------------|
| `ignoreCache` | `boolean` | Skip cache |
| `linkedId` | `string` | Link to your own user/session ID |
| `tag` | `object` | Attach custom metadata |

### Result

```js
{
  requestId: "abc123...",          // unique event ID
  deviceId: "Abs2d8F0gTk9l...",   // stable device identifier
  signedDeviceToken: "eyJ..."     // signed token for verification
}
```

---

## Browser Support

| | Chrome | Firefox | Safari | Edge | Samsung Internet |
|:-|:------:|:-------:|:------:|:----:|:----------------:|
| **Version** | 80+ | 113+ | 16.4+ | 80+ | 14+ |

---

<p align="center">
  <sub>Copyright &copy; 2026 Danetix. All rights reserved.</sub>
</p>
