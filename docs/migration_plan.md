# Migration Plan

## Old-to-new mapping

| Old component | Old role | New component | Migration decision |
|--------------|----------|---------------|--------------------|
| `output2.txt` loading in `main.py` | Load saved 3D skeleton sequence | `load_pose_sequence()` / MediaPipe landmark loader | Replace |
| Body-joint vector and angle feature extraction | Convert skeleton into motion features | `features/geometry.py` + `features/angles.py` | Keep concept, rewrite cleanly |
| Gaussian smoothing in `main.py` | Reduce frame noise | `features/smoothing.py` | Keep |
| `DTW.py` | Sequence alignment and comparison | `analysis/dtw_compare.py` | Keep almost directly |
| Pose/timing split scoring in `main.py` | Separate motion quality and timing quality | `analysis/scoring.py` | Keep concept, redesign interface |
| Max-difference frame logic | Identify worst pose / timing region | `analysis/error_localization.py` or `feedback/session_summary.py` | Keep concept |
| `save3D.py` | 3D skeleton rendering from saved file | optional visualization utility | Archive / optional reference |
| `CustomerClient/`, `TutorClient/` | Full legacy UI clients | simple OpenCV / Streamlit / lightweight app UI | Reference only |
| `make_sample_session.py` / variant scripts | Generate reference or variant sessions | optional template / test generation tools | Adapt selectively |

## Migration priority

### Priority 1: migrate first
- geometric feature extraction idea from `main.py`
- Gaussian smoothing
- `DTW.py`
- score / max-difference result design

### Priority 2: inspect and selectively reuse
- `make_sample_session.py`
- `make_variant_session.py`
- `view_image.py`

### Priority 3: archive
- `save3D.py`
- `main.spec`
- patch scripts
- old UI-heavy components
