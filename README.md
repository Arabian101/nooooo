package.json
netlify.toml
vite.config.ts
tsconfig.json
.gitignore
src/styles.css
src/router.tsx
src/routes/__root.tsx
src/routes/index.tsx
src/routes/winkel.tsx
src/routes/producten/$slug.tsx
src/routes/vakmanschap.tsx
src/routes/contact.tsx
src/routes/checkout/success.tsx
src/routes/checkout/cancel.tsx
src/components/Header.tsx
src/components/Footer.tsx
src/components/Logo.tsx
src/components/ProductCard.tsx
src/components/CartDrawer.tsx
src/data/products.ts
src/lib/cart.tsx
src/lib/format.ts
src/lib/stripe.ts
public/contact-form.html
package.json
{
  "name": "jaegerscissors",
  "private": true,
  "type": "module",
  "scripts": {
    "dev": "vite dev --port 3000",
    "build": "vite build"
  },
  "dependencies": {
    "@tailwindcss/vite": "4.2.2",
    "@tanstack/react-router": "1.170.40",
    "@tanstack/react-start": "1.168.60",
    "@tanstack/router-plugin": "1.168.41",
    "highlight.js": "11.11.1",
    "lucide-react": "0.576.0",
    "react": "19.2.8",
    "react-dom": "19.2.8",
    "stripe": "20.4.1",
    "tailwindcss": "4.2.2",
    "vite-tsconfig-paths": "6.1.1",
    "zod": "4.3.6"
  },
  "devDependencies": {
    "@netlify/vite-plugin-tanstack-start": "1.3.19",
    "@tailwindcss/vite": "4.2.2",
    "@types/node": "22.20.5",
    "@types/react": "19.2.18",
    "@types/react-dom": "19.2.5",
    "@vitejs/plugin-react": "5.2.0",
    "lucide-react": "0.576.0",
    "tailwindcss": "4.2.2",
    "typescript": "5.9.3",
    "rimraf": "6.1.3",
    "vite": "7.3.6"
  }
}

netlify.toml
[build]
  command = "vite build"
  publish = "dist/client"
[dev]
  command = "npm run dev"
  targetPort = 3000
  port = 8888

vite.config.ts
import { defineConfig } from 'vite'
import { tanstackStart } from '@tanstack/react-start/plugin/vite'
import viteReact from '@vitejs/plugin-react'
import viteTsConfigPaths from 'vite-tsconfig-paths'
import tailwindcss from '@tailwindcss/vite'
import netlify from '@netlify/vite-plugin-tanstack-start'

const config = defineConfig({
  plugins: [
    viteTsConfigPaths({
      projects: ['./tsconfig.json'],
    }),
    tailwindcss(),
    netlify(),
    tanstackStart(),
    viteReact(),
  ],
})

export default config

