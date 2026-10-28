# TRL assessment (evidence-based)

**Level reached: TRL 4 for the individual components, on SYNTHETIC data only.** TRL 5 is not claimed.

`pytest` (CI on every push) runs 6 tests:

| Component | Module | Validated against |
|---|---|---|
| Synthetic two-unit schedule (19 grades, first-order transitions) | `simulator.py` | grade count, lagged response after a change |
| MFI / density virtual sensor (ridge, log scale) | `virtual_sensor.py` | hold-out **grades** at near steady state: MFI MAPE under 10 % (SRS NFR-PER-02), density MAPE under 1 % |
| Transition dynamics: time constant, time to spec band, off-spec minutes, waste mass | `transition.py` | exact recovery of a known time constant, analytic vs simulated time to band, waste arithmetic |
| Transient catalyst activity (first-order recovery) | `transition.py` | monotone recovery |

## Not done (and why)
- Everything is **synthetic and illustrative** (grade setpoints, lag, noise). The MAPE above says the code is correct, not that the virtual sensor works on the plant.
- **No DCS/LIMS data**, so accuracy during real transitions is unknown (TRL 5 needs real transitions).
- The portfolio-level sequencing of the 19 grades (the product's core claim, SRS section 1) is **intentionally not implemented** in this public repository, pending the patent attorney's review. The optimal per-pair transition path (FR-SEQ-02) is also not implemented.
- Latency (NFR-PER-01) and availability are not measured.

## Next steps toward TRL 5
1. Historian + lab data for both units and a log of real changeovers (time and off-spec mass) under a data-sharing agreement.
2. Fit/validate the sensor on real data with grade-held-out splits; compare the time constants with real transitions.
3. Ingestion service and latency measurement.
