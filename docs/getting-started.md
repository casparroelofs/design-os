# Getting Started

## Naming Convention

Name your design workspace after the product:

```bash
# Via GitHub template (recommended)
# 1. Go to https://github.com/casparroelofs/design-os
# 2. Click "Use this template"
# 3. Name it: [product-name]-design-os

# Clone locally
git clone git@github.com:YOUR_USERNAME/[product-name]-design-os.git
cd [product-name]-design-os
```

Examples:
- `animira-design-os` — Designing Animira
- `managed-databricks-design-os` — Designing Managed Databricks

Each product gets its own instance. Don't reuse instances for different products.

---

## Clone the Repository

If not using GitHub templates:

```bash
git clone https://github.com/buildermethods/design-os.git my-product-design-os
cd my-product-design-os
```

Replace `my-product` with your actual product name.

## Remove the Original Remote

```bash
git remote remove origin
```

Now you have a clean local instance ready to use.

## Install Dependencies

```bash
bun install
# or: npm install
```

## Start the Dev Server

```bash
bun run dev
# or: npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

## Open Claude Code

In the same project directory, start Claude Code:

```bash
claude
```

You're ready to start designing. Run `/design-os/product-vision` to begin defining your product.

---

## Optional: Save as Your Own Template

If you want to reuse Design OS for future projects:

1. Push to your own GitHub repository:

```bash
git remote add origin https://github.com/YOUR_USERNAME/design-os.git
git push -u origin main
```

2. Go to your repository on GitHub, click **Settings**, and check **Template repository**.

Now you can create new instances using GitHub's "Use this template" button.

---

## Multi-Product Workflow

Design OS follows a "one instance per product" model:

```
~/Development/Repos/
├── design-os/                    # Template repo (base tool, no product)
├── animira-design-os/            # Animira designs
└── managed-databricks-design-os/ # Future: another product
```

**For new products:**
1. Use GitHub template to create `[product-name]-design-os`
2. Clone locally
3. Run `/design-os/product-vision` to start

**Export destination:** Copy `product-plan/` folder to the actual product repo after `/design-os/export-product`.
