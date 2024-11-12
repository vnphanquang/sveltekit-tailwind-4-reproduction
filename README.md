# Svelte + Tailwind 4 - Postcss Usage Reproduction

> [!IMPORTANT]
> This project is bootstraped with [sv](https://github.com/sveltejs/cli), using its 'demo' template.

Steps:

1. Clone this repository
2. Install dependency `pnpm install`
3. Build `pnpm run build`


Observe output in terminal, for `svelte` file that contains a `style` tag:

```
[vite-plugin-svelte] [...truncated_path...]/*.svelte svelte.preprocess returned this file as a dependency of itself. This can be caused by an invalid configuration or importing generated code that depends on .svelte files (eg. tailwind base css)
```

and

```
[...truncated_path...]/*.svelte svelte.preprocess depends on more than 10 external files which can cause slow builds and poor DX, try to reduce them. Found: [list_of_all_source_files_except_raster_images]
```

## Changes made to the project after `sv` bootstrap

1. Add `tailwindcss` as a postcss plugin to `vite.config.ts`:

```diff
import { sveltekit } from "@sveltejs/kit/vite";
import { defineConfig } from "vite";
+ import tailwindcss from "@tailwindcss/postcss";

export default defineConfig({
+ css: {
+   postcss: {
+     plugins: [tailwindcss()],
+   },
+ },
  plugins: [sveltekit()],
});
```

2. Import `tailwindcss` to `src/app.css`:

```diff
+ @import 'tailwindcss';

/* truncated */
```
