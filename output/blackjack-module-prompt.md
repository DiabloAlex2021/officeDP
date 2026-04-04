# Blackjack Module Prompt

Derived from the implemented blackjack wall and console in `/Users/yifandu/Desktop/3dw_Office/character.html` and the proof renders in `/Users/yifandu/Desktop/3dw_Office/output/web-game-blackjack-result-ui/result-ui-board.png`, `/Users/yifandu/Desktop/3dw_Office/output/web-game-blackjack-console-bottom/console-bottom-clean.png`, and `/Users/yifandu/Desktop/3dw_Office/output/web-game-blackjack-wall-proof/board-deal-proof-clear.png`.

## Full Prompt

```text
Generate a complete playable blackjack interaction module from a stylized low-poly office game, isolated with no surrounding room or character, straight-on centered composition. This module has two linked parts: a wall-mounted blackjack board above and a floating blackjack control console below.

Wall board:
A wide horizontal wall sign, about 4.8 by 2.72 in proportion, matte charcoal back frame, thin gold trim, slight top marquee bar, faint gold underglow along the bottom edge. The board face is a 1024x640 style casino display: deep emerald felt gradient background from dark green to near-black, subtle vignette, double rounded border, outer border thick gold, inner border faint pale gold.

Top-left board header:
Large warm gold serif title: "BLACKJACK WALL".
Below it, two lines of small mint-green monospace rules:
"6 DECK · S17 · BJ 3:2 · DOUBLE ANY 2 · SPLIT TO 4"
"NO INSURANCE · SPLIT ACES DRAW ONE"

Top-right information stack:
Three rounded dark glass boxes with thin gold borders and soft inset glow.
Labels in mint monospace, values in bright white monospace.
Box 1: "BANKER BANK" with value {{banker_bank}}
Box 2: "PLAYER CREDITS" with value {{player_credits}}
Box 3: "BET · SHOE" with value {{bet}} · {{shoe_remaining}}

Dealer zone:
Upper-left middle area with mint monospace label like "DEALER {{dealer_total_label}}".
If no cards are dealt, show a muted rounded placeholder plate that says "DEAL TO START".
If cards are present, show overlapping vertical casino cards.
Card style: cream paper, rounded corners, beige border, rank in top-left and bottom-right, suit abbreviations "SP HE DI CL", black suits in dark charcoal, red suits in muted casino red.
Hidden hole card style: dark navy-blue card face, diagonal stripe pattern, gold outline, centered label "BANK".

Player hand play area:
Lower half of the board contains one to four evenly spaced rounded hand panels.
Each hand panel is a dark translucent rectangle with gold border.
Active hand panel is brighter, greener, and outlined with stronger gold.
Each hand panel title is mint monospace:
"HAND {{index}} · BET {{hand_bet}} · {{hand_total}}"
Each panel contains overlapping cards centered horizontally.
Each panel has a lower-left status or outcome label:
"ACTIVE", "WAIT", "STAND", "WIN +100", "LOSE -100", "PUSH", "BLACKJACK +150"
Outcome colors: green for player win or blackjack, muted red for banker win or lose state, pale gray for push, mint-green for active.

Result banner:
When a round is over, place a centered rounded banner above the player hand panels.
Banner style changes by result tone:
neutral = gold text on dark green-black
player win = green text and green outline
banker win = red text and red outline
push = pale gray text and silver-gray outline
Headline examples:
"PLAYER BLACKJACK +150"
"PLAYER WINS"
"BANKER WINS"
"ROUND PUSH"
Give the result text a terminal type-on feel, as if it was typed out character by character.

Bottom board ticker:
A slim full-width rounded strip along the bottom of the board with small monospace copy.
Example texts:
"Raise or lower the wager, then deal against the banker."
"Hand 1 · hit, stand, double, or split."
"Dealer 20. H1 WIN · H2 LOSE"

Blackjack console below the board:
A bottom-centered floating control panel titled "BLACKJACK CONSOLE".
Wide rounded rectangle, near-black glass surface, subtle green tint, thin gold border, soft drop shadow, premium casino terminal styling.
Desktop width: about 620px max, centered.
Mobile version: nearly full width with reduced margins.

Console title:
Centered, small gold uppercase letters with wide tracking:
"BLACKJACK CONSOLE"

Console readout card:
Large rounded dark gradient inner card near the top of the console.
Small muted green monospace label:
"TABLE READOUT", "LAST RESULT", or "ROUND RESULT"
Large bold headline under it:
"BETTING"
"HAND 1 · 16"
"PLAYER BLACKJACK +150"
"BANKER WINS"
Smaller readout line below:
"PLAYER 5,000 · BANK 1,000,000 · BET 100 · SHOE 312"
If showing round-over state, the border and headline color follow the same tone logic as the board result banner:
neutral gold, player green, banker red, push gray.

Console helper text:
Centered small muted mint line between the readout card and the buttons.
Examples:
"Set the wager, then deal against the banker."
"Choose the live hand action below and play against the banker."
"Round closed. Review the typed result above, then deal the next hand or change the wager."

Console action buttons:
Neat grid of rounded pill buttons.
Desktop: 4 columns.
Mobile: 2 columns.
Buttons use dark navy-black fill with faint blue tint, thin blue-gold border, monospace labels, compact uppercase text.
Pressed state: brighter blue.
Active state: green highlight.
Disabled state: faded and low-opacity.
Betting and round-over buttons:
"BET -100"
"BET +100"
"BET +500"
"DEAL HAND" or "NEXT HAND"
Player-turn buttons:
"HIT"
"STAND"
"DOUBLE"
"SPLIT"

Gameplay cues encoded in the UI:
minimum bet 100
bet step 100
large bet step 500
6-deck shoe
dealer stands on soft 17
blackjack pays 3:2
double on any two cards
split up to 4 hands
result history can surface as "LAST RESULT"

Overall art direction:
Clean low-poly game UI, flat-shaded but premium, casino signage mixed with retro terminal interface, high legibility, crisp typography, exact spacing, symmetrical layout, dark green / gold / mint palette, no decorative clutter outside the blackjack unit.

Exclude:
characters, office floor, wheelchair rack, windows, style menu, d-pad, movement controls, extra HUD, poker chips, roulette, slot machines, realistic casino table, cinematic perspective clutter
```

