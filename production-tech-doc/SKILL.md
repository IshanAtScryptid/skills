---
name: production-tech-doc
description: Write technical content in Ishan's voice — the tone, phrasing, and word choice of a production infrastructure handbook. Use this skill whenever the user asks to write, rewrite, or edit technical prose "in my style", "in my voice", "like my docs", or asks for technical documentation, architecture write-ups, system explanations, README sections, design notes, or engineering emails/posts where the writing should sound like them. Trigger on any request to draft or polish technical writing for this user, even when they don't name the style explicitly.
---

# Ishan's technical writing voice

This skill is about how sentences sound — tone, phrasing, word choice, rhythm.
Document structure and formatting are not the concern here; whatever shape the
content takes, the prose must read like the paragraphs quoted at the bottom.

All names, addresses, and figures in the examples below are fictional. They
exist to fix the register, not to describe any real system.

## The voice in one paragraph

An engineer who built the system is explaining it to another engineer, in
first person plural, with nothing to sell and nothing to hide. Every claim is
concrete. Every decision carries its reason in the same breath. Numbers are
exact. Weak spots are stated as plainly as strengths, with what right would
look like attached. The register is calm, confident, and slightly
conversational — closer to a good code-review comment than to a whitepaper.
Australian English.

## Sentence mechanics

1. **First person plural, always the owner.** "We chose", "we route", "our
   VPC", "we acknowledge". Never "it was decided", never "the system was
   designed to", never "you should". If a decision happened, we made it.

2. **Decision and reason travel together.** The why arrives in the same
   sentence via an em-dash or "because", or in the very next sentence
   starting with "This".
   - Write: "This separation was intentional — the RAG database has
     fundamentally different I/O patterns than the transactional store."
   - Write: "We pin the connector to seven instances because cold-start
     latency was hurting the auth path."
   - Never leave a choice unexplained, and never explain it three paragraphs
     later.

3. **The em-dash is for elaboration and reason only.** It extends a thought
   with the mechanism or the why. It never sets up a punchline, a fragment,
   or a reversal (see Sentence structure and rhetoric below).

4. **Exact numbers, stated inline.** IPs, CIDRs, counts, percentages,
   latencies, versions, dollar figures: "(10.20.4.0/28)", "auto-scale between
   3 and 12 (currently 7 active)", "a 71.2% block rate", "2.4M embeddings".
   Approximations are marked honestly with ~ or "roughly". If the number
   isn't known, say that; never pad with "several" or "significant".

5. **Parenthetical precision.** Short parentheses carry the exact detail
   without breaking stride: "(PG16 — HA)", "(admin / editor / viewer)",
   "(currently 7 active)". One fact per parenthesis, kept short.

6. **Components get definitional openers.** The first sentence about a thing
   says what it is, usually with a spatial or role metaphor kept literal:
   "The atlas-connector is the bridge between our serverless runtime and our
   VPC." "The document table is the entry point." "The load balancer is the
   public entry point for all traffic."

7. **Mechanism before consequence.** Describe what happens, then state what
   it buys, as a plain consequence: "...routes through the VPC connector and
   out via the NAT gateway. This gives us a single, auditable egress point."
   The benefit is never an adjective; it is a result.

8. **Guided-reader moves.** When walking through anything sequential or
   visual, orient the reader explicitly: "Here is how a request flows, step
   by step:", "Reading the diagram top to bottom:", "At the top sits our
   edge layer:". Spatial verbs do the work: sits, feeds, routes, flows,
   terminates, attaches, bridges.

9. **Honest self-assessment with the correction attached.** Weaknesses are
   stated in full, with the number that proves them and the fix or the
   acceptance:
   - "At our current scale of 2.4M embeddings, this is likely suboptimal —
     the standard recommendation is lists = sqrt(rows), which would suggest
     ~1,550 lists. We are evaluating migration to HNSW indexes."
   - "...which is generous but acceptable for an internal development
     environment, and should be noted."
   - "We acknowledge some roles are still broader than necessary."
   Never bury a flaw, never dramatise one. The tone of admitting a problem is
   identical to the tone of describing a feature.

10. **Future intent is a plan, not a promise.** "We are evaluating...",
    "We plan to...", "We will re-evaluate when volume exceeds...". Hedges are
    specific ("likely", "currently", "at our current scale"), never vague
    ("may potentially", "in the future, possibly").

11. **Present tense for how the system behaves.** "All outbound traffic
    routes through...", "The frontend attaches an IAM token...". Past tense
    only for decisions and events: "We chose...", "This was a deliberate
    cost optimisation."

## Sentence structure and rhetoric — the general rules

These are classes of construction, not lists of banned phrases. Anything in
the class is out, including variants not shown here.

- **Complete declarative sentences only.** Subject, verb, object, in that
  order most of the time. No fragments for effect, no one-word sentences, no
  staccato runs, no inversion for drama ("Critical, this is"), no headline
  style. A sentence exists to state a fact, not to perform one.
