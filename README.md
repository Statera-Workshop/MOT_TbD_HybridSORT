# MOT_TbD_HybridSORT

**Hybrid-SORT** - online multi-object tracking by detection on KITTI-MOTS: 25 detectors + the detections of FairMOT.

- Paper: Yang et al., AAAI 2024; official code: `ymzis69/HybridSORT`
- Principle: weak cues: confidence in the Kalman state (TCM), height-modulated IoU, 4-corner directions
- **(best)**: the best of the 10 trackers on that detector; last column = that best HOTA.
- Implementation: `common/mot/trackers.py` (`hybridsort`), re-implemented after the official code, official defaults
  (the class docstring lists every value and every `[Unified]` difference). Causality check: all OK.

### Results (Hybrid-SORT, official defaults, KITTI-MOTS val)

| detector | HOTA | DetA | AssA | MOTA | IDF1 | IDSW | car | pedestrian | tracker ms | pipeline ms | best tracker on this detector |
|---|---|---|---|---|---|---|---|---|---|---|---|
| cascade_rcnn | 0.595 | 0.542 | 0.655 | 0.598 | 0.711 | 55 | 0.681 | 0.509 | 0.71 | 35.6 | 0.625 |
| libra_rcnn | 0.572 | 0.520 | 0.633 | 0.538 | 0.700 | 84 | 0.674 | 0.471 | 0.88 | 27.4 | 0.599 |
| faster_rcnn | 0.557 | 0.505 | 0.618 | 0.553 | 0.690 | 82 | 0.657 | 0.456 | 0.84 | 25.8 | 0.582 |
| dynamic_rcnn | 0.556 | 0.502 | 0.618 | 0.544 | 0.687 | 79 | 0.649 | 0.463 | 0.76 | 25.7 | 0.579 |
| gfl | **0.522** (best) | 0.464 | 0.587 | 0.514 | 0.646 | 39 | 0.618 | 0.425 | 0.60 | 21.4 | 0.522 |
| atss | 0.517 | 0.456 | 0.589 | 0.481 | 0.650 | 69 | 0.606 | 0.429 | 0.71 | 22.4 | 0.527 |
| retinanet | 0.514 | 0.455 | 0.583 | 0.511 | 0.656 | 56 | 0.600 | 0.428 | 0.66 | 21.8 | 0.535 |
| tood | **0.506** (best) | 0.451 | 0.568 | 0.494 | 0.628 | 57 | 0.630 | 0.381 | 0.62 | 25.4 | 0.506 |
| v6 | 0.501 | 0.443 | 0.568 | 0.501 | 0.634 | 44 | 0.626 | 0.375 | 0.64 | 7.2 | 0.509 |
| ppyoloe | 0.481 | 0.425 | 0.548 | 0.460 | 0.596 | 63 | 0.630 | 0.331 | 0.69 | 7.0 | 0.487 |
| fcos | 0.479 | 0.418 | 0.552 | 0.442 | 0.587 | 41 | 0.589 | 0.370 | 0.61 | 22.2 | 0.493 |
| deformable_detr | 0.469 | 0.403 | 0.550 | 0.447 | 0.616 | 47 | 0.572 | 0.367 | 0.64 | 68.9 | 0.482 |
| rtmdet | **0.465** (best) | 0.393 | 0.553 | 0.444 | 0.591 | 30 | 0.610 | 0.320 | 0.58 | 6.8 | 0.465 |
| x | 0.465 | 0.397 | 0.548 | 0.448 | 0.603 | 51 | 0.608 | 0.322 | 0.64 | 6.1 | 0.478 |
| v9 | 0.453 | 0.371 | 0.557 | 0.416 | 0.562 | 31 | 0.603 | 0.304 | 0.54 | 12.5 | 0.460 |
| x2 | **0.452** (best) | 0.381 | 0.538 | 0.420 | 0.577 | 33 | 0.603 | 0.301 | 0.59 | 5.6 | 0.452 |
| v10 | 0.452 | 0.388 | 0.528 | 0.448 | 0.573 | 43 | 0.589 | 0.314 | 0.56 | 8.4 | 0.455 |
| v11 | **0.435** (best) | 0.353 | 0.543 | 0.387 | 0.535 | 33 | 0.602 | 0.269 | 0.56 | 7.0 | 0.435 |
| v8 | 0.433 | 0.366 | 0.518 | 0.415 | 0.538 | 37 | 0.585 | 0.280 | 0.55 | 5.9 | 0.443 |
| v12 | **0.424** (best) | 0.344 | 0.526 | 0.376 | 0.527 | 41 | 0.556 | 0.291 | 0.55 | 9.0 | 0.424 |
| centernet | **0.395** (best) | 0.308 | 0.510 | 0.365 | 0.514 | 17 | 0.495 | 0.295 | 0.45 | 8.0 | 0.395 |
| v26 | **0.390** (best) | 0.322 | 0.482 | 0.376 | 0.505 | 33 | 0.574 | 0.207 | 0.56 | 9.4 | 0.390 |
| fairmot | **0.387** (best) | 0.310 | 0.486 | 0.360 | 0.510 | 19 | 0.517 | 0.258 | 0.50 | 8.7 | 0.387 |
| v13 | 0.363 | 0.306 | 0.445 | 0.343 | 0.445 | 40 | 0.578 | 0.149 | 0.55 | 11.2 | 0.372 |
| v1 | 0.327 | 0.300 | 0.360 | 0.332 | 0.424 | 122 | 0.452 | 0.203 | 0.57 | 6.4 | 0.374 |
| ssd | 0.287 | 0.242 | 0.359 | 0.274 | 0.358 | 24 | 0.534 | 0.039 | 0.44 | 29.7 | 0.288 |

