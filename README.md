# celinetruong.me: polished build

`index.html` is the whole site: one self-contained file with fonts, images, and the
React runtime inlined. Nothing to install, nothing to build. Drop it on any host.

## Deploying

The live site currently serves from `celine-truong-9d8bad0b-8556-49f9-9d.vercel.app`,
with `celinetruong.me` pointing at it. To ship this version, replace that project's
`index.html`, or deploy this folder as a new static project and repoint the domain.

```bash
npx vercel deploy --prod
```

Run it from this directory. It will ask you to log in the first time.

## Page order

Value first, character last. Events leads throughout: the nav, the stat grid, and
the rotating hero word all open on Events.

1. Hero
2. Built for founder communities: the "why hire her" pitch, straight under
   the hero. A root-cause paragraph, three numbered steps (find the right
   people, understand the founder, amplify and make it real), then six
   transferable-skill cards
3. The four numbers
4. Events: Office Hours (After Dark), then a highlighted "Partner &
   ecosystem economics" block (UCLA Anderson, the CTET venue model, the
   five-brand-partner pop-up), then Beats & Beans
5. Sales: Gartner
6. Social
7. Build: Clem
8. What I'd build for you
9. Zero to one
10. Who you'd be working with: quote, David Goldberg's recommendation,
    testimonials, on the aubergine ground
11. Contact

The founder-communities pitch and the partner-economics block both have no
nav anchor, so they were free to move anywhere. The four anchored sections
(Events, Sales, Social, Build) keep their original relative order: moving one
of them out of nav order would mean clicking "Sales" scrolls past something
the nav still lists after it.

### Style

No em dashes anywhere in the copy, by request. Use a colon, a comma, parentheses,
or split into two sentences instead. Check `build/patch.py` for the pattern before
adding new copy.

Written in first person throughout ("I," not "she"), by request, with two
exceptions kept in third person on purpose:

- The four testimonial quotes (Manager, Ty, and David Goldberg's letter and its
  excerpts). These are verbatim words from named other people. Rewriting
  "Celine is..." to "I am..." inside a quote would misattribute what that person
  actually said, not just restyle her own copy.
- Other people's own pronouns inside a shared sentence: "Rose ran ops because
  she thrived on execution" in the Office Hours team section stays third person
  for Rose. Only the clauses about Celine herself changed.

The nav and footer wordmark ("CELINE TRUONG"), the contact email, and the hero
photo's alt text were left alone: a name-brand, an email address, and an
objective image description aren't narrative copy.

### On the recommendation

David Goldberg's letter is excerpted, not reproduced whole. The original was
written for a teaching placement in Spain and closes on a line about students
being "in the finest care and mentorship." That framing is omitted, since it
reads as a mismatch to anyone hiring for these roles. If you send this to a
programme of that kind, put those lines back.

Every quoted phrase is verbatim from the letter. Keep it that way.

## Palette

Sampled from the hero photograph, then pushed for saturation. Three hue families:
warm neutral (78 to 82), olive from the plant (116 to 118), burgundy from the
cardigan (18).

| Role | Value | Hex |
| --- | --- | --- |
| paper | `oklch(97% 0.013 82)` | `#faf4ec` |
| sand band | `oklch(89% 0.034 78)` | `#e7d9c2` |
| ink | `oklch(23% 0.022 45)` | `#261a14` |
| olive (primary) | `oklch(45% 0.098 118)` | `#515c0e` |
| burgundy (accent) | `oklch(44% 0.155 18)` | `#951c30` |
| petrol (numerals only) | `oklch(45% 0.080 198)` | `#006265` |
| aubergine (closing ground) | `oklch(24% 0.055 330)` | `#2d152c` |
| rose (closing eyebrow) | `oklch(82% 0.055 30)` | `#e6b8af` |

Each colour has one job. Olive is structure: links, eyebrows, pills. Burgundy is
emphasis: the rotating hero word, the recommendation, the partner-economics
numbers. Petrol is every other headline numeral and nothing else. Aubergine is a
surface, used once. Keep it that way; four accents only work while each stays in
its lane.

