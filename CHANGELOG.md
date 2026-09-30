# CHANGELOG

All notable changes to this project are documented in this file.  
This project follows a progressive versioning model aligned with feature delivery milestones.

---

## [v8.0] - 2024 - Desktop Optimization & Adaptive Layout System

### Added
- Full desktop layout optimization for screens ≥ 1024px, implemented entirely via CSS without modifying JavaScript logic or DOM structure.
- Three-breakpoint responsive system: `768px` (tablet landscape), `1024px` (desktop), `1600px` (large screens) - layered on top of the existing mobile-first foundation.
- Multi-column CSS Grid layout at ≥ 1024px organizing content into: navigation column / card grid area / analysis panel.
- Hover interaction states for all interactive card components: `spec-card`, `arcano-card`, `wm-card`, `n52-carta`, `tir-card` - each with `translateY` lift and `box-shadow` depth on cursor entry.
- Custom scrollbar styling (`::webkit-scrollbar`) with brand-consistent purple thumb and minimal track.
- Fluid typography scaling via `clamp()` on major headings (`eb-h1`, `portal-h1`), preventing layout overflow on extreme viewport sizes.

### Improved
- Tab navigation bar (`eb-nav`) promoted to `position: sticky` with `backdrop-filter: blur(12px)` - remains anchored to the viewport top during vertical scroll, eliminating the need to scroll back to navigate between tabs on long content sections.
- Back button (`btn-voltar`) repositioned to `position: fixed` in the upper-left corner of the viewport at ≥ 1024px, always accessible regardless of scroll depth.
- Card grids (`arcanos-grade`, `wm-grid`, `tir-grid`) scaled to three columns via `repeat(auto-fill, minmax(300px, 1fr))`, providing better visual density and spatial balance on wide screens.
- Entity-specific card grid (`spec-grade`) expanded to two wide columns via `minmax(480px, 1fr)` for improved readability of long-form card content.
- Resolution grid (`res-naipe-lista`) reorganized into two columns at ≥ 1024px, reducing excessive vertical scrolling.
- Card illustration height increased: `arcano-img-wrap` from 180px to 220px, `wm-img-wrap` from 155px to 260px - proportional to the wider card footprint at desktop widths.
- Individual card modal (`sim-modal-card`) padded to `2.5rem 3rem` and max-width capped at `780px` for comfortable reading line length.
- Modal LUZ/SOMBRA section (`sim-modal-luz-sombra`) rendered in two columns, and Past/Present/Future section (`sim-modal-ppf`) rendered in three columns - eliminating the stacked single-column layout on large screens.
- Reading analysis panel (`slg-ppf`) rendered as a 3-column grid at ≥ 1024px, aligning each temporal position side by side.
- Content containers (`eb-wrap`, `sim-topo`) capped at `max-width: 1400px` and centered with `margin: 0 auto`, preventing layout stretch on ultra-wide displays.
- At ≥ 1600px, `eb-wrap` expands to `max-width: 1500px` and card grids scale to `minmax(320px, 1fr)` - maintaining proportional density without over-stretching.

### Technical
- All desktop rules are isolated within `@media (min-width: ...)` blocks appended to the end of the stylesheet - zero interference with the 14 existing `max-width` mobile adjustment queries.
- Tab bar sticky implementation uses negative `margin-left`/`margin-right` compensation (`-3rem`) with matching `padding-left`/`padding-right` to allow the sticky bar to span the full container width without expanding the layout container itself.
- `backdrop-filter` and `-webkit-backdrop-filter` applied in tandem for cross-browser compatibility on the sticky nav and fixed back button.

---

## [v7.0] - 2024 - Identity Consolidation & Nomenclature Standardization

### Changed
- Replaced generic tiragem titles across all three entity systems with proprietary names that reflect the cultural and spiritual identity of each entity, establishing a consistent nomenclature standard throughout the platform.

**Malandragem - Zé Pelintra:**
| Previous | Current |
|---|---|
| A Jogada Simples | O Chapéu do Malandro |
| A Encruzilhada | Os 3 Saravá |
| O Jogo do Malandro | Os Arcos da Lapa |
| O Baralho do Zé | As 7 Navalhas |
| A Mesa do Malandro | A Mesa do Malandro *(retained)* |
| O Reinado do Zé | Ginga da Malandragem |

