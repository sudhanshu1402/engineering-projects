# UNO

Terminal UNO played against a simple computer opponent. One file, no dependencies.

## What it does

A text version of UNO for one human player versus the PC. You each start with 7 cards, a starting card is flipped, and you take turns matching by color, rank, or playing a wild. First to empty their hand wins. Everything runs in the terminal with `input()` prompts and short `time.sleep` pauses so the PC's moves are readable.

## Rules implemented

- Standard deck built from 4 colors × ranks 0-9, Skip, Reverse, Draw2 (two of each per color), plus Draw4 and Wild (one of each color slot).
- Match rule: a card is playable if it shares the top card's color, shares its rank, or is a color-less action card (Draw4 / Wild).
- Action cards: Skip and Reverse both give the current player another turn (with only two players they behave the same). Draw2 makes the opponent draw two, Draw4 makes them draw four, Wild and Draw4 let you set the next color.
- "Pull" a card from the deck if you can't or don't want to play: if the pulled card is playable it's added to your hand, otherwise your turn ends.
- Last-card guard: you can't win on an action card. If your final card is an action card, the game deals you an extra card.

The PC opponent is intentionally naive — it plays the first valid card it finds, and when it plays a Wild/Draw4 it just picks the color of its first remaining card.

## Stack

Pure Python 3 standard library (`random`, `time`). No packages to install.

## Run

```bash
python uno.py
```

Then follow the prompts:

- `Hit or Pull? (h/p)` — `h` to play a card, `p` to draw from the deck.
- If you chose `h`, enter the index number shown next to the card you want.
- After a Wild or Draw4, type the new color in caps (`RED`, `GREEN`, `BLUE`, `YELLOW`).
- After a game ends, `y` plays again, anything else quits.

## Example turn

```
Top card is: RED 7
Your cards:
 1.RED 3
 2.BLUE Skip
 3.GREEN 7

Hit or Pull? (h/p): h
Enter index of card: 3
```

Playing `GREEN 7` is legal here because it matches the top card's rank (7), which also switches the active color to green.

## Notes / scope

This is a learning project, not a faithful full-ruleset UNO engine. A few known limitations:

- Skip and Reverse have no distinct effect in a two-player game; both just keep the turn.
- The deck isn't reshuffled when it runs out, so a very long game can hit an empty-deck error.
- Card index and color input aren't validated, so out-of-range indexes or typos can raise errors.

Structure is organized into `Card`, `Deck`, and `Hand` classes with a set of small helper functions (`single_card_check`, `full_hand_check`, `win_check`, `last_card_check`) driving one main game loop.
