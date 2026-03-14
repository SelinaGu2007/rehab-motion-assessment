# Legacy Code Inventory

## Top-level directories

| Path | Type | Purpose | Decision | Notes |
|------|------|---------|----------|-------|
| `CustomerClient/` | UI client | User-facing interface | Reference | Useful for understanding original user flow, but not a priority for direct migration |
| `TutorClient/` | UI client | Tutor / therapist / instructor-side interface | Reference | Good for product context, not needed in MVP |
| `test_exe/` | Core analysis | Main analysis pipeline and DTW workflow | Adapt | Most important legacy directory to inspect and mine |
| `simple_3d_viewer/` | Visualization | 3D visualization of skeleton or motion | Reference / Archive | Lower priority for RGB-first rebuild |
| `show_videos/` | Demo assets | Demo videos / exported visual outputs | Archive / Reference | Keep for proof of prior prototype and demo material |
| `tools/` | Utilities | Session generation / patch scripts | Inspect further | Contains potentially reusable data-generation ideas |
| `data/` | Data | Legacy data storage | Archive | Currently empty, no reusable content |
| `docs/` | Documentation | Project notes / design docs | Keep as reference | Useful for reconstruction and storytelling |
| `README.md` | Documentation | Project overview | Keep as reference | Helps recover old project framing |
| `requirements.txt` | Config | Python dependencies | Adapt | Useful for understanding old environment |
| `score_result.json` | Output artifact | Example scoring result | Keep as reference | Helpful for understanding expected output structure |
| `background.jpg` | Asset | UI asset | Archive | Non-core asset |
| `.gitignore` | Config | Git ignore rules | Keep | Can be reused or adapted |
| `.git/` | Repo metadata | Git history | Keep privately | Not part of new architecture, but useful for version history |

## `test_exe/`

| Path | Type | Purpose | Decision | Notes |
|------|------|---------|----------|-------|
| `test_exe/main.py` | Monolithic pipeline | Main motion-analysis workflow | Reference + migration blueprint | Defines old end-to-end pipeline, but should be split rather than reused directly |
| `test_exe/DTW.py` | Algorithm module | DTW distance, path, and error-window logic | Keep (near-direct migration) | Hardware-agnostic and highly reusable |
| `test_exe/save3D.py` | Visualization utility | Render 3D skeleton frames from saved joint text | Reference / partial Archive | Useful for understanding old skeleton topology and format, not core for new system |
| `test_exe/view_image.py` | Visualization | Image/result display | Reference / Adapt | Potential source of visualization ideas |
| `test_exe/dtw_try.py` | Experiment script | DTW testing / experimentation | Reference | Helps understand how DTW was used |
| `test_exe/main.py.bak` | Backup | Older main pipeline version | Reference | Only for comparison if needed |
| `test_exe/main.spec` | Build config | Packaging spec | Archive | Not needed during rebuild |
| `test_exe/__pycache__/` | Cache | Python bytecode cache | Drop | Ignore |

## `tools/`

| Path | Type | Purpose | Decision | Notes |
|------|------|---------|----------|-------|
| `tools/make_sample_session.py` | Data generation | Build sample/reference sessions | Adapt | Potentially useful for generating standard templates |
| `tools/make_variant_session.py` | Data generation | Build motion variants | Adapt | Useful idea for incorrect-form or perturbed motion testing |
| `tools/make_variant_session_fixed.py` | Data generation | Revised variant generator | Reference / Adapt | Possibly a better version of variant generation |
| `tools/patch_main_edge_skip.py` | Patch script | Temporary patch for main pipeline | Reference | Indicates old system accumulated local fixes |
| `tools/patch_showImage.py` | Patch script | Temporary visualization patch | Archive / Reference | Keep only as historical context |
| `tools/patch_view_image.py` | Patch script | Temporary visualization patch | Archive / Reference | Keep only as historical context |

## Key findings from legacy code

The old system is fundamentally a pipeline that:

1. reads saved skeleton sequences from `output2.txt`
2. converts body joints into geometric angle-based motion features
3. applies Gaussian smoothing to reduce frame-level noise
4. uses DTW to align the user motion with a reference motion
5. computes pose and timing related scores
6. exports score and max-difference results for interpretation
