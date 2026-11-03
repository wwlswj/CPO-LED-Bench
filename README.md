# CPO-LED Bench v2.0

CPO-LED Bench is an image-inclusive benchmark for normal-only anomaly
detection in LED-screen animations. It supports temporal-order inspection,
partially observed semantic-slot consistency, natural production anomalies,
and source-isolated evaluation.

The complete image archive is published as a GitHub Release asset:

**[Download CPO-LED-Bench-v2.0-full.zip](https://github.com/wwlswj/CPO-LED-Bench/releases/download/v2.0.0/CPO-LED-Bench-v2.0-full.zip)**

- Archive size: `395,563,944` bytes
- SHA-256: `a462f4c144b4675aaeb7ccdc819066653fd9500615843996f941226c05a3b19d`
- Version: `2.0.0`
- Licence: CC BY 4.0

This repository contains the dataset card, image index, split definitions,
model-ready manifests, configuration, frozen evaluation reports, and
per-file checksums. The image files themselves are distributed through the
Release asset so that the repository remains lightweight.

## Dataset content

| Item | Count |
|---|---:|
| Dynamic difference images | 50,100 |
| Static LED crop images | 20,040 |
| Total image files | 70,140 |
| Spatial base windows | 5,010 |
| Expanded temporal windows | 13,802 |
| Natural production anomalies | 222 |
| Natural test normal windows | 300 |

Dynamic examples contain ten consecutive difference images per base window.
Static examples contain one `600 x 165` grayscale center crop for each LED
subimage. The image index records role, source, sequence, window, frame, label,
and relative path.

## Natural and stress anomalies

The natural test subset contains production-derived device-absent and
static-animation observations. These events were not injected by benchmark
code. Reverse, shuffle, freeze, and frame-drop variants are stored separately
as deterministic temporal stress cases and are identified by the `transform`
field.

## Splits and evaluation

Normal training, normal calibration, validation, and test use source-sequence
isolation. The test split must not be used for early stopping, feature
selection, conformal threshold selection, or fusion-weight selection.

- `splits/normal_train.csv`
- `splits/normal_calibration.csv`
- `splits/validation.csv`
- `splits/test.csv`
- `splits/domain_test.csv`
- `splits/split_summary.csv`

`manifests/` contains the expanded CPO-STCM sample manifest and the natural
test image manifest. `results/` contains frozen reports used by the
manuscript. `checksums.sha256` records SHA-256 values for every file in the
full archive except the checksum file itself.

## UCSD Ped2

The archive includes derived manifests, reimplemented baseline checkpoints,
and frozen evaluation reports for UCSD Ped2. Raw UCSD Ped2 images are not
redistributed and remain subject to the original dataset terms. The source
information is recorded in `external/ucsd_ped2/summary.json`.

## Licence

The owner-provided LED images, annotations, split definitions, manifests, and
derived evidence are released under the Creative Commons Attribution 4.0
International licence. See `LICENSE`. Third-party datasets and software remain
subject to their respective terms.

## Citation

```bibtex
@dataset{wang2026cpcoled,
  author    = {Wang, Wanli and Wei, Xian},
  title     = {{CPO-LED Bench v2.0}},
  year      = {2026},
  version   = {2.0.0},
  publisher = {GitHub},
  url       = {https://github.com/wwlswj/CPO-LED-Bench}
}
```

Machine-readable citation metadata is provided in `CITATION.cff`.

## Contact

Please use the repository issue tracker for dataset questions or reproducible
errors. Author affiliations are listed in `CITATION.cff`.
