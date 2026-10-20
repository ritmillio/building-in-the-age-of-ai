# design-rules.md (template)

> Your taste, written down once. Attach it to every design or UI request (or link it from AGENTS.md). Max ~15 lines; a long rules file gets ignored.

- **Colours:** one ink colour for actions (`#0d0d0d`), one accent for links and highlights (`#1971c2`), status colours only for status. No other hues.
- **Type:** one font family for the app (`Inter`), one for headings (`Instrument Serif`). Sizes: 12 / 14 / 16 / 20 / 28.
- **Spacing:** a 4px scale (4, 8, 12, 16, 24, 32, 48). No random values.
- **Corners:** small radius on controls (4px), larger on cards and dialogs (8px). Never fully round buttons.
- **Lines and depth:** thin 1px hairlines. No gradients on surfaces, no heavy shadows; only floating layers (menus, dialogs) get one soft shadow.
- **Every screen has:** an empty state, a loading state and an error state.
- **Copy:** short, plain, no hype words, no exclamation marks.
- **References:** these 3 screens are what good looks like: `refs/01.png`, `refs/02.png`, `refs/03.png`.
