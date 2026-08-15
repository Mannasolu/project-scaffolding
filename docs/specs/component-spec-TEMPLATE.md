# Component Spec: [COMPONENT NAME]

> **What this document is:** a precise description of ONE component -- precise
> enough to hand to an agent (or a person) to build without you in the room.
> This is the bridge between the master plan (what the whole project is) and
> actual construction. One spec per component. Delete these prompt lines as you
> fill each section.
>
> **The pattern (spec-driven):** agree on the spec BEFORE building. The agent
> builds to the spec. When reality forces a change, update the spec to match
> what shipped -- the spec and the code never drift apart.

**Status:** DRAFT | AGREED | BUILT
**Owner / role:** [who or which role owns this -- e.g. backend architect]
**Depends on:** [other components or specs this needs; "none" if standalone]

## 1. Purpose
> One or two sentences. What this component does and why it exists. If someone
> asked "why not just skip it," the answer is here.

## 2. Inputs
> What it receives. Data, files, signals, config. Be exact about shapes/formats.

## 3. Outputs
> What it produces. Same precision. This is the contract other components rely on.

## 4. Behavior
> What it does with inputs to produce outputs. The core logic, in plain steps.
> Include the failure behavior: what happens on bad input, interruption, retry.

## 5. Boundaries (explicitly NOT this component's job)
> What it does not do. This is where scope creep gets stopped before it starts.

## 6. How you'll know it works (acceptance)
> Concrete, testable conditions. "Given X input, produces Y output." An agent
> can check itself against these; a person can verify without guessing.

## 7. Open questions
> Anything unresolved about this component. Resolve before status moves to AGREED.
