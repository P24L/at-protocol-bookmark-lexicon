 Struktura projektu

 at-protocol-bookmark-lexicon/
├── README.md
├── lexicons/
│   ├── app.hyber-limit.bookmark.json
│   ├── app.hyber-limit.bookmark.list.json
│   └── app.hyber-limit.bookmark.embed.json
├── docs/
│   ├── business-requirements.md
│   └── implementation-guide.md
├── examples/
│   └── usage-examples.md
└── schemas/
    └── validation-tests.json


Claude Code workflow

Vytvořit jednotlivé lexicon JSON soubory
Přidat validační skripty
Napsat dokumentaci s příklady použití
Vytvořit TypeScript typy z lexikonů

Doporučené první kroky

Přesunout JSON schemas z BRD dokumentu do samostatných souborů
Přidat package.json pro případné build tools
Vytvořit validátor lexikonů
Napsat README s quick start guide