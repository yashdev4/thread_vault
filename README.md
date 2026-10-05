# ThreadVault Archive

> **Note:** This repository is an automated, private archive of conversations managed by [ThreadVault](https://github.com/eoxs/threadvault).

## Automated Maintenance & Guidelines

- **Do Not Edit Directly:** This repository is maintained by an automated export process. If files are edited directly on GitHub, ThreadVault detects the modification as a conflict and will skip updating those files to preserve your manual edits.
- **Privacy Notice:** This repository is configured to be strictly private. ThreadVault's private-repo guard refuses export if the repository is ever made public.
- **Deletion Semantics:** When a thread is deleted in ThreadVault, its files are deleted from the repository in the subsequent export commit. Prior commits in git history continue to contain the archived text unless explicitly purged using the squash command:
  ```bash
  python -m thread_save.cli.github squash
  ```

## Repository Structure

```
.
├── README.md              # Repository documentation and maintenance rules
├── index/
│   ├── threads.json       # Machine index mapping thread_id -> metadata and page paths
│   └── YYYY-MM.md         # Human-readable monthly indexes with relative links
└── YYYY/
    └── MM/
        └── {timestamp}_{account}_{short}_{slug}_p{NN}.md  # Canonical conversation pages
```
