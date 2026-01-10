# AGENTS.md

This file provides guidance for AI agents working on the Fractal Boston website. It documents patterns, conventions, and learnings to ensure consistency across changes.

## Repository Overview

This is a **static website** built with vanilla HTML, CSS, and minimal JavaScript:
- No build process, frameworks, or package managers
- Main file: `index.html`
- Styles: `styles.css` (custom) + `normalize.css` (reset)
- Deployment: GitHub Pages (via `CNAME` file)

## Site Structure

The site uses a card-based layout with organic, playful shapes:
- **Header**: H1 title with floating decorative elements
- **Hero Section**: Main CTA and community description
- **Activities Section**: Multiple subsections (dinners, classes, coworking, etc.)
- **Luma Calendar**: Event calendar subscription
- **Stay Connected**: Newsletter signup and contact info

## Styling Patterns & Conventions

### Design Philosophy

The site uses an **organic, playful aesthetic** with:
- Irregular border-radius values that feel hand-drawn
- Subtle gradients with green tints (`#f0fdf4`)
- Gentle rotations on elements (`rotate(-0.5deg)`)
- Decorative shapes and floating animations
- Main color: `--main-color: #059669` (green)

### Content Section Classes

Each major content section typically has a custom class (e.g., `.education-block`, `.luma-calendar`, `.coworking-block`) with:

1. **Background gradient** with subtle green tint
2. **Organic border-radius** for uniqueness
3. **Optional h3 styling** for section headings

### Creating a New Section: Step-by-Step

When adding a new content section, follow this pattern:

#### 1. HTML Structure

```html
<div class="your-section-name card">
  <h3>Section Title</h3>
  <p>Your content here...</p>
  <!-- Optional: buttons, links, images -->
</div>
```

#### 2. CSS Styling - Background & Shape

Add a class in `styles.css` with:

```css
.your-section-name {
  background: linear-gradient(XXXdeg, #fefefe 0%, #f0fdf4 100%);
  border-radius: YYpx ZZpx AApx BBpx / CC% DD% EE% FF%;
}
```

**Key points:**
- **Gradient direction**: Vary the angle (105deg, 285deg, etc.) to make each section unique
- **Always use**: `#fefefe` (near-white) to `#f0fdf4` (subtle green tint)
- **Border-radius**: Use 8 values (4 corners with x/y for each) with irregular numbers to create organic shapes
- **Inspiration**: Look at `.education-block` (105deg) and `.luma-calendar` (285deg) for examples

#### 3. CSS Styling - H3 Underline (Optional)

If your section needs a longer h3 underline (like activities sections), add:

```css
.your-section-name h3::after {
  transform: scaleX(0.6) rotate(-0.8deg);
}
```

**Key points:**
- Default h3 underline: `scaleX(0.2)` (short)
- Activities-style underline: `scaleX(0.6)` (longer, more prominent)
- Vary the rotation slightly: `-0.5deg`, `-0.8deg`, `-1.2deg`
- This makes section headings stand out more

### H3 Underline System

The site uses a progressive underline system for h3 elements:

```css
/* Default: short underline for most h3s */
h3::after {
  transform: scaleX(0.2) rotate(-0.5deg);
}

/* Activities sections: longer underline */
.activities-section h3::after {
  transform: scaleX(0.6) rotate(-1.2deg);
}

/* Luma calendar: longer underline */
.luma-calendar h3::after {
  transform: scaleX(0.6) rotate(-0.8deg);
}

/* Stay connected: no underline */
.stay-connected h3::after {
  display: none;
}
```

**When to use longer underlines** (scaleX(0.6)):
- Major content sections with multiple paragraphs
- Sections that introduce new topics/activities
- Anywhere you want extra visual hierarchy

### Call-to-Action (CTA) Patterns

#### Main CTA (Hero Button)

```html
<a href="URL" target="_blank" rel="noopener noreferrer nofollow" class="main-cta">
  <button class="block accent">✨ Text ✨</button>
</a>
```

**Current main CTAs link to**: `https://fractal.boston/discord`

#### Secondary CTA (Block Button)

```html
<a href="URL" target="_blank" style="text-decoration: none;">
  <button class="block">Button Text</button>
</a>
```

