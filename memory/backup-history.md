# Brain Backup History

| Timestamp (IST) | Files | Commit | Push status |
|---|---|---|---|
| 2026-06-15 23:00 | 13 | 37f9f5a | Pending — first push from Mac Mini (sandbox can't auth) |
| 2026-06-15 23:08 | 6 | BLOCKED — staged, not committed | Blocked (sandbox). `git commit` fails: stuck `.git/index.lock` is unremovable (mount = "Operation not permitted" on `.git/`). `git push` fails: SSH `Host key verification failed` (no creds). 6 files staged (BACKLOG, BRAIN, WATCH, decisions/2026-06-15, excluded-topics, professional-input-history). Resolution: run native on Mac Mini — `rm -f brain/.git/index.lock && git -C brain commit && git push`. Self-heals with Tue 06-16 authenticated run. |
| 2026-06-17 23:08 | 23 | BLOCKED — not committed | Same blockers persist. `.git/index.lock` still present (created 06-15 17:39, unremovable: "Operation not permitted"). `git push` → `Permission denied (publickey)`. 23 files pending (11 tracked-mod, 12 untracked incl. GEO/conversion maps, decisions/2026-06-17, experiments/, verifier-log, needs-human-review/). Last successful commit: `5c06290` (06-15). **DAY 3 of blocked backup → ESCALATED to Slack.** Manual fix on Mac Mini: `rm -f brain/.git/index.lock && git -C brain add -A && git -C brain commit -m "manual unblock" && git -C brain push origin main`. |
