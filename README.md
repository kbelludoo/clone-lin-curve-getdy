# clone-lin-curve-getdy

Experimental LIN clone of Curve Finance 3pool `get_dy` (i64-positive scale:
`SCALE=1e9`, `N=3`, equal rates, explicit fee, 128-bit Newton `(a*b+add)/d`,
fail-closed if the quotient does not fit i64, if `dx=0`, or if `fee > 1e10`).

- **Upstream:** [curvefi/curve-contract](https://github.com/curvefi/curve-contract) `contracts/pools/3pool/StableSwap3Pool.vy` commit `bae23a2fc9a0302d174ea1ffce8219a44a92149c`. Curve.Fi publishes that tree as informational-only (no reproduction license); this repository does **not** vendor the Vyper source. Hashes only: sha256 `03e0bf29ae2fe945a3629b8085062da8f9d9d25957e86001dfc3df68c895f9dc`, git blob `04d170189a1b5ddfecfc0af9ea3fe23eb0840423`.
- **LIN kernel:** [`src/lin_curve_getdy.lin`](src/lin_curve_getdy.lin) (sha256 `b585ef4d3c784661debd7798115f59fd846cb924be946bb08dc4ba9e032cc041`, identical to lin-open)
- **C11 oracle copy:** [`test/oracles/curve_getdy_c11.c`](test/oracles/curve_getdy_c11.c)
- **Proofs (lin-open only):** [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/curve_getdy/` and `make curve-getdy-proof`
- **Class:** EXPERIMENTAL. Not Ethereum Curve 3pool uint256. Not `RATES` 1e30 / `PRECISION` / `exchange`. Not a production pool replacement.

Named goldens (i64-positive, equal `1e9` balances, `dx=1e8`): no-fee **99900110**; 0.04% fee (`4e6`) **99860150** at `A=100` and **99954955** at `A=2000`; omit-minus-1 **99900111**; `dx=0` fail-closed **0**; fee overflow fail-closed **0**. Naive i64 `D^2` wraps to **-8838116264523025375**.
