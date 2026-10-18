# I Ching 64 Hexagrams Dataset

> **Free, open-source, structured dataset of the 64 I Ching hexagrams in English, Simplified Chinese, and Traditional Chinese.**
>
> Maintained by [DaoPaths.com](https://daopaths.com) — Authentic Chinese Metaphysics Online

[![License: CC0-1.0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)
[![JSON](https://img.shields.io/badge/Format-JSON-blue.svg)](https://www.json.org/)
[![Languages](https://img.shields.io/badge/Languages-3-green.svg)](https://daopaths.com)

---

## Overview

This dataset contains all 64 hexagrams of the I Ching (易经, Book of Changes), one of the oldest Chinese classical texts, in three languages:

- **English** (`iching-64-hexagrams.en.json`)
- **Simplified Chinese** (`iching-64-hexagrams.zh.json`)
- **Traditional Chinese** (`iching-64-hexagrams.zh-hant.json`)

Each hexagram includes:

- **Structural metadata**: number, Chinese name, pinyin, English translation, unicode symbol, upper/lower trigrams, five-element attribution, yin-yang classification
- **Classical text**: the Judgment (卦辞) in English and Chinese
- **Modern interpretation**: core meaning, description, and detailed HTML reading
- **Reference URL**: link to the full reading on DaoPaths.com

## Use Cases

- **Divination apps**: Build I Ching casting tools, mobile apps, or web widgets
- **Academic research**: Analyze hexagram structure, trigram relationships, or textual patterns
- **Machine learning**: Train NLP models on classical Chinese texts with English translations
- **Data visualization**: Create interactive hexagram charts, King Wen sequence diagrams, or trigram networks
- **Educational tools**: Teach Chinese philosophy, divination, or classical Chinese language

## Data Schema

Each hexagram is a JSON object with the following fields:

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `number` | integer | Hexagram number (1-64) in King Wen sequence | `1` |
| `slug` | string | URL-friendly identifier | `"hexagram-1"` |
| `chinese` | string | Chinese name (single character) | `"乾"` |
| `pinyin` | string | Romanization with tone marks | `"Qián"` |
| `english` | string | English translation | `"The Creative"` |
| `symbol` | string | Unicode hexagram symbol | `"䷀"` |
| `unicode` | string | Same as `symbol` (for compatibility) | `"䷀"` |
| `upper_trigram` | string | Upper trigram with unicode symbol | `"乾☰"` |
| `lower_trigram` | string | Lower trigram with unicode symbol | `"乾☰"` |
| `element` | string | Five-element attribution | `"Metal"` |
| `yin_yang` | string | Yin or Yang classification | `"Yang"` |
| `title` | string | Full page title (SEO-optimized) | `"Hexagram 1: 乾为天 (The Creative) — I Ching Meaning & Reading"` |
| `description` | string | Short description for meta tags | `"Hexagram 1 (Qián — The Creative): meaning, judgment and guidance..."` |
| `judgment` | string | Classical Judgment text (卦辞) | `"The Creative works sublime success, furthering through perseverance."` |
| `core_meaning` | string | Modern interpretation of core meaning | `"Heaven in motion: strength, initiative and leadership at their peak."` |
| `html` | string | Full HTML reading (judgment, core meaning, career, love, wealth, health, advice) | `"<p class=\"hex-symbol\">䷀</p>\n<h2>The Judgment</h2>..."` |
| `url` | string | Full reading URL on DaoPaths.com | `"https://daopaths.com/i-ching/hexagram-1"` |

## Example

```json
{
  "number": 1,
  "slug": "hexagram-1",
  "chinese": "乾",
  "pinyin": "Qián",
  "english": "The Creative",
  "symbol": "䷀",
  "unicode": "䷀",
  "upper_trigram": "乾☰",
  "lower_trigram": "乾☰",
  "element": "Metal",
  "yin_yang": "Yang",
  "title": "Hexagram 1: 乾为天 (The Creative) — I Ching Meaning & Reading",
  "description": "Hexagram 1 (Qián — The Creative): meaning, judgment and guidance for career, love, wealth and health. Heaven in motion: strength, initiative and leadership at their peak.",
  "judgment": "The Creative works sublime success, furthering through perseverance.",
  "core_meaning": "Heaven in motion: strength, initiative and leadership at their peak.",
  "html": "<p class=\"hex-symbol\">䷀</p>\n<h2>The Judgment</h2>\n<blockquote><p>The Creative works sublime success, furthering through perseverance.</p></blockquote>\n<h2>Core Meaning</h2>\n<p>Heaven in motion: strength, initiative and leadership at their peak.</p>...",
  "url": "https://daopaths.com/i-ching/hexagram-1"
}
```

## File Structure

```
iching-dataset/
├── README.md                          # This file
├── LICENSE                            # CC0 1.0 Universal (Public Domain)
├── iching-64-hexagrams.en.json        # English (160 KB)
├── iching-64-hexagrams.zh.json        # Simplified Chinese (130 KB)
└── iching-64-hexagrams.zh-hant.json   # Traditional Chinese (127 KB)
```

## Usage Examples

### Python

```python
import json

# Load English dataset
with open('iching-64-hexagrams.en.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

# Get all hexagrams
hexagrams = data['hexagrams']

# Find hexagram by number
hexagram_1 = next(h for h in hexagrams if h['number'] == 1)
print(hexagram_1['english'])  # "The Creative"
print(hexagram_1['judgment'])  # "The Creative works sublime success..."

# Filter by element
fire_hexagrams = [h for h in hexagrams if h['element'] == 'Fire']
print(f"Fire hexagrams: {[h['chinese'] for h in fire_hexagrams]}")

# Random hexagram (for divination)
import random
cast = random.choice(hexagrams)
print(f"Your hexagram: {cast['chinese']} ({cast['english']})")
print(cast['core_meaning'])
```

### JavaScript / Node.js

```javascript
const fs = require('fs');

// Load English dataset
const data = JSON.parse(fs.readFileSync('iching-64-hexagrams.en.json', 'utf-8'));
const hexagrams = data.hexagrams;

// Find hexagram by name
const creative = hexagrams.find(h => h.english === 'The Creative');
console.log(creative.symbol);  // "䷀"

// Get all Yang hexagrams
const yangHexagrams = hexagrams.filter(h => h.yin_yang === 'Yang');
console.log(`Yang hexagrams: ${yangHexagrams.length}`);
```

### Command Line (jq)

```bash
# Get all hexagram names
jq '.hexagrams[].english' iching-64-hexagrams.en.json

# Find hexagram 64
jq '.hexagrams[] | select(.number == 64)' iching-64-hexagrams.en.json

# Count hexagrams by element
jq '.hexagrams | group_by(.element) | map({element: .[0].element, count: length})' iching-64-hexagrams.en.json
```

## Data Sources

- **Classical text**: The Judgment (卦辞) follows the received text of the *Zhou Yi* (周易), the earliest layer of the I Ching, dating to the Western Zhou dynasty (1046–771 BCE).
- **English translation**: Based on the Legge (1882), Wilhelm-Baynes (1950), and Lynn (1994) translations, with modern scholarly corrections.
- **Modern interpretation**: Original commentary by DaoPaths.com, grounded in the Ten Wings (十翼) commentary tradition.
- **Trigram attributions**: Five-element and yin-yang classifications follow the *Xi Ci Zhuan* (系辞传) and later Han dynasty commentaries.

## Related Resources

- **[DaoPaths.com](https://daopaths.com)** — Free online I Ching divination, BaZi charting, Feng Shui tools, and Chinese zodiac forecasts
- **[I Ching Online](https://daopaths.com/i-ching)** — Cast the 64 hexagrams online with the King Wen sequence
- **[Daoist Wiki](https://daopaths.com/wiki)** — In-depth articles on I Ching interpretation, trigram symbolism, and divination history

## Contributing

This dataset is maintained by [DaoPaths.com](https://daopaths.com). If you find errors or have suggestions:

1. **Open an issue** on this repository
2. **Email us**: contact@daopaths.com
3. **Submit a pull request** with corrections (please cite classical sources)

## License

**CC0 1.0 Universal (Public Domain)**

This dataset is released into the public domain. You may:

- ✅ Use it for commercial projects
- ✅ Modify and redistribute it
- ✅ Use it in academic research
- ✅ Train AI models on it

**No attribution required**, but a link back to [DaoPaths.com](https://daopaths.com) is appreciated.

## Citation

If you use this dataset in academic work, please cite:

```bibtex
@dataset{daopaths_iching_2026,
  title={I Ching 64 Hexagrams Dataset},
  author={DaoPaths.com},
  year={2026},
  url={https://daopaths.com/i-ching},
  license={CC0-1.0}
}
```

---

**Made with ☯️ by [DaoPaths.com](https://daopaths.com)**
