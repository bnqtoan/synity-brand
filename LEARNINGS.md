# SYNITY Logo Project - Learnings

## Project Overview
- **Client:** SYNITY - Digital transformation & CTO-as-a-Service for SMEs
- **Deliverables:** Logo, mockups, brand guidelines
- **Tool:** Brand Vibe skill + Gemini 3 Pro Image API

---

## Key Learnings

### 1. Brand Research Phase

**What worked:**
- Reading client's actual website content (SYNITY.md) for positioning
- Understanding target market: education/training & service businesses, 1-2B VND/month revenue
- Extracting brand promise: "80% automation in 90 days"

**Insight:** Logo direction should reflect "enterprise consulting" not "tech startup" - premium, authoritative, not playful.

---

### 2. Logo Generation

**Initial failures:**
- First 6 options looked too "startup SaaS" - colorful, generic tech symbols
- Didn't match client's existing dark premium aesthetic

**Breakthrough:**
- Analyzed client's hero banner screenshot
- Identified existing style: dark navy #0a0e1a, gradient text, premium feel
- Generated `synity_v2_01.png` matching this direction

**Winning concept:**
- Clean wordmark "SYNITY"
- Final Y has upward curved flourish (represents growth/aspiration)
- No icons or symbols - pure typography

---

### 3. Logo Consistency in Mockups

**Problem:** Gemini interprets logos rather than copying exactly.

**Failed approaches:**
- Vague descriptions: "Y with flourish" → inconsistent results
- Single reference image → logo still varies

**Successful approaches:**

1. **Precise description:**
   ```
   BAD:  "Y with flourish"
   GOOD: "final letter Y has right diagonal stroke extending upward as elegant curved line going up-right"
   ```

2. **Negative instructions:**
   ```
   "NO swoosh on other letters - ONLY final Y"
   "NO icons above text - pure wordmark"
   ```

3. **Use successful output as reference** for consistency

---

### 4. Multi-Reference Generation (NEW CAPABILITY)

**Problem:** Need both correct logo AND specific person's face in ceremony mockup.

**Solution:** Added `-r2` flag to script for second reference image.

```bash
python3 scripts/generate.py "BRAND" "industry" -m \
  -r "scene_with_correct_logo.png" \
  -r2 "founder_face.jpeg" \
  -o "output.png" \
  -e "Combine scene from image 1 with person appearance from image 2"
```

**Result:** `synity_ceremony_2ref.png` - correct logo + founder-like appearance

---

### 5. Mockup Success Rates

| Mockup Type | Logo Accuracy | Notes |
|-------------|---------------|-------|
| Business card | 80% | Simple, works well |
| Stationery set | 60% | May add unwanted icon variations |
| Presentation screen | 85% | Good for wordmarks |
| Ceremony/event | 70% | Use 2-ref for face+logo |
| Vehicle wrap | 90% | Simple placement |
| Apparel | 85% | Good embroidery simulation |
| Social banner | 80% | May add decorative elements |

---

### 6. 2-Round Approach

When single generation fails:

```
Round 1: Generate with logo reference → correct logo, generic face
Round 2: Use Round 1 output + face reference → merge both
```

This preserves logo while improving specific elements.

---

### 7. Script Improvements Made

Added to `generate.py`:
- `-r2` flag for second reference image
- Multi-image support in API call
- Updated from "Logo Pro Max" to "Brand Vibe" naming

---

## Prompt Templates That Work

### Stationery
```
Premium corporate stationery flat lay on dark [color] surface.
Items: business cards, letterhead, envelope, pen.
Logo: [BRAND] wordmark - [precise logo description].
Full wordmark on ALL items - no abbreviations.
Photorealistic, matte textures, premium consulting aesthetic.
```

### Ceremony with founder
```
Corporate keynote event.
Speaker: [detailed appearance from ref2].
Behind: large screen with [BRAND] logo - [precise logo description].
Professional conference hall, [color] lighting, audience in formal attire.
Combine scene from image 1 with person from image 2.
```

---

## Files Generated

| File | Purpose |
|------|---------|
| `synity_v2_01.png` | Primary logo |
| `synity_mockup_01.png` | Business card on marble |
| `synity_mockup_03.png` | Office lobby signage |
| `synity_mockup_stationery4.png` | Stationery set |
| `synity_mockup_presentation.png` | Conference room screen |
| `synity_mockup_meeting.png` | Boardroom |
| `synity_mockup_tshirt.png` | Polo shirt |
| `synity_mockup_lanyard.png` | Event badge |
| `synity_mockup_social.png` | LinkedIn banner |
| `synity_mockup_vehicle.png` | Car wrap |
| `synity_ceremony_2ref.png` | Keynote with founder |
| `brand-guidelines.html` | Brand guidelines page |

---

## What AI Can't Do Well

1. **Exact logo replication** - always interprets/varies
2. **Precise negative space** - FedEx-level hidden meanings fail
3. **Exact face likeness** - general appearance only
4. **Consistent style across generations** - each is independent

## What AI Does Well

1. **Rapid concept exploration** - 10+ directions quickly
2. **Photorealistic mockups** - convincing product shots
3. **Style matching** - can follow brand aesthetic
4. **Scene composition** - professional layouts

---

## Recommendations for Future Projects

1. **Start with brand research** - understand positioning before generating
2. **Match existing visual identity** - analyze client's current materials
3. **Be extremely specific** about logo details in every prompt
4. **Use successful outputs as references** for consistency
5. **Use 2-ref approach** for complex mockups needing multiple elements
6. **Expect 3-5 iterations** per mockup type for best results
7. **Final logo should be recreated in Illustrator** - AI output is starting point
