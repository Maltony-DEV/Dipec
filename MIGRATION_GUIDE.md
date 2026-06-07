# Setup and Migration Guide: React + Tailwind + TypeScript + shadcn

Since the current codebase is a static HTML project (`index.html`) using CDNs for Tailwind and Lucide Icons, this guide will walk you through migrating this project to a modern React stack with Tailwind CSS, TypeScript, and shadcn UI.

---

## 1. Setting Up the React + TypeScript Project

We recommend initializing a new project using Next.js (App Router) as it is the standard and most robust framework for React applications.

Run the following command in your terminal to initialize a new Next.js project with TypeScript and Tailwind CSS:

```bash
npx create-next-app@latest dipec-app --typescript --tailwind --eslint --app --src-dir=false --import-alias="@/*"
```
During the prompt, select the following options:
- **Would you like to use src/ directory?** No (this ensures files are created at the root level).
- **Would you like to use App Router?** Yes.
- **Would you like to customize the default import alias?** Yes (`@/*`).

Once initialized, navigate to the folder:
```bash
cd dipec-app
```

---

## 2. Installing shadcn UI CLI

Initialize shadcn in your project by running:

```bash
npx shadcn@latest init
```

You will be asked a few configuration questions. We recommend the following settings:
- **Style**: Default
- **Base color**: Slate
- **CSS variables for colors**: Yes
- **Where is your global CSS file?** `app/globals.css`
- **Do you want to use CSS variables for colors?** Yes
- **Where is your tailwind.config.js?** `tailwind.config.js`
- **Configure the import alias for components:** `@/components`
- **Configure the import alias for utils:** `@/lib/utils`
- **Are you using React Server Components?** Yes

This initializes a configuration file `components.json` at the root of your project.

---

## 3. Component & Style Paths

### Default Paths
- **Shadcn UI Components**: `components/ui/` (e.g. `@/components/ui/button`)
- **App Components**: `components/` (e.g. `@/components/custom-hero`)
- **Global Styles**: `app/globals.css` (Next.js) or `src/index.css` (Vite)

### Why is the `/components/ui` Folder Important?

1. **CLI Defaults**: The shadcn CLI is designed to automatically add UI primitives (like buttons, dialogs, dropdowns) into the `/components/ui` directory. If you change this path, you must update your `components.json` accordingly, which can lead to inconsistencies.
2. **Separation of Concerns**: Keeping generic, low-level UI elements (like `Button`, `Input`, `Dialog`) in `components/ui` separated from your domain-specific layout components (like `Header`, `Hero`, `Footer`) in `components/` keeps your import structure clean and highly organized.
3. **Automatic Maintenance**: Keeping shadcn primitives in their dedicated `ui` folder allows you to run `npx shadcn@latest add [component]` or update existing components without worrying about overwriting your own custom pages or business logic.

---

## 4. Copying the React Component

Copy the `ExpandingCards` component and the demo from this repository to your new Next.js project:

1. Copy [expanding-cards.tsx](file:///Users/usuario/Dipac_2.0/components/ui/expanding-cards.tsx) to `/components/ui/expanding-cards.tsx` in your new project.
2. Copy [demo.tsx](file:///Users/usuario/Dipac_2.0/components/ui/demo.tsx) to `/components/ui/demo.tsx` in your new project.

### Install Dependencies
In the new project root, run:
```bash
npm install lucide-react clsx tailwind-merge
```
*(Note: `lucide-react` is used for icons, and `clsx` + `tailwind-merge` are utilized by shadcn's helper utility `cn` located in `lib/utils.ts` to coordinate conditional class merges.)*

---

## 5. Integrating the Component

To render the `ExpandingCardsDemo` on your home page, modify `app/page.tsx` in your Next.js project:

```tsx
import ExpandingCardsDemo from "@/components/ui/demo";

export default function Home() {
  return (
    <main class="min-h-screen bg-black">
      <ExpandingCardsDemo />
    </main>
  );
}
```
Now, start the dev server:
```bash
npm run dev
```
And view your interactive expanding cards at `http://localhost:3000`!