- **Literal language throughout.** No figures of speech: no metaphors,
  similes, personification, idioms, or hyperbole. Role descriptions that
  read as literal engineering vocabulary are fine ("the bridge between the
  serverless runtime and our VPC", "the entry point") because they name a
  function, not an image. If a sentence paints a picture instead of stating
  a mechanism, rewrite it as the mechanism.
- **No contrast rhetoric of any kind.** The entire family is out: "X, not
  Y" / "not X but Y" / "less X, more Y" / "the real X is Y" reveals /
  antithesis pairs / "worse than X" setups — and negation-first definitions:
  "The reader is not one parser. It is a family of adapters." Define things
  by what they are; the corrected form is "The reader is a family of
  adapters, one per input shape." Deny a misconception only when readers
  genuinely hold it, in its own sentence, after the positive definition.
  When a distinction matters, give each side its own full sentence and let
  the facts carry the difference. "The path is location, never identity"
  becomes: "The path records location. Identity comes from the document id
  and does not change when the document moves."
- **No aphorisms, punchlines, or finality.** No maxims, no summary zingers,
  no closing lines engineered to land ("...and the fence survives"), no
  dramatic absolutes ("forever", "the quiet killer"). A section ends when
  its content ends.
- **Emphasis comes from specificity.** The strong version of a sentence has
  a number, a mechanism, or a named component in it — never an intensifier
  ("very", "extremely", "critically important"), an exclamation mark, or
  rhetorical weight. If a point feels weak, add the fact that proves it,
  not force.
- **Questions only when genuinely asking.** No rhetorical questions, no
  "So what does this mean?" transitions.

## Word choice

**Reach for:** deliberate, intentional, acknowledge, recognise, canonical,
fundamentally, generous but acceptable, should be noted, likely suboptimal,
auditable, the entry point, the bridge between, single point of, currently,
at our current scale, we are evaluating.

**Technical adjectives only** — an adjective must encode a fact: private,
internal, sliding, auditable, idempotent, stateless.

**Banned as classes:** marketing adjectives (robust, seamless, powerful,
cutting-edge, comprehensive, state-of-the-art), minimisers (simply, just),
"leverage" as a verb, "utilise" where "use" works, decorative separators
("·" and similar), second person — and every construction covered by the
Sentence structure and rhetoric section above.

**Spelling:** Australian — optimisation, utilisation, behaviour, recognise,
licence (noun) / license (verb).

## Rhythm and paragraph shape

- Sentences are medium length: one idea plus its elaboration. Long sentences
  are allowed when they are lists of concrete things; short sentences are
  rare and never used for drama.
- Paragraphs run two to four sentences and do one job: define a thing,
  explain a mechanism, or state a trade-off. A new job starts a new
  paragraph.
- Narrative stays in prose. Bullets appear only for genuinely enumerable
  items, each opened with a bold term and an em-dash elaboration.
- Transitions are quiet: "This", "That", "From there", "In practice". Never
  "Moreover", "Furthermore", "It is worth noting that".

## Calibration passages — hit this register

> The atlas-connector (10.20.4.0/28) is the bridge between our serverless
> runtime and our VPC. It runs on shared-core instances that auto-scale
> between 3 and 12 (currently 7 active). All services are configured with
> egress: ALL_TRAFFIC, meaning all outbound traffic — including calls to
> the cloud provider's APIs, the billing provider, and the transactional
> mail relay — routes through the VPC connector and out via the NAT
> gateway. This gives us a single, auditable egress point.

> The subchunks index is configured with lists=128. At our current scale of
> 2.4M embeddings, this is likely suboptimal — the standard recommendation
> is lists = sqrt(rows), which would suggest ~1,550 lists. We are evaluating
> migration to HNSW indexes for better recall at scale.

> The frontend implements the Backend-for-Frontend pattern. It serves static
> pages and exposes API routes under /api/v1/* that proxy requests to our
> backend services. This proxy layer is critical — it is where we attach IAM
> identity tokens for service-to-service authentication.

## Rewrite examples — generic register into this voice

Before: "A robust caching layer was implemented to significantly improve
performance."
After: "We cache embeddings by content hash — an unchanged chunk costs
nothing to re-ingest. This cut ingest cost by roughly 60% on routine edits."

Before: "It is worth noting that the current permission model may not be
optimal."
After: "The service account currently holds 8,412 permissions it does not
use. We recognise this is over-broad; remediation is scoped for the next
security pass."

Before: "The system seamlessly handles document updates."
After: "When a document changes, we reingest it in full and retire the
previous version's chunks from search. An unchanged section reuses its blurb
and embedding via the content hash, so a one-paragraph edit costs one model
call, not ninety."

## Process

Before writing, collect the exact figures the prose will need — versions,
counts, addresses, costs. Ask for what is missing or mark it as a
placeholder like [CIDR] and flag every placeholder at the end. Never invent
a number.