**Pomba Gira 7 Rosas:**
| Previous | Current |
|---|---|
| A Pergunta da Rainha | Gargalhada da Moça |
| O Triângulo do Fogo | As 3 Rosas Vermelhas |
| A Cruz da Calunga | A Cruz da Calunga *(retained)* |
| O Altar da Rosa | As 7 Rosas |
| Os Sete Véus | Fios de Conta |
| O Ano da Rosa | Pétalas da Roseira |

**Exu Tatá Caveira:**
| Previous | Current |
|---|---|
| O Veredito | O Trono do Tatá |
| A Cruz Mestra | A Cruz do Cruzeiro |
| As Cinco Cruzes | Jogo dos Ossos |
| Os Sete da Calunga | O Sete da Calunga *(retained)* |
| A Revelação da Cruz | A Revelação das 9 Covas |
| O Ciclo da Calunga | O Ciclo da Calunga *(retained)* |

---

## [v6.0] - 2024 - Visual Layer: Arcanos Menores

### Added
- Full-resolution Rider-Waite illustrations rendered within each of the 56 Arcanos Menores cards, using original artwork sourced from the public domain Pictorial Key to the Tarot.

### Fixed
- Resolved `z-index` conflict between the image placeholder element and the card illustration, which previously caused the placeholder to render over the loaded image on mobile browsers.

### Refactored
- Unified and deduplicated CSS ruleset for `.wm-img-wrap`, `.wm-img`, `.wm-img-ph`, and `.wm-img-overlay` - eliminated three conflicting declarations accumulated across iterative development cycles.
- Applied `object-fit: contain` to card images, ensuring full card visibility without cropping, consistent with the rendering behavior of the Arcanos Maiores section.

---

## [v5.0] - 2024 - Structural Integrity & Navigation Stability

### Fixed
- Resolved critical HTML structural imbalance caused by mismatched `<div>` nesting across multiple entity sections (`mal`, `ros`, `cav`, `wai`). The imbalance was causing browser DOM misinterpretation, rendering tab content outside its parent element and making it inaccessible via CSS selectors used by `trocarTab()`.
- Corrected nesting depth of `sim-overlay` and `sim-tutorial` elements, which were being rendered inside the `eb-wai` ebook container instead of at root level - preventing the interactive game from initializing correctly.
- Restored visibility of Tiragens and Resoluções tabs across all three entity systems (`mal-tir`, `mal-res`, `ros-tir`, `ros-res`, `cav-tir`, `cav-res`).

### Refactored
- Removed redundant `wai-nai` (Ler com Naipes) and `wai-busca` (Busca) tabs from the Waite navigation, consolidating the search functionality into the persistent global search bar already present in the interface.
- Renamed the `wai-tir` navigation label from "Como Jogar" to "Tiragens" for semantic accuracy.

---

## [v4.0] - 2024 - Reading Intelligence & UX Refinement

### Added
- **Conselho Lúcido** block appended to the full reading analysis (`fazerLeituraGeral`): aggregates `conselho_pratico` fields from all revealed cards into a consolidated, actionable guidance section.
- Collapsible toggle (▲/▼) on the **Síntese Final** block within the full analysis panel.
- Collapsible toggle (▲/▼) on the **Carta Invertida - como ler** block within the individual card modal.

### Changed
- Replaced binary inverted card interpretation (automatic light/shadow swap) with a four-perspective model: **Bloqueio**, **Interiorização**, **Excesso**, **Ajuste** - removing deterministic negative framing and aligning with a contextual, non-fatalistic reading approach.
- Updated inverted card labels from "☽ ASPECTO SOMBRA (CARTA INVERTIDA)" to "☽ ASPECTO EM FOCO (INVERTIDA)", preserving both aspects visible to the reader without value hierarchy.

### Refactored
- Normalized `slg-reflexao-txt` CSS: removed `font-style: italic` and `font-family: Playfair Display`, replacing with `font-family: Inter` and `font-style: normal` for improved readability on mobile screens.
- Removed redundant `✶ REFLEXÃO E CONSELHO` label from the individual card modal - section context already established by the `CONSELHO` header element.

