To reproduce issue
---

1. Run `pnpm install && pnpm dev --turbo`
2. Open app in browser (https://localhost:3000)
3. Save any simple change to app/page.tsx (e.g. add a character literal to the output)

The app will crash with the following error:

    Error: Module [project]/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/esm/client/components/error-boundary.js [app-ssr] (ecmascript) was instantiated because it was required from module [project]/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/esm/build/templates/app-page.js?page=/page { COMPONENT_0 => "[project]/app/layout.tsx [app-rsc] (ecmascript, Next.js server component)", COMPONENT_1 => "[project]/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/client/components/not-found-error.js [app-rsc] (ecmascript, Next.js server component)", COMPONENT_2 => "[project]/app/page.tsx [app-rsc] (ecmascript, Next.js server component)", METADATA_3 => "[project]/app/favicon.ico.mjs { IMAGE => \"[project]/app/favicon.ico [app-rsc] (static)\" } [app-rsc] (structured image object, ecmascript)" } [app-rsc] (ecmascript) <locals>, but the module factory is not available. It might have been deleted in an HMR update.
        at instantiateModule (/nextjs-repro/.next/server/chunks/ssr/[turbopack]_runtime.js:492:15)
        at getOrInstantiateModuleFromParent (/nextjs-repro/.next/server/chunks/ssr/[turbopack]_runtime.js:572:12)
        at commonJsRequire (/nextjs-repro/.next/server/chunks/ssr/[turbopack]_runtime.js:136:20)
        at require (/nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:39:20088)
        at /nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:89292
        at eo (/nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:89477)
        at /nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:91706
        at Object._fromJSON (/nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:92262)
        at JSON.parse (<anonymous>)
        at eu (/nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:89971)
        at en (/nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:89039)
        at /nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:96197
        at /nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:96214
        at /nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:96247
        at /nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:96264
        at t (/nextjs-repro/node_modules/.pnpm/next@14.2.23_@babel+core@7.26.0_@opentelemetry+api@1.9.0_react-dom@18.3.1_react@18.3.1__react@18.3.1/node_modules/next/dist/compiled/next-server/app-page.runtime.dev.js:35:96487)
     ⨯     at instantiateModule (/nextjs-repro/.next/server/chunks/ssr/[turbopack]_runtime.js:492:15)
        at getOrInstantiateModuleFromParent (/nextjs-repro/.next/server/chunks/ssr/[turbopack]_runtime.js:572:12)
        at commonJsRequire (/nextjs-repro/.next/server/chunks/ssr/[turbopack]_runtime.js:136:20)
        at JSON.parse (<anonymous>)
    digest: "2437251089"

Misc
---

The boilerplate in this repo was seeded w/ `pnpx create-next-app@latest` + `pnpx @sentry/wizard@latest -i nextjs`.
