# @papercusp/card-stack

An overlapping **card-deck browser** for a group of same-type items: cards
stack down-and-right with their real content dimmed underneath, the active
card sits on top with a category badge riding its top edge and `‹ Prev / Next ›`
pills straddling its bottom edge, and cycling animates the classic index-based
deck pattern (the top card flies off with a tilt + fade while the next card
slides up out of the pile — stepping back flies it back on).

- **Animation without a dependency** — every card in the window
  `[active-1 … active+maxPeek]` stays mounted as the same element type; only
  its transform/opacity (derived from its distance to the active index)
  changes, so pure CSS transitions do all the motion (the same technique as
  the Motion/Framer card-stack example, minus the drag physics). The deck's
  height animates between cards via a measured `ResizeObserver` layout.
- **Headless of domain** — `renderCard` render-prop; optional `renderExpanded`
  and `header` (category badge). Theming via CSS custom properties
  (`--bg-1`, `--bg-2`, `--accent`, `--border`, `--fg*`) with self-contained
  fallbacks, so it renders sensibly with no theme at all.
- **Accessible** — keyboard ← → on the focused deck, `aria-hidden` stacked
  layers, clickable position dots (`role=tablist`), labelled Prev/Next.

```tsx
import { CardStack } from '@papercusp/card-stack';

<CardStack
  items={ideas}
  getKey={(idea) => idea.id}
  header={<><span className="pc-cardstack__header-label">first-principles</span>
           <span className="pc-cardstack__header-count">{ideas.length}</span></>}
  renderCard={(idea) => <IdeaCard idea={idea} />}
  ariaLabel="first-principles ideas"
/>
```

Peer deps: `react` (18/19), `lucide-react` (the two chevrons).

Born in the Papercusp operator's Learning tab (Ideas decision-queue and
Observations stacks, 2026-07-19); extracted here because nothing in it knows
about Papercusp.
