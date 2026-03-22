# UX Sketches — Planning Poker Meet Add-on

## Design Principles

1. **One tap to select, one tap to confirm.** No menus, no scrolling.
2. **Touch-friendly.** Cards are large enough to tap while on a video call.
3. **Unambiguous selection.** Selected card uses strong border + fill.
4. **Live feedback.** Vote count updates in real time — reduces verbal check-ins.
5. **Host vs. participant.** Host gets extra controls; participants see a clean voting view.

---

## Phase 1–2: Side Panel — Voting View

```
┌─────────────────────────────────┐  ← ~320px wide side panel
│  🃏  Planning Poker             │  ← header, 48px
├─────────────────────────────────┤
│  Story: [Add story title...]    │  ← host-editable in Phase 4
│                                 │
│  Pick your card:                │
│                                 │
│  ┌───┐ ┌───┐ ┌───┐ ┌───┐ ┌───┐ │
│  │ 0 │ │ 1 │ │ 2 │ │ 3 │ │ 5 │ │  ← row 1
│  └───┘ └───┘ └───┘ └───┘ └───┘ │
│  ┌───┐ ┌───┐ ┌───┐ ┌───┐ ┌───┐ │
│  │ 8 │ │13 │ │21 │ │ ? │ │☕ │ │  ← row 2
│  └───┘ └───┘ └───┘ └───┘ └───┘ │
│                                 │
│  ┌───────────────────────────┐  │
│  │     ✓  Confirm Vote       │  │  ← disabled until card selected
│  └───────────────────────────┘  │
│                                 │
├─────────────────────────────────┤
│  Votes in: 3 / 5                │  ← Phase 3
│  ● Ana  ● Bob  ○ Carol  ○ ...   │  ← ● = voted, ○ = waiting
└─────────────────────────────────┘
```

### Card States

| State | Visual |
|-------|--------|
| Default | White background, light grey border, black text |
| Hover/focus | Slight shadow lift |
| Selected (pre-confirm) | Blue border (2px), light blue background fill |
| Voted (post-confirm) | Checkmark overlay, card slightly desaturated — can still change |
| Disabled (after reveal) | Greyed out, no pointer events |

---

## Phase 3: Side Panel — After Voting

```
┌─────────────────────────────────┐
│  🃏  Planning Poker             │
├─────────────────────────────────┤
│  Story: "User SSO login"        │
│                                 │
│  Your vote:  ┌───┐              │
│              │ 5 │ ✓            │  ← confirmed card shown
│              └───┘              │
│                                 │
│  [  Change Vote  ]              │  ← re-enables card grid
│                                 │
├─────────────────────────────────┤
│  Votes in: 4 / 5                │
│  ● Ana  ● Bob  ● Carol  ○ Dave  │
│                                 │
│  Waiting for Dave...            │
└─────────────────────────────────┘
```

---

## Phase 3: Main Stage — Reveal View

```
┌──────────────────────────────────────────────────────────────┐
│   Story: "As a user, I want to log in with SSO"              │
│                                                              │
│   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐       │
│   │    5    │  │    8    │  │    5    │  │    3    │       │
│   │  Ana    │  │  Bob    │  │  Carol  │  │  Dave   │       │
│   └─────────┘  └─────────┘  └─────────┘  └─────────┘       │
│                                                              │
│   Average: 5.25       Spread: 3 → 8                         │
│                                                              │
│              [ Start New Round ]    [ Reset ]                │
└──────────────────────────────────────────────────────────────┘
```

### Before Reveal (votes hidden)

Cards show a card-back pattern (e.g. `?` or a solid colour) until the host
clicks **Reveal Votes**. This prevents anchoring bias.

```
│   ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐
│   │  ░░░░░  │  │  ░░░░░  │  │  ░░░░░  │  │  ░░░░░  │
│   │  Ana ✓  │  │  Bob ✓  │  │ Carol ✓ │  │  Dave ✓ │
│   └─────────┘  └─────────┘  └─────────┘  └─────────┘
│
│   All votes in!
│
│              [ Reveal Votes ]
```

---

## Phase 4: Host Controls (Side Panel)

```
┌─────────────────────────────────┐
│  🃏  Planning Poker  [HOST]     │
├─────────────────────────────────┤
│  Story: [User SSO login      ]  │  ← editable text input
│                                 │
│  [  Start New Round  ]          │
│  [  Reset Votes      ]          │
│  [  Reveal Votes     ]          │  ← only visible when all voted
│                                 │
├─────────────────────────────────┤
│  Votes in: 4 / 5                │
│  ● Ana (voted)  ● Bob (voted)   │
│  ● Carol (voted) ○ Dave         │
└─────────────────────────────────┘
```

Participants see the same panel but without the host control buttons.

---

## Color / Style Reference

| Token | Value | Usage |
|-------|-------|-------|
| Primary blue | `#1a73e8` | Selected card border, confirm button |
| Light blue | `#e8f0fe` | Selected card background |
| Surface | `#ffffff` | Card background, panel background |
| Grey border | `#dadce0` | Default card border |
| Text primary | `#202124` | Card values, labels |
| Text secondary | `#5f6368` | "Waiting for...", counts |
| Success green | `#1e8e3e` | Voted checkmark |

Font: `'Google Sans', Roboto, sans-serif` — matches Meet's own UI.
