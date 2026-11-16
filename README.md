# tiny-chess-01 entry

A chess engine in 4 KB of Python: `main.py` is the whole engine
(4,044 bytes, an lzma-packed payload with its unpacker, as the rules
allow). It plays the make.fun gauntlet through the env at
MAKEFUN_ENV_URL and exits when every game is over.

## How it plays

- Negamax with alpha-beta (PVS), a transposition table, check
  extensions, null-move pruning and a captures-only quiescence
  search. Move legality is pin-aware, which keeps the search fast.
- Fixed budget of 50,000 nodes per move with iterative deepening:
  no clock, no unseeded randomness, so replays match move for move.
- Evaluation is material plus piece-square tables (king table swaps
  to its endgame form once no queens remain), maintained
  incrementally as moves are made.
- Root moves that would repeat a position from the game's own
  history are scored as the draw they would become.

Python 3.13, standard library only. 0BSD, see LICENSE.
