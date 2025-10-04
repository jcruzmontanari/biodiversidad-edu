# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive educational biodiversity website for a school presentation featuring 11+ biodiversity elements (flowers, fruits, animals, natural objects). Each element has:
- Detailed educational information
- Interactive games (quiz, memory, drag & drop, true/false, matching)
- QR code access for mobile devices
- Modern, responsive design

## Technology Stack

- Pure HTML5/CSS3/JavaScript (no build tools or frameworks)
- Single-file components (each element is a standalone HTML file)
- Responsive design with CSS Grid and Flexbox
- Interactive games implemented in vanilla JavaScript

## File Structure

```
src/
├── index.html          # Main landing page with all elements
├── flores-rosas.html   # Template with quiz + matching game
├── pina.html           # Template with drag & drop game
├── coral.html          # Template with true/false game
├── hojas.html          # Template with part labeling game
├── pasto.html          # Template with memory game
├── jaguar.html         # Template with simple quiz
└── [other-elements].html
```

## Development Commands

**No build process required** - All files are static HTML. Simply open any HTML file in a browser.

**Local testing:**
```bash
# Use any static server, for example:
python3 -m http.server 8000
# or
npx serve src
```

## Architecture

### Page Structure
Each element page follows this pattern:
1. **Header section** - Title, emoji icon, scientific name with color gradient background
2. **Image container** - Hero image (Unsplash URLs or local)
3. **Info sections** - Educational content (2-3 paragraphs)
4. **Facts grid** - 4 data cards with key statistics
5. **Curiosity box** - Interesting fact
6. **Quiz section** - 3 multiple-choice questions
7. **Game section** - Interactive game (varies by template)

### CSS Color System
Each element has a unique gradient defined in two places:
- `index.html`: Card header background (lines ~181-213)
- Individual pages: Header gradient (line ~43)

Common gradients:
- Flores: `#ff9a9e to #fecfef` (pink)
- Coral: `#4facfe to #00f2fe` (blue)
- Hojas: `#56ab2f to #a8e063` (green)
- Jaguar: `#667eea to #764ba2` (purple)

### JavaScript Game Patterns

**Quiz System:**
- Variables: `score`, `answered`, `totalQuestions`
- `checkAnswer(questionNum, optionIndex, isCorrect)` - Handles answer clicks
- `updateScore()` - Shows final score and message
- `resetQuiz()` - Clears all answers for replay

**Matching Game (flores-rosas.html):**
- Variables: `selectedLeft`, `selectedRight`, `matchedPairs`
- `selectMatch(side, id, element)` - Handles item selection
- `checkMatch()` - Validates if pair matches via `data-id` attributes
- `resetMatching()` - Clears all matches

**Memory Game (pasto.html):**
- Cards flip on click, auto-flip back after 1 second if no match
- Uses `data-id` for matching logic

**Drag & Drop (pina.html):**
- HTML5 drag events: `ondragstart`, `ondrop`, `ondragover`
- Items move to drop zones when correctly placed

## Adding New Elements

1. Copy closest template based on desired game type
2. Update these sections:
   - Title and emoji (line ~49-52)
   - Scientific name (line ~56)
   - Header gradient colors (line ~43)
   - Image URL (line ~62)
   - All educational content (descriptions, facts, curiosity)
   - Quiz questions and answers (3 questions minimum)
   - Game content (adapt to new theme)
3. Add card to `index.html` grid (follow existing pattern at lines ~247-410)
4. Update card color class in index.html CSS (lines ~181-213)

## Important Implementation Notes

- **All pages are standalone** - CSS and JavaScript are inline, no external dependencies
- **Mobile-first responsive** - Grid collapses to single column on mobile (breakpoint: 768px)
- **Animation system** - Cards use staggered animations with `animation-delay`
- **QR codes** - Generated externally, not part of codebase (see README.md for instructions)
- **Images** - Use Unsplash URLs for quick development, can be replaced with local images

## Game Development Guidelines

When creating/modifying games:
- Provide clear instructions in `.game-instructions` div
- Show immediate feedback (green for correct, red for incorrect)
- Include score display after completion
- Add reset button that appears after game completion
- Disable interaction after answer/match to prevent double-clicks
- Use smooth CSS transitions (0.3s ease standard)

## Content Guidelines (from README.md)

- Target audience: 12 years old
- Language: Spanish (Argentina)
- Educational focus: biodiversity, ecosystems, conservation
- Each element should cover:
  - Basic description (2-3 paragraphs)
  - 4 key data points (size, lifespan, habitat, etc.)
  - One interesting curiosity
  - Ecological importance
  - 3 quiz questions with 3 options each

## Deployment

Project is running on Vercel

## Project Context

Created as a collaborative father-child educational project. The README.md contains extensive implementation guidance in Spanish, including content suggestions for each element, image URLs, and presentation tips.
