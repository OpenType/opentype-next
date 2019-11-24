---
author: be5invis
---

# IDEA: Breaking the 64K limit

* **The OpenType-Next should support > 64K glyphs in one font.**
  * GID will be 32-bit.
* A special table could be provided, to indicate glyph subsets that could be used by legacy applications and libraries that expect GID being 16-bit.
  * Such glyph subsets are called “down-level glyph subset”.
  * An OpenType-Next font could have multiple down-level glyph subsets. A `STAT`-like mechanism could be used to fake the legacy applications, making them think there is a font family instead of a large font.
  * For each down-level subset, a bijection between 16-bit “Legacy GID”s of down-level glyphs and the corresponded 32-bit “Real GID”s, is required.
  * Absence of this table indicates that this font should never be used by legacy applications. Legacy applications should reject loading it.
* TTF component references – if still supported – will use to Real GID rather than Legacy GID.
* When processing in legacy software…
  * `CMAP`, `GSUB`, `COLR`, `SVG ` entries involving glyphs outside the down-level subset will be ignored.
  * `GPOS` will not be affected, since in legacy API we cannot use glyphs beyond the down-level subset.

