# LandBase

**A land-count recommender for Magic: The Gathering Commander decks, built for an intro CS course.**

Given a decklist, LandBase estimates how many of each basic land type you should run based on the color-pip distribution of your deck's spells — decks that lean heavily on one color get proportionally more of that basic, rather than an even split.

## How it works

1. Pulls card data from a local [Scryfall](https://scryfall.com/) bulk-data snapshot (`scryfall_all.json`) to look up each card's mana cost, color identity, and type.
2. Counts colored mana symbols ("pips") across the whole deck.
3. Recommends a basic-land count for each color, proportional to that color's share of total pips, then rounds and reconciles the totals so the recommended count always matches your actual land slots.

Decks can be loaded three ways:
- **Upload a decklist file**
- **Archidekt username + deck name** (searches Archidekt for the matching deck)
- **Archidekt deck URL** (pulls the decklist directly via Archidekt's API)

## Tech

Python with a `tkinter` desktop GUI. `requests` + `BeautifulSoup` handle the Archidekt search/scrape; the Archidekt API is used directly when a deck URL is available.

## Running it

```bash
pip install requests beautifulsoup4
python ui.py
```

`ui.py` is the entry point — it launches the desktop app.

## Status

This was a course project for an intro to Computer Science class, built as a first pass at the problem. Known limitations (some noted as in-progress in the code):
- Doesn't yet account for modal double-faced cards' alternate mana costs
- Doesn't substitute nonbasic lands for basics — recommendations are basics-only for now
- No color-fixing logic beyond raw pip counts (e.g. Frank Karsten-style mana-base ratios)
