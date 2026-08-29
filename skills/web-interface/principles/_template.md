# <Principle name>

**Rule:** <one sentence an engineer can act on without reading further. State the invariant, not the vibe.>

## Why

<Two or three sentences. What breaks when this is ignored, and what a user actually perceives. If the rule has a derivation or a browser behaviour behind it, give it here. A rule with a reason survives; a rule without one gets overridden by the next person in a hurry.>

## How

<Concrete implementation. Real CSS/HTML/JS, not pseudocode. Include the token or custom-property form so the rule ends up encoded in the design system rather than retyped by hand. Add a Tailwind or framework note only when the plain-CSS version does not carry over.>

## Failure modes

- <The specific wrong thing, described as it appears on screen rather than as it appears in the code.>

## Review checklist

- [ ] <Binary and checkable. If it cannot be answered yes or no from the UI or the diff, rewrite it.>
