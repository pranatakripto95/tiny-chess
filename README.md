# Ember Chess

A 4 KB Python chess engine for make.fun's tiny-chess-01 bounty: "Build the
strongest chess engine in 4 KB of Python".

`main.py` (2,646 bytes, packed with the kit's `makefun compress`) is the whole
engine. Its readable source is `engine.py` (kept beside it in the working
tree; the bundle carries it as the pack source). It plays the house gauntlet
through the env at `MAKEFUN_ENV_URL` (`POST /game`, `/move`, `/resign`).

## How it plays

- 0x88 board, copy-make move generation (perft-verified on the standard
  test positions, including castling, en passant and promotions).
- Negamax alpha-beta with iterative deepening to a fixed node budget
  (100,000 nodes a move — deterministic, no clock, no unseeded randomness),
  a transposition table, and a quiescence search over captures, promotions
  and replies to check.
- Move ordering: transposition-table move first, then captures by MVV-LVA,
  promotions, and killer moves.
- Evaluation: material (pawn 100, knight 320, bishop 330, rook 500, queen
  900) plus piece-square tables and a bishop-pair bonus.

## Local practice score (trial-0, 6 games)

**Elo 1,191** — 2 wins (depth-2, nodes-100k), 1 draw (depth-3), 3 losses
(depth-4, nodes-250k, nodes-500k). Above the 1,154 practice floor.

## License

MIT. See LICENSE.
