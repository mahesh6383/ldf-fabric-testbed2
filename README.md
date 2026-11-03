# LDF Simulation Testbed 2: Data Breach in a Research Data Commons

An interactive, in-browser testbed comparing two paradigms under a cyber-attack. Single file, no build step, no dependencies. Companion to the solar-community testbed.

## Scenario

A research community stores **120 sensitive records on 36 nodes**. An adversary compromises nodes one at a time.

| | Object-centric store | Living Digital Fabric |
|---|---|---|
| Data layout | Whole records on one controller | Each record split into 5 shares on random nodes, any 3 reconstruct |
| Nodes needed to breach | 1 | 3 |
| Monitoring | Only the controller watches | Each node is watched by its honest neighbours |
| Response | Quarantine leaf nodes | Quarantine, then refresh shares |

## Principles modelled

1. **Threshold secret sharing** (Shamir, 1979): fewer than k shares reveal nothing about a record. Used here as an established proxy for LDF's "data as a distributed field configuration".
2. **Peer monitoring** (immune-system analogy): `P(detect) = 1 - (1 - d)^m`, where `m` is the number of honest neighbours and `d` the per-tick detection probability.
3. **Proactive refresh** (Herzberg et al., 1995): after quarantine, shares are re-randomized so stolen shares stop being useful. Records already reconstructed stay exposed.

## Metrics

Records exposed (%), nodes compromised now, nodes needed to breach, first detection time, and cumulative cost.

**Cost (relative units):** `exposed records x record value + response events x response cost x 0.5`. Both weights are editable. They are assumptions, not prices.

**Analytic check:** for `c` randomly compromised nodes, the expected exposed fraction is the hypergeometric tail `P(X >= 3)`, `X ~ Hypergeometric(36, c, 5)`. It is shown next to the simulated value.

## Controls

Scripted experiment, attack on/off, informed or random attacker, attack rate, detection strength, record value, response cost, reset, and CSV export of the run.

## Run locally

Open `index.html` in a browser.

## Deploy on GitHub Pages

1. Upload all files to a new repository, with `index.html` at the root.
2. **Settings, Pages, Deploy from a branch, `main`, `/ (root)`, Save.**
3. The site appears at `https://<username>.github.io/<repository>/`.

## Honest limitations

- Software simulation only.
- The object-centric store is a stylised single store. Real systems add replication and encryption at rest.
- Monitoring and detection probabilities are modelling assumptions.
- One seeded run per setting, with no statistical replicates.
- The fabric is not invulnerable: raise the attack rate and lower detection and it is breached too. The claim is a higher breach threshold and graceful degradation.

## Roadmap

Monte Carlo over seeds, stronger baselines (encrypted replicated stores), an adaptive attacker, DESI-based alerting, and an edge-device testbed.

## References

- Shamir, A. (1979). How to share a secret. *Communications of the ACM*.
- Herzberg, A., Jarecki, S., Krawczyk, H., Yung, M. (1995). Proactive secret sharing. *CRYPTO '95*.

## Author

Mahesh A, Shoolini University. MIT License.
