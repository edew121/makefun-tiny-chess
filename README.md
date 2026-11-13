# Tiny Chess Engine (4 KB)

A compact Python chess engine for the make.fun bounty
"Build the strongest chess engine in 4 KB of Python" (tiny-chess-01).

## Engine

- 0x88 board, alpha-beta search with iterative deepening
- Fixed node budget: 120,000 nodes per move (deterministic, no clock)
- Null-move pruning (R=2) and delta pruning in quiescence;
  quiescence search (captures and check evasions), transposition table,
  MVV-LVA move ordering
- Evaluation: material + piece-square tables (tapered king table,
  incl. rook on 7th rank / central back rank), bishop pair,
  with incremental Zobrist hashing and incremental evaluation
- Transposition-table and repetition handling; draws by repetition
  and fifty moves are recognised in search
- Python 3 standard library only; no model calls, no randomness

`main.py` is the engine packed as an LZMA payload with a tiny unpacker
(the same packing approach the house sunfish baseline uses), 4,092 bytes.

## Practice results (local, official kit env + scorer)

- Trial 0: Elo 1396 (4W 0D 4L)
- Trial 1: Elo 1464 (4W 1D 3L)
- Trial 2: Elo 1396 (3W 2D 3L) with the final packed entry
  (mean of the three practice trials: 1418.7; lead vs sunfish
  +70 / +68 / +143, 90% t-interval of the lead above 0)

Practice floor is 1154; the house sunfish 4 KB baseline averages 1325
over the three practice instances.

## License

MIT — see LICENSE.