## State Presets

- `Betting open`: banker `1,000,000`, player `5,000`, bet `100`, shoe `312`, no dealer cards, no player hands, board ticker `Raise or lower the wager, then deal against the banker.`, console label `TABLE READOUT`, headline `BETTING`, buttons `BET -100`, `BET +100`, `BET +500`, `DEAL HAND`.
- `Player turn, split-ready`: dealer shows `6C` plus one hidden `BANK` card, player hand `8H 8S`, hand label `HAND 1 · BET 100 · 16`, ticker `Hand 1 · hit, stand, double, or split.`, console headline `HAND 1 · 16`, buttons `HIT`, `STAND`, `DOUBLE`, `SPLIT`.
- `Player turn, after split`: dealer shows `6C` plus hidden `BANK`, hand 1 is active with `8H 3H`, hand 2 waits with `8S KS`, board supports two separate hand panels, ticker `Split made. Play hand 1.`, buttons `HIT`, `STAND`, `DOUBLE`, `SPLIT` disabled.
- `Round over, blackjack`: dealer `6C 10D`, player `AH KH`, result banner and console headline `PLAYER BLACKJACK +150`, readout `PLAYER 5,150 · BANK 999,850 · BET 100 · SHOE 312`, label `ROUND RESULT`.
- `Round over, split resolved`: dealer total `20`, two hand panels, hand 1 `WIN +100`, hand 2 `LOSE -100`, ticker `Dealer 20. H1 WIN · H2 LOSE`, console helper `Round closed. Review the typed result above, then deal the next hand or change the wager.`
- `Round over, double resolved`: single hand with doubled bet `200`, player total `21`, dealer total `17`, result reads `H1 WIN`, player bankroll `5,200`, bank bankroll `999,800`.
- `Betting with history loaded`: console label changes to `LAST RESULT` while staying in betting mode, then the standard wager buttons remain visible for the next round.

## Negative Prompt

```text
person, humanoid, office interior, wooden floor, wheelchair, right-side menu, d-pad, mobile controls, game HUD, camera orbit view, cluttered background, casino table, chips, photorealism, ornate realism, blurry text, distorted cards
```
