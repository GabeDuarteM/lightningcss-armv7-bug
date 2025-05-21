1. Setup docker multi-arch buildx if you don't have it already

```bash
docker buildx create --name multiarch-builder --driver docker-container --bootstrap
docker buildx use multiarch-builder
```

2. Run the following to build the image on both architectures

```sh
$ docker buildx build \
  --platform linux/arm/v6,linux/arm/v7 \
  .
```

3. The above should give you the following error:

```sh
 > [linux/arm/v7 builder 3/3] RUN --mount=type=cache,id=pnpm,target=/pnpm/store pnpm build:
8.643 ! Corepack is about to download https://registry.npmjs.org/pnpm/-/pnpm-10.11.0.tgz
11.31 ! The local project doesn't define a 'packageManager' field. Corepack will now add one referencing pnpm@10.11.0+sha512.6540583f41cc5f628eb3d9773ecee802f4f9ef9923cc45b69890fb47991d4b092964694ec3a4f738a420c918a333062c8b925d312f42e4f0c263eb603551f977.
11.31 ! For more details about this field, consult the documentation at https://nodejs.org/api/packages.html#packagemanager
11.31
13.98
13.98 > lightningcss-armv7@0.1.0 build /app
13.98 > next build
13.98
24.85    Downloading swc package @next/swc-wasm-nodejs... to /root/.cache/next-swc
50.42 Attention: Next.js now collects completely anonymous telemetry regarding usage.
50.42 This information is used to shape Next.js' roadmap and prioritize features.
50.42 You can learn more, including how to opt-out if you'd not like to participate in this anonymous program, by visiting the following URL:
50.42 https://nextjs.org/telemetry
50.42
50.95    ▲ Next.js 15.3.2
50.95
51.06    Creating an optimized production build ...
83.25
83.25
83.25 Retrying 1/3...
83.26
83.26
83.26 Retrying 1/3...
83.27
83.27
83.27 Retrying 1/3...
83.28
83.28
83.28 Retrying 1/3...
83.29
83.29
83.29 Retrying 1/3...
83.29
83.29
83.29 Retrying 1/3...
99.77 Failed to compile.
99.77
99.77 src/app/layout.tsx
99.77 An error occurred in `next/font`.
99.77
99.77 Error: Cannot find module '../lightningcss.linux-arm-musl.node'
99.77 Require stack:
99.77 - /app/node_modules/.pnpm/lightningcss@1.30.1/node_modules/lightningcss/node/index.js
99.77 - /app/node_modules/.pnpm/@tailwindcss+node@4.1.7/node_modules/@tailwindcss/node/dist/index.js
99.77 - /app/node_modules/.pnpm/@tailwindcss+postcss@4.1.7/node_modules/@tailwindcss/postcss/dist/index.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack/config/blocks/css/plugins.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack/config/blocks/css/index.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack/config/index.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack-config.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack-build/impl.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/compiled/jest-worker/processChild.js
99.77     at Module._resolveFilename (node:internal/modules/cjs/loader:1212:15)
99.77     at /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/server/require-hook.js:55:36
99.77     at Module._load (node:internal/modules/cjs/loader:1043:27)
99.77     at Module.require (node:internal/modules/cjs/loader:1298:19)
99.77     at mod.require (/app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/server/require-hook.js:65:28)
99.77     at require (node:internal/modules/helpers:182:18)
99.77     at Object.<anonymous> (/app/node_modules/.pnpm/lightningcss@1.30.1/node_modules/lightningcss/node/index.js:22:22)
99.77     at Module._compile (node:internal/modules/cjs/loader:1529:14)
99.77     at Module._extensions..js (node:internal/modules/cjs/loader:1613:10)
99.77     at Module.load (node:internal/modules/cjs/loader:1275:32)
99.77
99.77 src/app/layout.tsx
99.77 An error occurred in `next/font`.
99.77
99.77 Error: Cannot find module '../lightningcss.linux-arm-musl.node'
99.77 Require stack:
99.77 - /app/node_modules/.pnpm/lightningcss@1.30.1/node_modules/lightningcss/node/index.js
99.77 - /app/node_modules/.pnpm/@tailwindcss+node@4.1.7/node_modules/@tailwindcss/node/dist/index.js
99.77 - /app/node_modules/.pnpm/@tailwindcss+postcss@4.1.7/node_modules/@tailwindcss/postcss/dist/index.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack/config/blocks/css/plugins.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack/config/blocks/css/index.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack/config/index.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack-config.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/build/webpack-build/impl.js
99.77 - /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/compiled/jest-worker/processChild.js
99.77     at Module._resolveFilename (node:internal/modules/cjs/loader:1212:15)
99.77     at /app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/server/require-hook.js:55:36
99.77     at Module._load (node:internal/modules/cjs/loader:1043:27)
99.77     at Module.require (node:internal/modules/cjs/loader:1298:19)
99.77     at mod.require (/app/node_modules/.pnpm/next@15.3.2_react-dom@19.1.0_react@19.1.0__react@19.1.0/node_modules/next/dist/server/require-hook.js:65:28)
99.77     at require (node:internal/modules/helpers:182:18)
99.77     at Object.<anonymous> (/app/node_modules/.pnpm/lightningcss@1.30.1/node_modules/lightningcss/node/index.js:22:22)
99.77     at Module._compile (node:internal/modules/cjs/loader:1529:14)
99.77     at Module._extensions..js (node:internal/modules/cjs/loader:1613:10)
99.77     at Module.load (node:internal/modules/cjs/loader:1275:32)
99.77
100.1
100.1 > Build failed because of webpack errors
100.3  ELIFECYCLE  Command failed with exit code 1.
------
WARNING: No output specified with docker-container driver. Build result will only remain in the build cache. To push result image into registry use --push or to load image into docker use --load
Dockerfile:14
--------------------
  12 |     COPY --from=deps /app/node_modules ./node_modules
  13 |     COPY . .
  14 | >>> RUN --mount=type=cache,id=pnpm,target=/pnpm/store pnpm build
  15 |
  16 |     FROM base AS runner
--------------------
ERROR: failed to solve: process "/dev/.buildkit_qemu_emulator /bin/sh -c pnpm build" did not complete successfully: exit code: 1
```
