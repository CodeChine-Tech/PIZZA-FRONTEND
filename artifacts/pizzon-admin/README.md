# Pizzon Admin Panel

Full admin panel to **control the entire website**: orders, dispatch, riders, menu, content, settings, coupons, and users. **Not linked from the customer website** — no nav button or link to this panel; only staff with the URL can access it.

## Run locally

From repo root:

```bash
pnpm run start:admin
# or
pnpm run dev:admin
```

Opens at **http://localhost:5174**

## Login

- Any username (and any password) signs you in for demo.
- Replace with real auth (e.g. backend `/api/auth/login`) when integrating.

## Sidebar & routes (after login)

- **Dashboard** (`/`) — Overview, stats, recent orders
- **Orders** (`/orders`) — Orders list, assign rider, view, invoice, track
- **Order detail** (`/orders/:id`) — Status, customer, items, assign rider, invoice
- **Track** (`/track`) — Live rider map
- **Riders** (`/riders`) — Riders list, add/edit
- **Menu & Products** (`/menu`) — Categories and items (controls website menu)
- **Content** — About, Blog, Team, Specials, Gallery, Testimonials, Contact, Reservation (controls each section on the website)
- **Coupons** (`/coupons`) — Discount codes for checkout
- **Settings** (`/settings`) — Store info, hours, tax, delivery
- **Users** (`/users`) — Panel users (admin/staff)

No animations. Backend integration can replace mock data and wire save actions later.

## Deploy to Vercel

Deploy the admin as a **second Vercel project** from the same repo.

### Option A – Monorepo (recommended)

1. In Vercel: **Add New Project** → import the same repo.
2. Set **Root Directory** to **empty** (repo root).
3. Override:
   - **Build Command:** `pnpm install && pnpm run build:admin`
   - **Output Directory:** `artifacts/pizzon-admin/dist/public`
   - **Install Command:** `pnpm install`
4. Deploy. The admin will get its own URL (e.g. `pizzon-admin-xxx.vercel.app`).

### Option B – Subfolder as root

1. In Vercel: **Add New Project** → import the same repo.
2. Set **Root Directory** to `artifacts/pizzon-admin`.
3. Use default Build and Install; **Output Directory** is already `dist/public` in `vercel.json`.
4. Deploy.

### After deploy

- In your **customer** Vercel project, add env var **`VITE_ADMIN_URL`** = your admin URL (e.g. `https://pizzon-admin-xxx.vercel.app`). Then `yoursite.com/admin` will redirect to the admin app.
- Use a custom domain for the admin (e.g. `admin.yourdomain.com`) in the admin project’s Vercel settings if you want.
