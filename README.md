# DAO Sybil resilience — equal-split phase boundaries

## Run locally in 2 commands

From a cloned checkout with Python 3.9+:

```sh
python3 -m pip install -r requirements.txt
MPLBACKEND=Agg python3 run_sybil_pipeline.py
```

This writes `empirical_reversal_thresholds_k_boundary_phase_space.png` using four hard-coded summary pairs. It does not fetch or reconstruct raw ballots.

## What the model asks

How much extra square-root voting weight can one fixed token budget obtain by splitting equally across identities? With unsplit weight W and k wallets, total weight is sqrt(k) W. Against an opposing lead G that already includes the attacker's original losing-side vote, strict reversal requires `(sqrt(k) - 1) W > G`. The minimum integer split is `floor((1 + G/W)^2) + 1`.

The published summary pairs imply strict thresholds of **4, 25, 230 and 894 wallets**. Equality is a tie, not a strict reversal. The [boundary checks](https://github.com/thetarocks/catalyst-lab/blob/main/tests/test_benchmark_evidence.py) verify both the stated integer and the integer immediately below it.

## Data, scope and architecture

`DATA` in `run_sybil_pipeline.py` supplies W/G summary pairs → NumPy generates boundary lines → pandas organizes labels → Matplotlib renders the phase plot. Complete raw ballots and a ballot-level derivation of those four summary pairs are not committed, so their empirical provenance cannot be independently reconstructed from this repository alone.

This is an analytical follow-on to the [Arbitrum governance preprint on SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=7103878), which studies fixed-vote reweighting. The plot is not a replication of that paper and is not evidence of an observed attack. It omits identity costs, eligibility requirements, delegation and voter responses.

Try the [interactive preview](https://yourcatalyst.in/#research), read the [technical companion](https://yourcatalyst.in/artifacts/sybil-technical-note.pdf), or inspect the [versioned boundary evidence](https://yourcatalyst.in/evidence/sybil-boundaries.json).

The [collection pipeline](https://github.com/thetarocks/arbitrum-quadratic-voting-simulation) is separate. The [main portfolio](https://github.com/thetarocks/catalyst-lab) holds the browser implementation, test suite and project-hosted technical notes. Documentation and portfolio work use coding assistance; no delegate endorsement or observed exploitation is claimed.