### Score-threshold sensitivity (Hybrid-SORT, HOTA with one common threshold)

Not run for this tracker.

Part of the *Physical AI MOT* comparison of the **Statera Working Group**: 10 trackers x 25 detectors (+ the detections of FairMOT), 3 joint
detection-and-tracking networks and 1 end-to-end tracker under one protocol. The full comparison (Pareto front,
tracker ranking, JDT / E2E against tracking-by-detection) is in `MOT_Detectors_KITTIMOTS` (`RESULTS.md`).

## Protocol (all MOT_* repositories)

- Online / causal only: every method sees the current frame and its own state; checked by re-running prefixes of
  every sequence (the output of frame t must not change when later frames are removed).
- Input 1216 x 384 (KITTI 1242 x 375 letterboxed), detectors trained from scratch on KITTI-MOTS train (12 sequences),
  30 epochs, Adam 1e-4, effective batch 8, seed 777 - the protocol of the *Physical AI Object Detection* series.
- Metrics: HOTA / DetA / AssA (TrackEval classes, car / pedestrian mean), MOTA, IDF1, IDSW.
- Latency: RTX 4070 Laptop GPU, batch 1, fp32, medians over val; pipeline = detector (forward + post-processing) +
  ReID (appearance trackers) + tracker (CPU); image decoding / letterboxing not included.
- Trackers run with their official default parameters; frame-based values given for 30 fps are scaled to 10 fps.
  A sensitivity table with one common score threshold for every tracker is reported separately (chosen on val, so it
  is analysis, not ranking).

## Data: KITTI-MOTS (box level, val = 9 sequences, 2,981 frames)

KITTI tracking images (21 training sequences) with instance / track annotations; boxes = tight boxes of the masks,
classes car and pedestrian, ignore regions (id 10000) neither rewarded nor penalised. The annotations are taken from
the **KITTI-STEP** panoptic maps (same sequences and split, car / person instances merged from KITTI-MOTS; frames,
track counts and pedestrian masks match the KITTI-MOTS paper, car masks differ by 39 of 26,899).

```bash
bash tools/mot/get_kitti_mots.sh            # KITTI tracking images + annotations (KITTI-STEP fallback)
python tools/mot/kittimots_to_voc.py        # VOC-layout copy with tracks + count report
UNIFIED_IMAGE_DATASET=kittimots python tools/mot/count_loader.py     # counts as the loaders read them
```

**Licence of the data and of every trained weight here: KITTI / KITTI-MOTS / KITTI-STEP are CC BY-NC-SA 3.0
(non-commercial).**

## Usage

```bash
pip install -r requirements.txt
pip install "git+https://github.com/JonathonLuiten/TrackEval.git@12c8791b303e0a0b50f753af204249e622d0281a"
# saved detections (+ ReID features) of the 25 detectors: Release of Statera-Workshop/MOT_Detectors_KITTIMOTS
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --trackers hybridsort --causal
python tools/mot/run_tracker.py --source kittimots --dets dets/x_reid.npz --gt-as-pred      # evaluation self-test
python tools/mot/mot_table.py                                                             # tables of all runs
```

`run_tracker.py --trackers` accepts every tracker of the comparison (iou, sort, bytetrack, ocsort, hybridsort, botsort, botsort_reid, deepsort, tracktrack, fairmot), so other
trackers can be run on the same detections. Results of this repository: `results/` (JSON per detector).

## Files

```
common/mot/trackers.py    the trackers of the comparison (default here: hybridsort)
common/mot/core.py        boxes, IoU, assignment, Kalman filters, camera-motion estimation
common/mot/evaluate.py    KITTI-MOTS ground truth and TrackEval metrics
tools/mot/run_tracker.py  run / time / evaluate trackers on saved detections (+ causality check)
tools/mot/*kitti*         data preparation
results/                  evaluation JSON of this repository's tracker(s)
THIRD_PARTY.md            sources and licences
```

## Global Collaboration

Hills Robotics is currently participating in multiple projects in Korea and internationally.

We are actively interested in building relationships with organizations that can complement our technology with global sales networks, distribution channels, system integration capabilities, manufacturing ecosystems, AI infrastructure, robotics technologies, research capabilities, or strategic investment.

Several technology and business collaborations are already underway. Some partners, projects, system architectures, and commercial programs cannot be publicly disclosed because they are subject to confidentiality and business agreements.

We believe that the emerging Physical AI ecosystem cannot be built by a single company.
It requires a global network connecting robotics companies, AI researchers, semiconductor and computing companies, sensor manufacturers, software developers, universities, system integrators, industrial customers, investors, and global distribution partners.

We have now begun our serious exploration of the Physical AI frontier, and we welcome connections with people and organizations who want to build this ecosystem together.

## Research, Contribution, and Donation

The repositories of the Statera Working Group are intended to contribute to the broader technical discussion around Physical AI.

Researchers, engineers, developers, companies, universities, and independent contributors interested in these subjects are welcome to connect with us.

If you would like to collaborate on Physical AI or autonomous robotics, participate in research or technology development, discuss international business cooperation, propose technology or platform integration, contribute technical knowledge, or support this GitHub knowledge initiative through sponsorship or donation, please contact us.

## Contact

**Richard Minsoo Go**
Head of AI, Hills Robotics
Statera Working Group

Personal / Research Contact:
[gominsoo888@gmail.com](mailto:gominsoo888@gmail.com)

Hills Robotics / Business Contact:
[minsoo.go@hillslogis.com](mailto:minsoo.go@hillslogis.com)

Hills Robotics:
https://hillslogis.com/

For inquiries regarding next-generation outdoor autonomous robotic platforms, Physical AI Spider Grid, Intelligence Cabinet, Edge AI, or On-Premise AI architectures that are not yet publicly presented on the company website, please contact us directly.
