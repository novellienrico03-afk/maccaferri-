# Maccaferri NextGen - Nature-Based Solutions (NBS)
## Project Repository Boilerplate

Questa è la struttura tecnica per la revisione del sito Maccaferri in chiave **Pura Avanguardia**. Il progetto utilizza **Next.js 14**, **Tailwind CSS** per lo styling e **Framer Motion** per le animazioni.

---

### 1. Struttura del Progetto (File Tree)

maccaferri-vanguard/
├── public/
│   └── assets/             # Video 4K, Render 3D, Loghi storici
├── src/
│   ├── components/         # Componenti UI (Bento, Hero, Map)
│   │   ├── Hero.tsx
│   │   ├── VanguardToggle.tsx
│   │   ├── GlobalMap.tsx
│   │   └── VanguardCTA.tsx
│   ├── styles/
│   │   └── globals.css     # Design System & Custom Animations
│   ├── types/
│   │   └── index.ts        # Type definitions per Case Studies e Software
│   └── app/
│       └── page.tsx        # Home Page Assembler
├── tailwind.config.js      # Custom Theme (Mac-Black, Mac-Green)
└── package.json            # Dependencies


---

### 2. Configurazione Design System (`tailwind.config.js`)

```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./src/**/*.{js,ts,jsx,tsx,mdx}",
  ],
  theme: {
    extend: {
      colors: {
        'mac-black': '#0a0a0a',     // Deep Black (Apple Style)
        'mac-green': '#10b981',     // Tech Green (Vanguard)
        'mac-slate': '#1e293b',     // Engineering Slate
        'mac-accent': '#f8fafc',    // Pure White for text
      },
      fontFamily: {
        sans: ['Inter', 'SF Pro Display', 'sans-serif'],
      },
      letterSpacing: {
        tighter: '-0.05em',
        widest: '0.2em',
      }
    },
  },
  plugins: [],
}import { motion } from 'framer-motion';

export default function Hero() {
  return (
    <section className="relative h-screen flex items-center justify-center bg-mac-black overflow-hidden">
      <div className="absolute inset-0 opacity-30">
        <video autoPlay loop muted className="w-full h-full object-cover" src="/assets/nature-engineering.mp4" />
      </div>
      <div className="relative z-10 text-center px-4">
        <motion.span 
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          className="text-mac-green tracking-widest uppercase text-xs font-bold"
        >
          Established 1879 — Shaping the Future
        </motion.span>
        <motion.h1 
          initial={{ opacity: 0, y: 30 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ delay: 0.2 }}
          className="mt-6 text-6xl md:text-9xl font-bold text-white tracking-tighter"
        >
          Riprogrammare <br /> il Pianeta.
        </motion.h1>
      </div>
    </section>
  );
} import { useState } from 'react';
import { motion, AnimatePresence } from 'framer-motion';

export default function VanguardToggle() {
  const [view, setView] = useState('vision');

  return (
    <div className="bg-mac-black py-20 px-6">
      <div className="max-w-6xl mx-auto">
        <div className="flex justify-center mb-16">
          <div className="inline-flex p-1 bg-white/5 rounded-full border border-white/10">
            {['vision', 'tech'].map((mode) => (
              <button
                key={mode}
                onClick={() => setView(mode)}
                className={`px-8 py-2 rounded-full text-sm font-bold transition-all ${
                  view === mode ? 'bg-mac-green text-black' : 'text-gray-400'
                }`}
              >
                {mode === 'vision' ? 'Visione Estetica' : 'Specifiche Tecniche'}
              </button>
            ))}
          </div>
        </div>

        <AnimatePresence mode="wait">
          <motion.div
            key={view}
            initial={{ opacity: 0, scale: 0.98 }}
            animate={{ opacity: 1, scale: 1 }}
            exit={{ opacity: 0, scale: 1.02 }}
            className="grid md:grid-cols-2 gap-12"
          >
            {view === 'vision' ? (
              <div className="col-span-2 text-center">
                <h2 className="text-5xl font-light italic text-white italic">"L'armonia è la forma più alta di protezione."</h2>
              </div>
            ) : (
              <div className="col-span-2 bg-white/5 p-12 rounded-3xl border border-white/10 font-mono">
                <p className="text-mac-green">// DATA_SHEET_V24</p>
                <div className="mt-6 grid grid-cols-2 md:grid-cols-4 gap-8">
                  <div><p className="text-gray-500">Resistenza</p><p className="text-2xl text-white">150kN/m</p></div>
                  <div><p className="text-gray-500">Impatto CO2</p><p className="text-2xl text-white">-35%</p></div>
                  <div><p className="text-gray-500">Longevità</p><p className="text-2xl text-white">120y</p></div>
                  <div><p className="text-gray-500">BIM Ready</p><p className="text-2xl text-white">True</p></div>
                </div>
              </div>
            )}
          </motion.div>
        </AnimatePresence>
      </div>
    </div>
  );
}