tsconfig.json
{
  "include": ["**/*.ts", "**/*.tsx"],
  "compilerOptions": {
    "target": "ES2022",
    "jsx": "react-jsx",
    "module": "ESNext",
    "lib": ["ES2022", "DOM", "DOM.Iterable"],
    "types": ["vite/client"],

    /* Bundler mode */
    "moduleResolution": "bundler",
    "allowImportingTsExtensions": true,
    "verbatimModuleSyntax": false,
    "noEmit": true,

    /* Linting */
    "skipLibCheck": true,
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noFallthroughCasesInSwitch": true,
    "noUncheckedSideEffectImports": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}

.gitignore
node_modules
.DS_Store
dist
dist-ssr
*.local
.env
.netlify
.tanstack

src/styles.css
@import "tailwindcss" source("../");

@theme {
  --font-display: 'Cormorant Garamond', 'Times New Roman', serif;
  --font-sans: 'Manrope', system-ui, -apple-system, sans-serif;

  --color-ink: #0b0b0c;
  --color-coal: #141416;
  --color-graphite: #1d1d20;
  --color-steel: #8a8a90;
  --color-ivory: #f3efe7;
  --color-brass: #c9a227;
  --color-brass-light: #e3c766;
}

html {
  scroll-behavior: smooth;
}

body {
  margin: 0;
  background: var(--color-ink);
  color: var(--color-ivory);
  font-family: var(--font-sans);
  -webkit-font-smoothing: antialiased;
}

::selection {
  background: var(--color-brass);
  color: var(--color-ink);
}

.eyebrow {
  font-size: 0.7rem;
  letter-spacing: 0.32em;
  text-transform: uppercase;
  color: var(--color-brass);
  font-weight: 600;
}

.hairline {
  border-color: rgb(243 239 231 / 0.1);
}

.btn-brass {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.6rem;
  background: var(--color-brass);
  color: var(--color-ink);
  padding: 0.95rem 1.75rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  transition: background 0.25s ease, transform 0.25s ease;
}
.btn-brass:hover {
  background: var(--color-brass-light);
}
.btn-brass:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn-ghost {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.6rem;
  border: 1px solid rgb(243 239 231 / 0.25);
  padding: 0.95rem 1.75rem;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  transition: border-color 0.25s ease, color 0.25s ease;
}
.btn-ghost:hover {
  border-color: var(--color-brass);
  color: var(--color-brass-light);
}

.grain::after {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;
  opacity: 0.06;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}

@keyframes rise {
  from {
    opacity: 0;
    transform: translateY(18px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
.rise {
  animation: rise 0.9s cubic-bezier(0.2, 0.7, 0.2, 1) both;
}

@keyframes slide-in {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(0);
  }
}
.slide-in {
  animation: slide-in 0.35s cubic-bezier(0.2, 0.7, 0.2, 1) both;
}

src/router.tsx
import { createRouter } from '@tanstack/react-router'

// Import the generated route tree
import { routeTree } from './routeTree.gen'

// Create a new router instance
export const getRouter = () => {
  const router = createRouter({
    routeTree,
    scrollRestoration: true,
    defaultPreloadStaleTime: 0,
  })

  return router
}

src/routes/__root.tsx
import { HeadContent, Link, Scripts, createRootRoute } from '@tanstack/react-router'
import { CartDrawer } from '@/components/CartDrawer'
import { Footer } from '@/components/Footer'
import { Header } from '@/components/Header'
import { CartProvider } from '@/lib/cart'

import '../styles.css'

const siteName = 'JAEGERscissors.nl — Premium barberscharen'
const siteDescription =
  'Professionele high-end barberscharen van Japans staal. Handgeslepen, levenslange slijpservice en gratis verzending in Nederland en België.'

export const Route = createRootRoute({
  head: () => ({
    meta: [
      {
        charSet: 'utf-8',
      },
      {
        name: 'viewport',
        content: 'width=device-width, initial-scale=1',
      },
      {
        title: siteName,
      },
      {
        name: 'description',
        content: siteDescription,
      },
      {
        name: 'theme-color',
        content: '#0b0b0c',
      },
      {
        property: 'og:title',
        content: siteName,
      },
      {
        property: 'og:description',
        content: siteDescription,
      },
      {
        property: 'og:type',
        content: 'website',
      },
      {
        property: 'og:image',
        content: '/.netlify/images?url=/img/hero.png&w=1200&fm=jpg',
      },
      {
        name: 'twitter:card',
        content: 'summary_large_image',
      },
    ],
    links: [
      { rel: 'preconnect', href: 'https://fonts.googleapis.com' },
      { rel: 'preconnect', href: 'https://fonts.gstatic.com', crossOrigin: 'anonymous' },
      {
        rel: 'stylesheet',
        href: 'https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,400;1,500&family=Manrope:wght@400;500;600;700&display=swap',
      },
    ],
  }),
  shellComponent: RootDocument,
  notFoundComponent: NotFound,
})

function RootDocument({ children }: { children: React.ReactNode }) {
  return (
    <html lang="nl">
      <head>
        <HeadContent />
      </head>
      <body>
        <CartProvider>
          <Header />
          <main>{children}</main>
          <Footer />
          <CartDrawer />
        </CartProvider>
        <Scripts />
      </body>
    </html>
  )
}

function NotFound() {
  return (
    <div className="max-w-xl mx-auto px-5 py-40 text-center">
      <p className="eyebrow">404</p>
      <h1 className="font-display text-5xl mt-4">Deze pagina is weggeknipt</h1>
      <p className="mt-4 text-ivory/60">
        De pagina die je zoekt bestaat niet (meer).
      </p>
      <Link to="/winkel" className="btn-brass mt-10">
        Naar de collectie
      </Link>
    </div>
  )
}

src/routes/index.tsx
import { Link, createFileRoute } from '@tanstack/react-router'
import { ArrowRight, Award, RefreshCcw, ShieldCheck, Truck } from 'lucide-react'
import { ProductCard } from '@/components/ProductCard'
import products from '@/data/products'
import { formatEuro, img } from '@/lib/format'

export const Route = createFileRoute('/')({
  component: Home,
})

const featured = products.filter((p) =>
  ['kaiser-6-0', 'jaeger-7-0', 'wolf-effileer-6-0'].includes(p.slug),
)
const limited = products.find((p) => p.slug === 'damast-6-5')!

const usps = [
  { icon: Award, title: 'Japans staal', text: 'VG-10, ATS-314 en damast tot 62 HRC' },
  { icon: RefreshCcw, title: 'Levenslang slijpen', text: 'Eerste beurt gratis, daarna vaste prijs' },
  { icon: Truck, title: 'Gratis verzending', text: 'Verzekerd, binnen 1–2 werkdagen' },
  { icon: ShieldCheck, title: '5 jaar garantie', text: 'Op materiaal- en productiefouten' },
]

const reviews = [
  {
    quote:
      'Na tien jaar knippen dacht ik dat een schaar een schaar was. De Kaiser bewees het tegendeel — geen trekken, geen pijn in mijn pols.',
    name: 'Mehmet K.',
    shop: 'Barbershop Oost, Amsterdam',
  },
  {
    quote:
      'De Jäger 7.0 is gemaakt voor schaar-over-kam. Lange, rustige halen en het blad blijft ongelooflijk lang scherp.',
    name: 'Sanne de V.',
    shop: 'Kapsalon Nobel, Utrecht',
  },
  {
    quote:
      'Mijn hele team werkt inmiddels met JAEGER. De slijpservice is snel en de scharen komen terug alsof ze nieuw zijn.',
    name: 'Rico B.',
    shop: 'The Gentleman’s Cut, Rotterdam',
  },
]

function Home() {
  return (
    <>
      {/* Hero */}
      <section className="relative overflow-hidden grain">
        <img
          src={img('/img/hero.png', 1920)}
          alt="JAEGER barberschaar op leisteen"
          width={1584}
          height={672}
          fetchPriority="high"
          className="absolute inset-0 w-full h-full object-cover object-[70%_center] opacity-80"
        />
        <div className="absolute inset-0 bg-gradient-to-r from-ink via-ink/80 to-transparent" />
        <div className="absolute inset-x-0 bottom-0 h-40 bg-gradient-to-t from-ink to-transparent" />
        <div className="relative max-w-7xl mx-auto px-5 md:px-8 min-h-[78vh] flex items-center py-24">
          <div className="max-w-xl">
            <p className="eyebrow rise">Professionele barberscharen</p>
            <h1
              className="rise font-display text-6xl md:text-8xl leading-[0.95] mt-6"
              style={{ animationDelay: '0.1s' }}
            >
              Precisie die je <em className="text-brass not-italic md:italic">voelt</em>.
            </h1>
            <p
              className="rise mt-8 text-lg text-ivory/70 leading-relaxed max-w-md"
              style={{ animationDelay: '0.2s' }}
            >
              Handgeslepen scharen van Japans kobaltstaal, ontworpen met en voor
              barbers. Voor elke fade, elke lijn, elke dag.
            </p>
            <div
              className="rise mt-10 flex flex-wrap gap-4"
              style={{ animationDelay: '0.3s' }}
            >
              <Link to="/winkel" className="btn-brass">
                Shop de collectie <ArrowRight size={16} />
              </Link>
              <Link to="/vakmanschap" className="btn-ghost">
                Ons vakmanschap
              </Link>
            </div>
          </div>
        </div>
      </section>

      {/* USPs */}
      <section className="border-y hairline bg-coal">
        <div className="max-w-7xl mx-auto px-5 md:px-8 grid grid-cols-2 lg:grid-cols-4">
          {usps.map(({ icon: Icon, title, text }) => (
            <div key={title} className="flex gap-4 py-8 px-2 md:px-6 items-start">
              <Icon className="text-brass shrink-0 mt-0.5" size={22} strokeWidth={1.5} />
              <div>
                <p className="text-sm font-semibold">{title}</p>
                <p className="text-xs text-ivory/50 mt-1">{text}</p>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* Featured */}
      <section className="max-w-7xl mx-auto px-5 md:px-8 pt-28">
        <div className="flex items-end justify-between gap-6 mb-12">
          <div>
            <p className="eyebrow">De collectie</p>
            <h2 className="font-display text-4xl md:text-5xl mt-3">
              Gekozen door barbers
            </h2>
          </div>
          <Link
            to="/winkel"
            className="hidden md:inline-flex items-center gap-2 text-xs font-bold tracking-[0.2em] uppercase text-brass hover:text-brass-light"
          >
            Alle scharen <ArrowRight size={14} />
          </Link>
        </div>
        <div className="grid gap-x-8 gap-y-14 md:grid-cols-3">
          {featured.map((product) => (
            <ProductCard key={product.slug} product={product} />
          ))}
        </div>
      </section>

      {/* Limited edition */}
      <section className="max-w-7xl mx-auto px-5 md:px-8 pt-32">
        <div className="grid lg:grid-cols-12 bg-coal border hairline">
          <div className="lg:col-span-7 relative min-h-80">
            <img
              src={img(limited.image, 1200)}
              alt="JAEGER Damast 6.5 limited edition"
              loading="lazy"
              className="absolute inset-0 w-full h-full object-cover"
            />
          </div>
          <div className="lg:col-span-5 p-10 md:p-14 flex flex-col justify-center">
            <p className="eyebrow">Limited edition · 250 stuks</p>
            <h2 className="font-display text-5xl mt-4">{limited.name}</h2>
            <p className="mt-5 text-ivory/65 leading-relaxed">
              {limited.shortDescription}
            </p>
            <dl className="mt-8 grid grid-cols-2 gap-6 text-sm">
              <div>
                <dt className="text-steel text-xs uppercase tracking-[0.2em]">Staal</dt>
                <dd className="mt-1">{limited.steel}</dd>
              </div>
              <div>
                <dt className="text-steel text-xs uppercase tracking-[0.2em]">Hardheid</dt>
                <dd className="mt-1">{limited.hardness}</dd>
              </div>
            </dl>
            <div className="mt-10 flex items-center gap-6">
              <Link
                to="/producten/$slug"
                params={{ slug: limited.slug }}
                className="btn-brass"
              >
                Ontdek de Damast
              </Link>
              <span className="font-display text-2xl">{formatEuro(limited.price)}</span>
            </div>
          </div>
        </div>
      </section>

      {/* Craft story */}
      <section className="max-w-7xl mx-auto px-5 md:px-8 pt-32 grid md:grid-cols-2 gap-14 items-center">
        <div className="relative">
          <img
            src={img('/img/craft.png', 900, 1100)}
            alt="Vakman slijpt een schaarblad op een wetsteen"
            loading="lazy"
            width={900}
            height={1100}
            className="w-full aspect-[9/11] object-cover"
          />
          <div className="absolute -bottom-6 -right-6 hidden md:block bg-brass text-ink p-6 max-w-[12rem]">
            <p className="font-display text-5xl leading-none">48</p>
            <p className="text-xs font-semibold uppercase tracking-[0.15em] mt-2">
              handelingen per schaar
            </p>
          </div>
        </div>
        <div>
          <p className="eyebrow">Vakmanschap</p>
          <h2 className="font-display text-4xl md:text-5xl mt-3 leading-tight">
            Geslepen met de hand. Getest in de stoel.
          </h2>
          <p className="mt-6 text-ivory/65 leading-relaxed">
            Elke JAEGER-schaar doorloopt 48 handelingen voordat hij ons atelier
            verlaat. Het convexe blad wordt met de hand op Japanse wetstenen
            geslepen, de spanning ingesteld en elk exemplaar wordt getest op
            nat en droog haar.
          </p>
          <p className="mt-4 text-ivory/65 leading-relaxed">
            En daarna stopt onze zorg niet: met de levenslange slijpservice blijft
            je schaar net zo scherp als op dag één.
          </p>
          <Link to="/vakmanschap" className="btn-ghost mt-10">
            Lees ons verhaal
          </Link>
        </div>
      </section>

      {/* Reviews */}
      <section className="max-w-7xl mx-auto px-5 md:px-8 pt-36">
        <div className="text-center max-w-2xl mx-auto">
          <p className="eyebrow">Uit de barbershop</p>
          <h2 className="font-display text-4xl md:text-5xl mt-3">
            Professionals over JAEGER
          </h2>
        </div>
        <div className="mt-14 grid md:grid-cols-3 gap-6">
          {reviews.map((r) => (
            <figure key={r.name} className="border hairline p-8 bg-coal/50">
              <div className="text-brass tracking-[0.3em] text-sm" aria-label="5 sterren">
                ★★★★★
              </div>
              <blockquote className="mt-5 font-display text-xl leading-snug text-ivory/90">
                “{r.quote}”
              </blockquote>
              <figcaption className="mt-6 text-sm">
                <span className="font-semibold">{r.name}</span>
                <span className="block text-ivory/45 text-xs mt-1">{r.shop}</span>
              </figcaption>
            </figure>
          ))}
        </div>
      </section>

      {/* CTA */}
      <section className="max-w-7xl mx-auto px-5 md:px-8 pt-32">
        <div className="relative overflow-hidden grain">
          <img
            src={img('/img/barber.png', 1600)}
            alt="Barber knipt met schaar over kam"
            loading="lazy"
            className="absolute inset-0 w-full h-full object-cover"
          />
          <div className="absolute inset-0 bg-ink/75" />
          <div className="relative px-8 py-24 md:py-32 text-center max-w-2xl mx-auto">
            <h2 className="font-display text-4xl md:text-6xl">
              Niet zeker welke schaar bij je past?
            </h2>
            <p className="mt-5 text-ivory/70">
              Onze adviseurs zijn zelf barber. Vertel ons hoe je knipt en we
              adviseren je persoonlijk — vrijblijvend.
            </p>
            <div className="mt-10 flex flex-wrap gap-4 justify-center">
              <Link to="/contact" className="btn-brass">
                Vraag advies
              </Link>
              <Link to="/winkel" className="btn-ghost">
                Vergelijk modellen
              </Link>
            </div>
          </div>
        </div>
      </section>
    </>
  )
}

src/routes/winkel.tsx
import { Link, createFileRoute } from '@tanstack/react-router'
import { ProductCard } from '@/components/ProductCard'
import products, { type Category, categoryLabels } from '@/data/products'

type Sort = 'aanbevolen' | 'prijs-laag' | 'prijs-hoog'

interface ShopSearch {
  categorie?: Category
  sorteer?: Sort
}

const sortLabels: Record<Sort, string> = {
  aanbevolen: 'Aanbevolen',
  'prijs-laag': 'Prijs: laag – hoog',
  'prijs-hoog': 'Prijs: hoog – laag',
}

export const Route = createFileRoute('/winkel')({
  validateSearch: (search: Record<string, unknown>): ShopSearch => ({
    categorie:
      typeof search.categorie === 'string' && search.categorie in categoryLabels
        ? (search.categorie as Category)
        : undefined,
    sorteer:
      typeof search.sorteer === 'string' && search.sorteer in sortLabels
        ? (search.sorteer as Sort)
        : undefined,
  }),
  head: () => ({
    meta: [{ title: 'Collectie — JAEGERscissors.nl' }],
  }),
  component: Shop,
})

function Shop() {
  const { categorie, sorteer = 'aanbevolen' } = Route.useSearch()
  const navigate = Route.useNavigate()

  const visible = products
    .filter((p) => !categorie || p.category === categorie)
    .sort((a, b) =>
      sorteer === 'prijs-laag'
        ? a.price - b.price
        : sorteer === 'prijs-hoog'
          ? b.price - a.price
          : 0,
    )

  const filters: Array<{ value?: Category; label: string }> = [
    { value: undefined, label: 'Alles' },
    ...(Object.keys(categoryLabels) as Array<Category>).map((value) => ({
      value,
      label: categoryLabels[value],
    })),
  ]

  return (
    <div className="max-w-7xl mx-auto px-5 md:px-8 pt-16">
      <header className="max-w-2xl">
        <p className="eyebrow">Collectie</p>
        <h1 className="font-display text-5xl md:text-6xl mt-3">
          {categorie ? categoryLabels[categorie] : 'Alle barberscharen'}
        </h1>
        <p className="mt-5 text-ivory/60 leading-relaxed">
          Iedere schaar wordt met de hand geslepen en geleverd met lederen etui,
          onderhoudsset en levenslange slijpservice.
        </p>
      </header>

      <div className="mt-12 flex flex-col sm:flex-row gap-6 sm:items-center justify-between border-y hairline py-5">
        <div className="flex flex-wrap gap-2">
          {filters.map((f) => {
            const active = f.value === categorie
            return (
              <Link
                key={f.label}
                to="/winkel"
                search={(prev) => ({ ...prev, categorie: f.value })}
                className={`px-4 py-2 text-[0.7rem] font-bold tracking-[0.18em] uppercase border transition-colors ${
                  active
                    ? 'bg-ivory text-ink border-ivory'
                    : 'border-ivory/20 text-ivory/70 hover:border-brass hover:text-ivory'
                }`}
              >
                {f.label}
              </Link>
            )
          })}
        </div>
        <label className="flex items-center gap-3 text-xs text-ivory/60">
          Sorteer
          <select
            value={sorteer}
            onChange={(e) =>
              navigate({
                search: (prev) => ({
                  ...prev,
                  sorteer: e.target.value === 'aanbevolen' ? undefined : (e.target.value as Sort),
                }),
              })
            }
            className="bg-coal border hairline px-3 py-2 text-ivory text-sm focus:outline-none focus:border-brass"
          >
            {(Object.keys(sortLabels) as Array<Sort>).map((s) => (
              <option key={s} value={s}>
                {sortLabels[s]}
              </option>
            ))}
          </select>
        </label>
      </div>

      <p className="mt-6 text-xs text-steel">
        {visible.length} {visible.length === 1 ? 'product' : 'producten'}
      </p>

      <div className="mt-8 grid gap-x-8 gap-y-16 sm:grid-cols-2 lg:grid-cols-3">
        {visible.map((product) => (
          <ProductCard key={product.slug} product={product} />
        ))}
      </div>
    </div>
  )
}

src/routes/producten/$slug.tsx
import { Link, createFileRoute, notFound } from '@tanstack/react-router'
import { Check, ChevronLeft, Minus, Plus, RefreshCcw, ShieldCheck, Truck } from 'lucide-react'
import { useState } from 'react'
import { ProductCard } from '@/components/ProductCard'
import products, { categoryLabels, getProduct } from '@/data/products'
import { MAX_QUANTITY, useCart } from '@/lib/cart'
import { formatEuro, img } from '@/lib/format'

export const Route = createFileRoute('/producten/$slug')({
  loader: ({ params }) => {
    const product = getProduct(params.slug)
    if (!product) throw notFound()
    return product
  },
  head: ({ loaderData }) => ({
    meta: loaderData
      ? [
          { title: `JAEGER ${loaderData.name} — JAEGERscissors.nl` },
          { name: 'description', content: loaderData.shortDescription },
          { property: 'og:image', content: img(loaderData.image, 1200) },
        ]
      : [],
  }),
  component: ProductPage,
})

function ProductPage() {
  const product = Route.useLoaderData()
  const { add } = useCart()
  const [quantity, setQuantity] = useState(1)

  const specs = [
    ['Lengte', product.size],
    ['Staal', product.steel],
    ['Hardheid', product.hardness],
    ['Greep', product.handle],
    ['Snede', product.edge],
  ]

  const related = products.filter((p) => p.slug !== product.slug).slice(0, 3)

  return (
    <div className="max-w-7xl mx-auto px-5 md:px-8 pt-10">
      <nav className="text-xs text-ivory/50 flex items-center gap-2">
        <Link to="/winkel" className="inline-flex items-center gap-1 hover:text-ivory">
          <ChevronLeft size={14} /> Collectie
        </Link>
        <span>/</span>
        <Link
          to="/winkel"
          search={{ categorie: product.category }}
          className="hover:text-ivory"
        >
          {categoryLabels[product.category]}
        </Link>
      </nav>

      <div className="mt-8 grid lg:grid-cols-12 gap-12">
        <div className="lg:col-span-7">
          <div className="relative bg-coal overflow-hidden">
            <img
              src={img(product.image, 1400)}
              alt={`JAEGER ${product.name}`}
              className="w-full aspect-[4/3] object-cover"
            />
            {product.badge && (
              <span className="absolute top-5 left-5 bg-ink/80 border border-brass/40 text-brass text-[0.62rem] font-bold tracking-[0.2em] uppercase px-3 py-1.5">
                {product.badge}
              </span>
            )}
          </div>
        </div>

        <div className="lg:col-span-5">
          <p className="eyebrow">{categoryLabels[product.category]}</p>
          <h1 className="font-display text-5xl md:text-6xl mt-3">{product.name}</h1>
          <p className="mt-2 text-ivory/60">{product.tagline}</p>

          <p className="mt-8 font-display text-4xl">{formatEuro(product.price)}</p>
          <p className="text-xs text-ivory/45 mt-1">Incl. 21% btw · gratis verzending</p>

          <p className="mt-8 text-ivory/75 leading-relaxed">{product.description}</p>

          <div className="mt-10 flex gap-3">
            <div className="flex items-center border border-ivory/20">
              <button
                className="px-4 h-full hover:text-brass disabled:opacity-30"
                onClick={() => setQuantity((q) => Math.max(1, q - 1))}
                disabled={quantity <= 1}
                aria-label="Minder"
              >
                <Minus size={16} />
              </button>
              <span className="w-8 text-center">{quantity}</span>
              <button
                className="px-4 h-full hover:text-brass disabled:opacity-30"
                onClick={() => setQuantity((q) => Math.min(MAX_QUANTITY, q + 1))}
                disabled={quantity >= MAX_QUANTITY}
                aria-label="Meer"
              >
                <Plus size={16} />
              </button>
            </div>
            <button
              onClick={() => {
                add(product.slug, quantity)
                setQuantity(1)
              }}
              className="btn-brass flex-1"
            >
              In winkelwagen
            </button>
          </div>

          <ul className="mt-8 space-y-3">
            {product.features.map((f) => (
              <li key={f} className="flex gap-3 text-sm text-ivory/80">
                <Check size={16} className="text-brass shrink-0 mt-0.5" /> {f}
              </li>
            ))}
          </ul>

          <div className="mt-10 grid grid-cols-3 gap-3 text-center">
            {[
              { icon: Truck, label: 'Morgen in huis' },
              { icon: RefreshCcw, label: '30 dagen bedenktijd' },
              { icon: ShieldCheck, label: '5 jaar garantie' },
            ].map(({ icon: Icon, label }) => (
              <div key={label} className="border hairline py-4 px-2">
                <Icon size={18} className="mx-auto text-brass" strokeWidth={1.5} />
                <p className="text-[0.68rem] mt-2 text-ivory/60">{label}</p>
              </div>
            ))}
          </div>

          <div className="mt-10">
            <h2 className="eyebrow mb-4">Specificaties</h2>
            <dl className="divide-y divide-ivory/10 border-y hairline">
              {specs.map(([label, value]) => (
                <div key={label} className="flex justify-between py-3 text-sm">
                  <dt className="text-ivory/50">{label}</dt>
                  <dd className="text-right">{value}</dd>
                </div>
              ))}
            </dl>
          </div>
        </div>
      </div>

      <section className="pt-32">
        <h2 className="font-display text-4xl mb-10">Ook interessant</h2>
        <div className="grid gap-x-8 gap-y-14 md:grid-cols-3">
          {related.map((p) => (
            <ProductCard key={p.slug} product={p} />
          ))}
        </div>
      </section>
    </div>
  )
}

src/routes/vakmanschap.tsx
import { Link, createFileRoute } from '@tanstack/react-router'
import { img } from '@/lib/format'

export const Route = createFileRoute('/vakmanschap')({
  head: () => ({
    meta: [{ title: 'Vakmanschap & slijpservice — JAEGERscissors.nl' }],
  }),
  component: Craft,
})

const steps = [
  {
    n: '01',
    title: 'Het staal',
    text: 'We werken uitsluitend met Japans kobalt- en poedermetaalstaal zoals VG-10 en ATS-314. Gehard tot 60–62 HRC voor een snede die maanden scherp blijft.',
  },
  {
    n: '02',
    title: 'Het slijpen',
    text: 'Het convexe blad wordt met de hand op natuurlijke Japanse wetstenen geslepen en gehoond. Zo snijdt de schaar het haar in plaats van het te knijpen.',
  },
  {
    n: '03',
    title: 'De balans',
    text: 'Elke schaar wordt afgesteld op spanning en balans, met het zwaartepunt precies op de schroef. Dat voel je na een volle dag knippen in je pols.',
  },
  {
    n: '04',
    title: 'De test',
    text: 'Voordat een schaar ons atelier verlaat, knippen we er zelf mee — op nat haar, droog haar en zijde. Pas daarna krijgt hij zijn serienummer.',
  },
]

function Craft() {
  return (
    <>
      <section className="relative overflow-hidden grain">
        <img
          src={img('/img/craft.png', 1920)}
          alt="Een schaarblad wordt met de hand geslepen"
          className="absolute inset-0 w-full h-full object-cover opacity-60"
        />
        <div className="absolute inset-0 bg-gradient-to-t from-ink via-ink/50 to-ink/30" />
        <div className="relative max-w-7xl mx-auto px-5 md:px-8 py-40 md:py-56">
          <p className="eyebrow">Vakmanschap</p>
          <h1 className="font-display text-6xl md:text-8xl mt-4 max-w-3xl leading-[0.95]">
            48 handelingen. Eén perfecte snede.
          </h1>
        </div>
      </section>

      <section className="max-w-7xl mx-auto px-5 md:px-8 pt-24 grid md:grid-cols-2 gap-14">
        <p className="font-display text-3xl md:text-4xl leading-snug text-ivory/90">
          JAEGER begon in een kleine barbershop, uit frustratie over scharen die na
          een paar maanden gingen trekken. Vandaag ontwerpen we de scharen die we
          zelf altijd wilden hebben.
        </p>
        <div className="space-y-5 text-ivory/65 leading-relaxed">
          <p>
            Onze naam komt van het Duitse woord voor jager: geduldig, precies en
            gefocust. Precies de eigenschappen die een goede barber nodig heeft.
          </p>
          <p>
            Iedere schaar wordt ontworpen in Nederland, in samenwerking met
            meesterslijpers in Seki — de Japanse stad die al eeuwenlang bekend
            staat om haar messenmakers.
          </p>
        </div>
      </section>

      <section className="max-w-7xl mx-auto px-5 md:px-8 pt-28">
        <div className="grid md:grid-cols-2 lg:grid-cols-4 border-t hairline">
          {steps.map((s) => (
            <div key={s.n} className="pt-8 pb-4 md:pr-8">
              <p className="font-display text-brass text-5xl">{s.n}</p>
              <h3 className="font-display text-2xl mt-4">{s.title}</h3>
              <p className="mt-3 text-sm text-ivory/60 leading-relaxed">{s.text}</p>
            </div>
          ))}
        </div>
      </section>

      <section id="slijpservice" className="max-w-7xl mx-auto px-5 md:px-8 pt-32">
        <div className="grid lg:grid-cols-2 bg-coal border hairline">
          <div className="p-10 md:p-14">
            <p className="eyebrow">Levenslange slijpservice</p>
            <h2 className="font-display text-4xl md:text-5xl mt-4">
              Scherp als op dag één. Voor altijd.
            </h2>
            <p className="mt-6 text-ivory/65 leading-relaxed">
              Stuur je JAEGER-schaar op met het gratis retourlabel en binnen vijf
              werkdagen heb je hem terug: geslepen, gepolijst, afgesteld en
              gereinigd. De eerste slijpbeurt is altijd gratis.
            </p>
            <ul className="mt-8 space-y-4 text-sm">
              <li className="flex justify-between border-b hairline pb-3">
                <span>Eerste slijpbeurt</span>
                <span className="text-brass">Gratis</span>
              </li>
              <li className="flex justify-between border-b hairline pb-3">
                <span>Knipschaar slijpen</span>
                <span>€ 39</span>
              </li>
              <li className="flex justify-between border-b hairline pb-3">
                <span>Effileerschaar slijpen</span>
                <span>€ 45</span>
              </li>
              <li className="flex justify-between">
                <span>Retourverzending</span>
                <span className="text-brass">Gratis</span>
              </li>
            </ul>
            <Link to="/contact" className="btn-brass mt-10">
              Slijpbeurt aanvragen
            </Link>
          </div>
          <div className="relative min-h-80">
            <img
              src={img('/img/set.png', 1200)}
              alt="JAEGER scharen in lederen koker"
              loading="lazy"
              className="absolute inset-0 w-full h-full object-cover"
            />
          </div>
        </div>
      </section>
    </>
  )
}

src/routes/contact.tsx
import { createFileRoute } from '@tanstack/react-router'
import { Check, Clock, Mail, MapPin } from 'lucide-react'
import { useState } from 'react'

export const Route = createFileRoute('/contact')({
  head: () => ({
    meta: [{ title: 'Contact & advies — JAEGERscissors.nl' }],
  }),
  component: Contact,
})

const subjects = [
  { value: 'advies', label: 'Persoonlijk advies over een schaar' },
  { value: 'slijpservice', label: 'Slijpservice aanvragen' },
  { value: 'bestelling', label: 'Vraag over mijn bestelling' },
  { value: 'zakelijk', label: 'Zakelijk / salon of academie' },
]

const empty = { name: '', email: '', phone: '', salon: '', subject: 'advies', message: '' }

function encode(data: Record<string, string>) {
  return Object.entries(data)
    .map(([key, val]) => `${encodeURIComponent(key)}=${encodeURIComponent(val)}`)
    .join('&')
}

function Contact() {
  const [fields, setFields] = useState(empty)
  const [status, setStatus] = useState<'idle' | 'sending' | 'sent' | 'error'>('idle')

  const onChange = (
    e: React.ChangeEvent<HTMLInputElement | HTMLTextAreaElement | HTMLSelectElement>,
  ) => setFields({ ...fields, [e.target.name]: e.target.value })

  const onSubmit = async (e: React.FormEvent<HTMLFormElement>) => {
    e.preventDefault()
    setStatus('sending')
    const botField = new FormData(e.currentTarget).get('bot-field')?.toString() ?? ''
    try {
      const res = await fetch('/contact-form.html', {
        method: 'POST',
        headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
        body: encode({ 'form-name': 'contact', 'bot-field': botField, ...fields }),
      })
      if (!res.ok) throw new Error(`Status ${res.status}`)
      setStatus('sent')
      setFields(empty)
    } catch (err) {
      console.error(err)
      setStatus('error')
    }
  }

  const input =
    'w-full bg-coal border border-ivory/15 px-4 py-3 text-ivory placeholder:text-ivory/30 focus:outline-none focus:border-brass transition-colors'

  return (
    <div className="max-w-7xl mx-auto px-5 md:px-8 pt-16 grid lg:grid-cols-12 gap-16">
      <div className="lg:col-span-5">
        <p className="eyebrow">Contact & advies</p>
        <h1 className="font-display text-5xl md:text-6xl mt-3 leading-tight">
          Advies van barber tot barber.
        </h1>
        <p className="mt-6 text-ivory/65 leading-relaxed">
          Twijfel je tussen modellen, wil je een slijpbeurt aanvragen of zoek je
          scharen voor je hele team? Laat het ons weten — we reageren binnen één
          werkdag.
        </p>
        <ul className="mt-10 space-y-6 text-sm">
          <li className="flex gap-4">
            <Mail size={18} className="text-brass mt-0.5" strokeWidth={1.5} />
            <span>
              <span className="block text-ivory/50 text-xs uppercase tracking-[0.2em]">E-mail</span>
              info@jaegerscissors.nl
            </span>
          </li>
          <li className="flex gap-4">
            <Clock size={18} className="text-brass mt-0.5" strokeWidth={1.5} />
            <span>
              <span className="block text-ivory/50 text-xs uppercase tracking-[0.2em]">Bereikbaar</span>
              Ma–vr 9:00 – 17:30
            </span>
          </li>
          <li className="flex gap-4">
            <MapPin size={18} className="text-brass mt-0.5" strokeWidth={1.5} />
            <span>
              <span className="block text-ivory/50 text-xs uppercase tracking-[0.2em]">Atelier</span>
              Op afspraak in Amsterdam
            </span>
          </li>
        </ul>
      </div>

      <div className="lg:col-span-7">
        {status === 'sent' ? (
          <div className="border hairline bg-coal p-12 text-center">
            <div className="w-14 h-14 mx-auto rounded-full bg-brass text-ink flex items-center justify-center">
              <Check size={26} />
            </div>
            <h2 className="font-display text-4xl mt-6">Bedankt voor je bericht</h2>
            <p className="mt-3 text-ivory/60">
              We nemen binnen één werkdag contact met je op.
            </p>
            <button onClick={() => setStatus('idle')} className="btn-ghost mt-8">
              Nog een bericht sturen
            </button>
          </div>
        ) : (
          <form
            name="contact"
            onSubmit={onSubmit}
            className="border hairline bg-coal/40 p-8 md:p-10 grid sm:grid-cols-2 gap-5"
          >
            <input type="hidden" name="form-name" value="contact" />
            <p className="hidden">
              <label>
                Niet invullen: <input name="bot-field" />
              </label>
            </p>
            <label className="block">
              <span className="text-xs uppercase tracking-[0.18em] text-ivory/60">Naam *</span>
              <input name="name" required value={fields.name} onChange={onChange} className={`${input} mt-2`} />
            </label>
            <label className="block">
              <span className="text-xs uppercase tracking-[0.18em] text-ivory/60">E-mail *</span>
              <input type="email" name="email" required value={fields.email} onChange={onChange} className={`${input} mt-2`} />
            </label>
            <label className="block">
              <span className="text-xs uppercase tracking-[0.18em] text-ivory/60">Telefoon</span>
              <input type="tel" name="phone" value={fields.phone} onChange={onChange} className={`${input} mt-2`} />
            </label>
            <label className="block">
              <span className="text-xs uppercase tracking-[0.18em] text-ivory/60">Salon / barbershop</span>
              <input name="salon" value={fields.salon} onChange={onChange} className={`${input} mt-2`} />
            </label>
            <label className="block sm:col-span-2">
              <span className="text-xs uppercase tracking-[0.18em] text-ivory/60">Onderwerp</span>
              <select name="subject" value={fields.subject} onChange={onChange} className={`${input} mt-2`}>
                {subjects.map((s) => (
                  <option key={s.value} value={s.value}>
                    {s.label}
                  </option>
                ))}
              </select>
            </label>
            <label className="block sm:col-span-2">
              <span className="text-xs uppercase tracking-[0.18em] text-ivory/60">Bericht *</span>
              <textarea
                name="message"
                required
                rows={6}
                value={fields.message}
                onChange={onChange}
                placeholder="Vertel ons bijvoorbeeld welke technieken je het meest gebruikt en welke handgrootte je hebt."
                className={`${input} mt-2 resize-y`}
              />
            </label>
            <div className="sm:col-span-2 flex flex-col sm:flex-row sm:items-center gap-4 justify-between">
              {status === 'error' ? (
                <p className="text-sm text-red-400">
                  Versturen is mislukt. Probeer het opnieuw of mail ons direct.
                </p>
              ) : (
                <p className="text-xs text-ivory/40">We gebruiken je gegevens alleen om te reageren.</p>
              )}
              <button type="submit" disabled={status === 'sending'} className="btn-brass">
                {status === 'sending' ? 'Versturen…' : 'Verstuur bericht'}
              </button>
            </div>
          </form>
        )}
      </div>
    </div>
  )
}

src/routes/checkout/success.tsx
import { Link, createFileRoute } from '@tanstack/react-router'
import { Check } from 'lucide-react'
import { useEffect } from 'react'
import { useCart } from '@/lib/cart'

export const Route = createFileRoute('/checkout/success')({
  head: () => ({ meta: [{ title: 'Bedankt voor je bestelling — JAEGERscissors.nl' }] }),
  component: CheckoutSuccess,
})

function CheckoutSuccess() {
  const { clear } = useCart()

  useEffect(() => {
    clear()
  }, [])

  return (
    <div className="max-w-xl mx-auto px-5 py-32 text-center">
      <div className="w-16 h-16 mx-auto rounded-full bg-brass text-ink flex items-center justify-center">
        <Check size={30} />
      </div>
      <p className="eyebrow mt-8">Bestelling geplaatst</p>
      <h1 className="font-display text-5xl mt-3">Bedankt voor je vertrouwen</h1>
      <p className="mt-5 text-ivory/65 leading-relaxed">
        Je betaling is gelukt. Je ontvangt binnen enkele minuten een bevestiging
        per e-mail. Je schaar wordt vandaag nog met de hand gecontroleerd en
        verzekerd verzonden.
      </p>
      <Link to="/winkel" className="btn-ghost mt-10">
        Verder winkelen
      </Link>
    </div>
  )
}

src/routes/checkout/cancel.tsx
import { Link, createFileRoute } from '@tanstack/react-router'
import { useCart } from '@/lib/cart'

export const Route = createFileRoute('/checkout/cancel')({
  head: () => ({ meta: [{ title: 'Betaling geannuleerd — JAEGERscissors.nl' }] }),
  component: CheckoutCancel,
})

function CheckoutCancel() {
  const { open } = useCart()

  return (
    <div className="max-w-xl mx-auto px-5 py-32 text-center">
      <p className="eyebrow">Betaling geannuleerd</p>
      <h1 className="font-display text-5xl mt-3">Geen zorgen</h1>
      <p className="mt-5 text-ivory/65 leading-relaxed">
        Er is niets afgeschreven. Je winkelwagen staat nog voor je klaar.
      </p>
      <div className="mt-10 flex flex-wrap gap-4 justify-center">
        <button onClick={open} className="btn-brass">
          Naar winkelwagen
        </button>
        <Link to="/winkel" className="btn-ghost">
          Verder winkelen
        </Link>
      </div>
    </div>
  )
}

src/components/Header.tsx
import { Link } from '@tanstack/react-router'
import { Menu, ShoppingBag, X } from 'lucide-react'
import { useEffect, useState } from 'react'
import { Logo } from '@/components/Logo'
import { useCart } from '@/lib/cart'

const nav = [
  { to: '/winkel', label: 'Collectie' },
  { to: '/vakmanschap', label: 'Vakmanschap' },
  { to: '/contact', label: 'Contact' },
] as const

export function Header() {
  const { count, open } = useCart()
  const [menuOpen, setMenuOpen] = useState(false)
  const [scrolled, setScrolled] = useState(false)

  useEffect(() => {
    const onScroll = () => setScrolled(window.scrollY > 24)
    onScroll()
    window.addEventListener('scroll', onScroll, { passive: true })
    return () => window.removeEventListener('scroll', onScroll)
  }, [])

  return (
    <>
      <div className="bg-brass text-ink text-center text-[0.68rem] font-semibold tracking-[0.2em] uppercase py-2 px-4">
        Gratis verzekerde verzending · 30 dagen bedenktijd · Levenslange slijpservice
      </div>
      <header
        className={`sticky top-0 z-40 transition-colors duration-300 border-b ${
          scrolled ? 'bg-ink/90 backdrop-blur hairline' : 'bg-ink border-transparent'
        }`}
      >
        <div className="max-w-7xl mx-auto px-5 md:px-8 h-20 flex items-center justify-between">
          <button
            className="md:hidden -ml-2 p-2"
            onClick={() => setMenuOpen(true)}
            aria-label="Menu openen"
          >
            <Menu size={22} />
          </button>

          <Link to="/" aria-label="JAEGERscissors home">
            <Logo />
          </Link>

          <nav className="hidden md:flex items-center gap-10">
            {nav.map((item) => (
              <Link
                key={item.to}
                to={item.to}
                className="text-xs font-semibold tracking-[0.22em] uppercase text-ivory/70 hover:text-ivory transition-colors"
                activeProps={{ className: '!text-brass' }}
              >
                {item.label}
              </Link>
            ))}
          </nav>

          <button
            onClick={open}
            className="relative p-2 -mr-2 hover:text-brass transition-colors"
            aria-label={`Winkelwagen (${count})`}
          >
            <ShoppingBag size={22} strokeWidth={1.6} />
            {count > 0 && (
              <span className="absolute -top-0.5 -right-0.5 min-w-5 h-5 px-1 rounded-full bg-brass text-ink text-[0.65rem] font-bold flex items-center justify-center">
                {count}
              </span>
            )}
          </button>
        </div>
      </header>

      {menuOpen && (
        <div className="fixed inset-0 z-50 bg-ink flex flex-col p-6 md:hidden">
          <div className="flex items-center justify-between h-14">
            <Logo />
            <button onClick={() => setMenuOpen(false)} aria-label="Menu sluiten">
              <X size={24} />
            </button>
          </div>
          <nav className="mt-16 flex flex-col gap-8">
            <Link
              to="/"
              onClick={() => setMenuOpen(false)}
              className="font-display text-4xl"
            >
              Home
            </Link>
            {nav.map((item) => (
              <Link
                key={item.to}
                to={item.to}
                onClick={() => setMenuOpen(false)}
                className="font-display text-4xl"
              >
                {item.label}
              </Link>
            ))}
          </nav>
        </div>
      )}
    </>
  )
}

src/components/Footer.tsx
import { Link } from '@tanstack/react-router'
import { Logo } from '@/components/Logo'

export function Footer() {
  return (
    <footer className="border-t hairline mt-32">
      <div className="max-w-7xl mx-auto px-5 md:px-8 py-16 grid gap-12 md:grid-cols-4">
        <div className="md:col-span-2 max-w-sm">
          <Logo />
          <p className="mt-5 text-sm text-ivory/60 leading-relaxed">
            Premium barberscharen van Japans staal, ontworpen voor professionals
            die geen compromissen sluiten. Geleverd vanuit Nederland.
          </p>
        </div>
        <div>
          <h4 className="eyebrow mb-5">Winkel</h4>
          <ul className="space-y-3 text-sm text-ivory/70">
            <li>
              <Link to="/winkel" className="hover:text-ivory">Alle scharen</Link>
            </li>
            <li>
              <Link to="/winkel" search={{ categorie: 'knipschaar' }} className="hover:text-ivory">
                Knipscharen
              </Link>
            </li>
            <li>
              <Link to="/winkel" search={{ categorie: 

---
*Content truncated for display.*