---

## [v3.0] - 2024 - Content Expansion & Navigation Features

### Added
- Integration of Rider-Waite original illustrations for all 22 Arcanos Maiores cards, rendered via the `arcano-img-wrap` component with gradient overlay and positional badge.
- Integration of Rider-Waite original illustrations for all 56 Arcanos Menores cards, with naipe-color-coded badge overlay.
- Global search bar (`filtrarWai78`) enabling cross-section lookup across all 78 Tarot cards by name, suit, or number - with intelligent Portuguese-language term parsing including synonym resolution (e.g., "ás" = "A", "valete" = "j" = "jota").
- Collapsible ibox (▲/▼) component applied universally across all content sections within all four systems.
- `56 ARCANOS MENORES · 14 POR NAIPE` counter header added to the `wai-men` tab, mirroring the `22 ARCANOS MAIORES` counter in `wai-mai`.
- "Cartas a retirar" ibox in the `spec/mm` and `cons` tabs of each entity system - specifying which cards to remove from the 52-card deck before playing.

### Changed
- Standardized figure card names across all Arcanos Menores from system-specific names (Mensageiro, Guardiã, Mestre) to canonical Tarot names: **Valete**, **Cavaleiro**, **Rainha**, **Rei**.
- Updated figure `data-nome-alt` attributes to include standard aliases for search compatibility.

### Fixed
- Corrected truncated text in the last `res-item` of each entity's Resoluções tab, which was causing `</div>` imbalance and content leakage between ebook sections.

---

## [v2.0] - 2024 - Interactive Consultation System

### Added
- **Interactive consultation game** (`sim-overlay`): full card draw simulation with shuffle animation, stop-to-select mechanic, and card reveal sequence.
- **Full reading analysis** (`fazerLeituraGeral`): automated generation of a complete reading panel including per-card breakdown (position, meaning, LUZ/SOMBRA, Passado/Presente/Tendência, conselho), reading statistics (Arcanos Maiores count, inverted cards, dominant suit), and Síntese Final.
- Inverted card system: 30% probability of inversion per draw, with visual `↓` indicator and distinct reading framing.
- `conselho_pratico` field rendered per card in both the individual modal (`abrirModalCarta`) and the full reading analysis panel.
- Six tiragem configurations: 1, 3, 5, 7, 10, and 13 cards, each with named positional layout (`POSICOES_TIRAGEM`) and descriptive label (`TIPOS_NOME`, `TIPOS_DESC`).

### Changed
- Extended the JSON data model for all 78 cards to include: `positivo`, `negativo`, `passado`, `presente`, `futuro`, `conselho`, `conselho_pratico`, `naipe_leitura`, `mesa_display`, `mesa_cor`.

---

## [v1.0] - 2024 - Initial Release

### Added
- Single-file web application (HTML5 + CSS3 + Vanilla JavaScript) with zero external dependencies.
- Main portal with four entry points: Malandragem, Pomba Gira 7 Rosas, Exu Tatá Caveira, and Tarot Rider-Waite.
- Individual ebook structure for each of the three entity systems, each containing six tabs: Baralho Específico (36 cards), Baralho de Consulta, Naipes 52 Cartas, Ler Sem o Baralho, Tiragens, and Resoluções.
- Tarot Rider-Waite system with four tabs: Arcanos Maiores (22 cards), Arcanos Menores (56 cards), Tiragens, and Resoluções.
- `trocarTab(eb, tab)` navigation function controlling tab visibility via CSS class toggling (`.eb-tab.ativo`).
- JSON dataset (`TODAS_CARTAS`) embedded inline containing all 78 Tarot cards with full metadata.
- 108 proprietary cards distributed across three entity systems (36 per system).
- 156 naipe resolutions (52 per entity system), one for each card in the standard 52-card deck.
- Suit correspondence system mapping standard playing card suits (♦♥♠♣) to the spiritual fields of each entity system.
- Mobile-first responsive layout using CSS Grid and Flexbox.
- Typography stack: Playfair Display · Bebas Neue · Inter.

---

*Sistemas Oraculares - May Sayuri*  
*lumin.up07@gmail.com - [@ah.moncheri](https://instagram.com/ah.moncheri)*