**Key points:**
- Use `style="text-decoration: none;"` to remove underlines from buttons
- Don't over-use emojis in button text unless explicitly requested
- Keep button text concise and action-oriented

### Link Patterns

The site uses two main link patterns:

1. **External links**: Always include `target="_blank" rel="noopener noreferrer nofollow"`
2. **Discord invite**: Use `https://fractal.boston/discord` (canonical URL, not direct Discord link)

## Common Tasks

### Updating CTAs/Links

When updating calls-to-action:
1. Check both hero section and footer
2. Update link URLs and button/link text consistently
3. Ensure proper rel attributes for external links

### Adding Event Content

Follow the pattern in `.activities-section`:
- Use `.event-block` for image galleries
- Use `.event-photo` class for images
- Wrap content in semantic tags

### Styling Guidelines

- **Avoid inline styles** except for rare cases (like removing text-decoration)
- **Use CSS variables**: `var(--main-color)`, `var(--text-color)`, etc.
- **Test responsiveness**: Site has breakpoints at 650px, 480px
- **Keep animations subtle**: Site uses gentle float/wobble animations

## Learnings from Recent Sessions

### Session: Discord Links & Luma Calendar Styling (Jan 2026)

**Task**: Update Discord links and style the Luma calendar section

**Changes Made**:
1. Updated hero "Join the Crew" button: `https://forms.gle/...` → `https://fractal.boston/discord`
2. Updated footer CTA text: "Fill out our interest form" → "Introduce yourself in Discord"
3. Styled `.luma-calendar` section with gradient and border-radius
4. Extended `.luma-calendar h3::after` underline from scaleX(0.2) to scaleX(0.6)
5. Rewrote calendar section copy to be more inviting and concise

**Key Insights**:
- When styling a new section, ALWAYS check if it needs an h3::after adjustment
- Gradient direction matters: reverse it (105deg → 285deg) for visual variety
- Border-radius should have 8 values for organic feel
- Button text should be action-oriented: "Open calendar" not "View the Luma calendar"
- Remove text-decoration from button links with inline style when needed

**Pattern Established**:
```css
/* Step 1: Add gradient background */
.new-section {
  background: linear-gradient(285deg, #fefefe 0%, #f0fdf4 100%);
  border-radius: 22px 30px 18px 35px / 28% 35% 32% 25%;
}

/* Step 2: Extend h3 underline if needed */
.new-section h3::after {
  transform: scaleX(0.6) rotate(-0.8deg);
}
```

## Best Practices

### Before Making Changes
1. Read existing code to understand current patterns
2. Check for similar sections to maintain consistency
3. Use `git diff` before committing to review changes

### Writing Commit Messages
- Keep first line concise (50 chars or less)
- Use imperative mood: "Update" not "Updated"
- Add details in commit body when needed
- Group related changes together

### Testing
- Open `index.html` in a browser to preview changes
- Test on mobile viewport (check responsive styles)
- Verify links open correctly

## Reference Examples

### Well-Styled Sections

**Education Block** (subtle gradient, flowing left):
```css
.education-block {
  background: linear-gradient(105deg, #fefefe 0%, #f0fdf4 100%);
  border-radius: 18px 35px 22px 28px / 32% 25% 40% 35%;
}
```

**Luma Calendar** (subtle gradient, flowing right):
```css
.luma-calendar {
  background: linear-gradient(285deg, #fefefe 0%, #f0fdf4 100%);
  border-radius: 22px 30px 18px 35px / 28% 35% 32% 25%;
}
.luma-calendar h3::after {
  transform: scaleX(0.6) rotate(-0.8deg);
}
```

### Copy Writing Style

- **Concise**: Prefer shorter, punchier sentences
- **Inviting**: Use "Subscribe to stay in the loop" over longer explanations
- **Action-oriented**: "Open calendar" over "View the Luma calendar"
- **Friendly**: Maintain warm, community-focused tone

## Future Considerations

- Keep site lightweight: avoid adding frameworks or build tools
- Maintain organic aesthetic: irregular shapes, gentle animations
- Update CLAUDE.md if project structure changes significantly
- Document new patterns in this file as they emerge
