# Rehab Motion Assessment

A camera-agnostic rehab motion assessment system, currently being rebuilt around RGB video input and pose estimation.

## Background
This project is a clean rebuild of an earlier rehabilitation motion-tracking prototype that used a 3D camera pipeline. The new version focuses on a modular, reproducible, and demo-friendly architecture while preserving the core ideas of motion feature extraction, sequence comparison, feedback, and session scoring.

## Current status
- Repository initialized
- Project skeleton created
- System spec drafted
- Legacy code inventory in progress
- Migration plan started

## Planned scope for the current version
- RGB video input
- Pose estimation
- Motion feature extraction
- Basic real-time feedback
- Post-session comparison and scoring

## Repository structure
```text
rehab-motion-assessment/
├── README.md
├── .gitignore
├── requirements.txt
├── docs/
├── src/
│   ├── analysis/
│   ├── features/
│   ├── feedback/
│   ├── io/
│   ├── pose/
│   └── visualization/
├── tests/
└── legacy/
```

## Next steps
1. Finalize `docs/system_spec.md`
2. Add `docs/legacy_code_inventory.md`
3. Add `docs/migration_plan.md`
4. Migrate the DTW module into `src/analysis/`
5. Rebuild the feature extraction layer