Both cardigan colours were pulled toward the page's warm axis rather than used
literally. The teal sampled at hue 225 (cool blue) and sits at 198, green-leaning,
so it reaches back toward the olive. The purple sampled at 298 (violet) and sits
at 330, a warm aubergine that reads as kin to the burgundy. The closing section
now runs on one warm family: aubergine ground, rose eyebrow, burgundy accents.
No section carries more than three accent hues.

The petrol is an interpretation, not a sample. In the photo the cardigan's teal is
`#193a48`, 0.44% of the knit and too dark to register.

Every text/background pair on the page clears WCAG AA. If you change a colour,
re-check it; several pairs sit in the 4.5 to 5.2:1 range with no headroom.

## What changed from the original

A polish pass against Emil Kowalski's `emil-design-eng` and `apple-design` skills
(installed at `../../.claude/skills/`).

- Press feedback, keyboard focus rings, `prefers-reduced-motion`
- Scroll reveals on a strong ease-out with staggered children
- Anchor links clear the sticky nav; hover gated to pointer devices
- Hero photo re-encoded: 6.2 MB PNG to 593 KB JPEG (page 9.0 MB to 1.5 MB)
- Hero photo now shows on mobile; it was `display:none` under 720px
- Funnel diagram labels were near-white on light green (about 1.5:1); now ink on
  a re-tuned ramp
- Body copy capped at 68 characters a line; several blocks ran past 130
- Real heading structure added (1 h1, 10 h2), where the page had none
- Removed the "See the mechanics behind the curtain" button. It linked to
  `Celine Truong Mechanics.dc.html`, which does not exist and 404s. Restore it
  from git or `build/patch.py` step 18 if that page gets built.

## Progressive disclosure

Founder-scan pass: read the page as someone busy, deciding whether to keep
scrolling. Six spots made a reader work through resume-density prose before
reaching the next hook. Each is now a native `<details>` element, default
closed: the headline, the number, and the one-line takeaway stay visible,
and the execution detail is one click away.

| Section | Stays visible | Behind the toggle |
| --- | --- | --- |
| Built for founder communities | Pitch + 3 numbered steps | The six transferable-skill cards |
| Events, Office Hours | Idea, role, photo | What I built, how I led the team, stats + embed |
| Events, Beats & Beans | Role | The economics bullets, why it matters, the 3 stat numbers |
| Sales | Headline, "$277,200 closed" | All three job entries |
| Social | Headline, one-line stat | Format breakdown, reach numbers, embeds, ratio card |
| Build | What Clem does, App Store rating | The four review quotes |

Native `<details>`/`<summary>`, no JavaScript: works with keyboards and
screen readers by default, and needs no maintenance in the reveal-animation
system (`.expand-body` content is invisible while collapsed, so the existing
scroll-reveal script naturally never has to fade it in). The `+` rotates to
an `×` on open via a CSS transform; the panel itself snaps open rather than
animating height, which is the standard, reliable way to do this.

The closing section (David Goldberg's recommendation, the two testimonials)
was deliberately left alone: a reader who scrolls that far has already shown
interest, and burying your strongest third-party endorsement behind a click
would cost more than it saves.

## Known gap

The Events "Why this matters for you" numbers include a "149% of goal" ticket
figure that portfolio-brief.md flags as unconfirmed against Beats & Beans. It is
held out of the page until confirmed.

## Editing

`index.html` is a build artifact: the page markup lives inside it as a JSON string,
so it is not hand-editable. The readable source is in `build/`:

| File | What it is |
| --- | --- |
| `build/source.template.html` | The actual page markup and component logic |
| `build/source.template.original.html` | The pre-polish version, for diffing |
| `build/patch.py` | Every change, as reproducible asserted edits |
| `build/build.py` | Injects the template and hero image back into `index.html` |
| `build/hero-optimized.jpg` | The re-encoded hero photo |

`patch.py` transforms the *original* template, so edits belong there rather than in
`source.template.html`, which it overwrites. It needs `live.html` (the original
downloaded bundle) present to rebuild, or just ask Claude.
