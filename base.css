import { readFileSync, writeFileSync, mkdirSync } from "node:fs";
import { dirname, resolve } from "node:path";
import { fileURLToPath } from "node:url";

const root = resolve(dirname(fileURLToPath(import.meta.url)), "..");

// L'ordine conta: i token devono esistere prima di essere usati.
const files = [
  "src/tokens.css",
  "src/base.css",
  "src/components/layout.css",
  "src/components/button.css",
  "src/components/form.css",
  "src/components/data.css",
  "src/components/overlay.css",
];

const pkg = JSON.parse(readFileSync(resolve(root, "package.json"), "utf8"));

const banner = `/*! elixir-ui v${pkg.version} — design system Elixir Group. Non modificare dist/: si genera con "npm run build". */\n`;

const out = banner + files
  .map((f) => `\n/* ===== ${f} ===== */\n` + readFileSync(resolve(root, f), "utf8"))
  .join("\n");

mkdirSync(resolve(root, "dist"), { recursive: true });
writeFileSync(resolve(root, "dist/elixir-ui.css"), out);

console.log(`dist/elixir-ui.css — ${(out.length / 1024).toFixed(1)} kB`);
