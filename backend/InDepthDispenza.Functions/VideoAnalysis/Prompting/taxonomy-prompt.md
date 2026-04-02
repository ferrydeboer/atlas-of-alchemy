# Taxonomy for Tag Extraction
Use the following taxonomy to extract structured tags from the transcript.

**Your taxonomy of existing tags:**
```json
{taxonomy}
```

---

## Taxonomy Structure

The taxonomy has four levels. Understanding what belongs at each level is essential for correct classification and for making good proposals.

**Type** — The fundamental nature of the outcome. Examples: `healing`, `manifestation`, `transformation`, `contribution`. Stable and corpus-independent. Never propose a new type unless a testimonial categorically fits nowhere else.

**Category** — The domain or system within which the outcome occurred. For `healing` this follows the medical system (neurological, cardiovascular, etc.). For other types it follows the nature of the outcome (financial, identity_shift, etc.). Always corpus-independent — the same categories must work across different speaker corpora.

**Subcategory** — The specific condition, experience, or outcome the person describes as their primary complaint or primary experience. This is the main classification level. A subcategory answers: *what did this person have or go through?*

**Attribute** — A descriptor that refines a subcategory without introducing a new entity. Attributes answer: *how severe, when, how confirmed, or which variant?* There are four valid attribute functions:
- **Severity or stage** — `stage_one` through `stage_four`, `advanced`, `metastatic`
- **Verification** — `medically_verified`, `scan_clear`, `full_remission`
- **Timing or context** — `during_meditation`, `during_retreat`, `spontaneous`
- **Subtype refinement** — `alcohol_addiction`, `type_1`, `type_2`, `mold_toxicity`

---

## Type Definitions

### transformation

`transformation` requires a **describable, pointable moment** — something the person can
locate in time. If no such moment is described, do not classify as transformation, even if
the person uses the word "transformation" or "changed." Gradual change over time belongs
in the `details` field of the healing or other achievement, not as a transformation entry.

**Three categories and when to use each:**

`somatic_breakthrough` — A physical or bodily event *during or immediately after* meditation
or coherence healing: energy surges, trembling, heat, involuntary movement, spontaneous
vocalization. No inner decision or realization is required — the physical event itself is
the achievement.

`identity_shift` — A lasting change in self-perception, self-worth, or life direction that
the person describes as a moment of knowing or decision. Includes: restored sense of
worthiness, lifelong behavioral pattern broken, boundary set for the first time — and
**any irreversible decision or action taken from inner guidance**, even if quiet and
undramatic. If someone stopped chemo, left a job, or ended a relationship because an inner
knowing overrode external reasoning, that is `identity_shift`. The decision is the moment.
Use `inner_guidance_followed` as subcategory when the person explicitly frames it as
following an inner voice, signal, or knowing. Use `surrender_moment` when they describe
consciously releasing control after resistance.

`mystical_experience` — An altered perception of reality, time, space, or self *during
meditation*. Must be an **internal** experience — a vision, dissolution of self, sense of
oneness, akashic insight, encounter with a presence. An external sign (thunder, a found
object, skywriting) is NOT a mystical_experience — it belongs in
`manifestation > synchronicity`.

---

### transformation vs manifestation — the decisive question

> Did this happen *inside* the person, or *outside* in the world?
> - Inside (internal state change) → `transformation`
> - Outside (external object, event, circumstance) → `manifestation > synchronicity`

A single event often produces both. The skywriting is `manifestation > synchronicity`.
The internal surrender or decision that followed it is a separate
`transformation > identity_shift` achievement. **Extract both when both are present.**

---

### healing vs transformation

A physical symptom improving or resolving is always `healing`, even if it followed a
meditation experience. The meditation experience *itself* — if described as notable — is a
separate `transformation` achievement. Extract both when both are present.

---

## Completeness Check

Before finalizing your response, verify:

- [ ] Every distinct reported outcome extracted — not only the most dramatic one?
- [ ] Did the person describe a quiet decision or inner knowing that changed their course?
  If yes → `transformation > identity_shift` (subcategory: `inner_guidance_followed`
  or `surrender_moment`)
- [ ] Did the person describe what the meditation *felt like*, separately from what healed?
  If yes → consider `transformation > somatic_breakthrough` or `mystical_experience`
- [ ] Did the person describe an external sign or synchronicity separately from an inner
  response to it? If yes → extract both `manifestation > synchronicity` and
  `transformation > identity_shift`
- [ ] Did the person share the work with others as a concrete act outside this testimonial?
  If yes → `contribution` (the act must be described, not merely implied)

---

## Tag Extraction Rules

1. **Use existing tags** — Always prefer existing taxonomy tags. Search the entire taxonomy before considering a proposal.
2. **Maintain hierarchy** — Every achievement must include the type, category, and at least one subcategory. Attributes are optional.
3. **Always include parent tags** — When using `cervical_cancer`, also include `cancer` and `healing` in the tags array.
4. **Always include a subcategory** — A category tag like `cancer` must never appear alone. There must always be at least one subcategory alongside it.
5. **Optionally include attributes** — Add attributes only when they genuinely refine the subcategory. Do not add attributes for their own sake.

---

## Deciding Between Subcategory and Attribute

Ask: *does this introduce something new the person had or experienced, or does it describe something already named?*

- `type_2` does not introduce a new condition — it refines `diabetes` → **attribute**
- `depression` introduces a new condition → **subcategory**
- `brain_fog` is the primary complaint in many testimonials → **subcategory**, not an attribute
- `medically_verified` describes how a result was confirmed, not the result itself → **attribute**
- `during_retreat` describes when something happened, not what happened → **attribute**

If something fits none of the four attribute functions, it is almost certainly a subcategory.

---

### Classification Boundaries

**`contribution` requires action beyond the testimonial itself.**
The act of giving a testimonial, sharing a healing story at a retreat, or appearing in a video is NOT a contribution achievement — it is the video itself. Do not classify the testimony as `contribution > teaching_or_sharing > public_testimony` unless the person describes a distinct act of outreach, advocacy, or sharing that exists independently of this video. Examples of valid `public_testimony`: testifying before a legislative body, publishing a book about their experience, speaking at an independent public event. Examples of invalid use: "shared her story at the retreat," "gave this testimonial to help others."

---
## Proposal Rules

Proposals belong inside the related achievement. The `proposals` array should frequently be empty — that means the taxonomy is working well.

**Only propose when all of the following are true:**
1. The content clearly does not match any existing tag anywhere in the taxonomy
2. The tag would be reusable across multiple testimonials, not a one-off mention
3. The proposed tag is corpus-independent — it would apply equally to other speaker corpora

**What level to propose at:**
- Propose a **subcategory** when the testimonial names a specific, distinct condition or experience not yet in the taxonomy (e.g. a named diagnosis, a distinct type of mystical experience)
- Propose an **attribute** only when it fits one of the four attribute functions and the value is genuinely reusable
- You may propose a new category or even a new type if nothing in the existing structure fits — but this should be rare

**Never propose:**
- Tags that already exist anywhere in the taxonomy tree
- Attributes that are symptoms or descriptions better captured in the `details` field
- Tags specific to a single testimonial that will not generalize
- Corpus-specific proper nouns as subcategories (event names, brand terms, speaker-specific phrases)