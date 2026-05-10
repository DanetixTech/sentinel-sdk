# @danetix/sentinel — distribution mirror

Этот репозиторий — **public mirror** распространения npm-пакета
[`@danetix/sentinel`](https://www.npmjs.com/package/@danetix/sentinel).
Здесь нет исходного кода SDK — только готовые production-бандлы,
которые публикуются на npm с verified provenance.

## Что здесь лежит

- `dist/stl.cjs.min.js` — CommonJS bundle
- `dist/stl.esm.min.js` — ES module bundle
- `dist/stl.min.js` — IIFE bundle (browser inline)
- `dist/stl.umd.min.js` — UMD bundle
- `package.json` — npm manifest
- `LICENSE`, `README.md` — обязательная мета

## Как сюда попадают артефакты

Build происходит в приватном репо `DanetixTech/sentinel` (там же src/,
tests/, rollup config). На каждый тег `v*` private workflow собирает
production-бандлы и пушит их сюда с тем же тегом. Затем уже здесь
срабатывает второй workflow (`.github/workflows/publish.yml`) и
выполняет `npm publish --access public --provenance` через
Trusted Publisher OIDC.

## Provenance

Каждая опубликованная версия `@danetix/sentinel` имеет
[provenance attestation](https://docs.npmjs.com/generating-provenance-statements)
с подписью через Sigstore. На странице пакета на npmjs.com рядом с
версией есть **Verified** badge → клик показывает source repo
(этот mirror) и workflow run, из которого собрана версия.

## Документация по самому SDK

См. `README.md` опубликованного npm-пакета:
<https://www.npmjs.com/package/@danetix/sentinel> — он подменяется на
production-документацию SDK во время mirror push.
