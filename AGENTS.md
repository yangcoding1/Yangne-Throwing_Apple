<!-- Generated: 2026-05-14 | Updated: 2026-05-14 -->

# TSTORY_SKIN

## Purpose
A Tistory blog skin project combining Apple/Toss-inspired design with Tistory's substitution variable (치환자) system. The goal is to produce a production-ready skin with a minimal, modern aesthetic — think Apple's whitespace discipline and Toss's depth design — that is fully responsive and supports dark mode.

## Key Files

| File | Description |
|------|-------------|
| `디자인_시스템_명세서.md` | Design system spec: color palette (light/dark), typography scale, component styles (buttons, cards, shadows) |
| `와이어프레임_설계_가이드.md` | Wireframe principles: visual hierarchy, negative space, responsive layout, user flow, interaction logic |
| `메인_페이지_와이어프레임_상세_명세서.md` | Detailed main page wireframe: sticky header, hero section, article list layout, sidebar, micro-interactions |
| `상세_페이지_와이어프레임_상세_명세서.md` | Detailed post page wireframe: dark mode toggle, scroll progress bar, floating TOC, 2-column layout |
| `mock-up.png` | Visual mockup of the intended design |

## Subdirectories

| Directory | Purpose |
|-----------|---------|
| `document-tistory-skin/` | Tistory skin API reference and substitution variable documentation (see `document-tistory-skin/AGENTS.md`) |

## For AI Agents

### Working In This Directory
- The actual skin output files (`skin.html`, `style.css`, `index.xml`) do not exist yet — this project is in the design/specification phase
- All spec files are in Korean; treat them as the single source of truth for design decisions
- When generating skin code, consult `document-tistory-skin/` for the correct substitution variable syntax and structure
- The target Tistory skin file structure is: `index.xml`, `skin.html`, `style.css`, preview images, and an `images/` folder for assets

### Design System Summary (from spec files)
**Light mode (Apple Minimal):**
- Background: `#FBFBFD`, Surface/Card: `#FFFFFF`, Text Primary: `#1D1D1F`, Text Secondary: `#86868B`, Accent: `#007AFF`

**Dark mode (Toss Depth):**
- Background: `#111111`, Surface/Card: `#1C1C1E`, Text Primary: `#F5F5F7`, Text Secondary: `#8E8E93`, Accent: `#3182F6`

**Typography:** Pretendard as primary font; Post Title 2.5rem/Bold, Section Header 1.5rem/Bold, Body 1.125rem/Regular (line-height 1.8), Metadata 0.875rem/Gray

**Components:** Buttons with `border-radius: 12px`, Cards `18–24px`, click feedback via `scale(0.96)`, shadows `0 4px 20px rgba(0,0,0,0.05)` light / `rgba(0,0,0,0.2)` dark

**Transitions:** Dark mode `0.4s ease`; Micro-interactions `cubic-bezier(0.4, 0, 0.2, 1)` at `0.3s`

### Main Page Layout
- Sticky header: blurred background, blog title left / nav links + search icon right
- Hero section: custom background image with overlay, glassmorphism profile card (bottom-left)
- Article list: text/info left + 120×120px thumbnail right, category chip + date metadata
- Sidebar: ~25–30% width, category card with hover slide animation
- Micro-interactions: card lift `translateY(-4px)`, thumbnail zoom `scale(1.1)` on hover

### Post Page Layout
- Dark mode toggle in header; scroll progress bar (2px) beneath header
- 2-column: body 70% (max 800px) + sidebar 30%
- Sticky floating TOC: highlights current section, smooth scroll on click

### Testing Requirements
- Test in both light and dark mode
- Verify responsive behavior: sidebar should collapse/hide on mobile
- Upload to Tistory skin editor and validate substitution variables render correctly

## Dependencies

### External
- Tistory platform — substitution variable rendering engine
- Pretendard font — primary typeface

<!-- MANUAL: -->
