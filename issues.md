# Lab 5 — Issues found in `movie_reviews.py`

| Issue | Type | Line(s) | Description | Fix Approach |
| --- | --- | --- | --- | --- |
| Weak MD5 hash (B324) | Security (High) | 46 | `hashlib.md5` is a broken hash; flagged High/High | Switched to `hashlib.sha256` |
| Bind to all interfaces (B104) | Security (Medium) | 4 | `STREAM_HOST = "0.0.0.0"` exposes the service on every network interface | Bind to `127.0.0.1` |
| Hardcoded password (B105) | Security (Low) | 6 | `MODERATOR_PASSWORD` committed in source | Read from `MODERATOR_PASSWORD` environment variable |
| Insecure PRNG (B311) | Security (Low) | 41 | `random.choice` is not cryptographically secure | Use `secrets.choice` |
| Missing whitespace / blank lines / inline comment spacing (E225, E302, E261, E231) | Style | 35, 48, 70, 72 | PEP 8 formatting violations | Added spaces around `=`, second blank line, two spaces before `#`, space after `,` |
| camelCase names (C0103) | Style/Convention | 11, 16, 26, 34, 39, 45, 48, 54 | Functions and args not snake_case | Renamed to `add_movie`, `rate_movie`, `review_text`, etc. |
| Missing docstrings (C0114, C0116) | Documentation | 1, 11-58 | Module and every function undocumented | Added module and function docstrings |
| `global` statement (W0603) | Design | 40 | `pick_featured` mutated module state via `global featured` | Removed global; function now just returns the choice |
| `range(len())` loop (C0200) | Readability | 50 | Index-based iteration | `enumerate(movies, start=1)` |
| Unnecessary `else` after `return` (R1705) | Readability | 28-31 | Redundant branch | Removed `else`, de-indented |
| `main()` runs on import | Design | 75 | Importing the module executes the demo | Added `if __name__ == "__main__":` guard |

## Results
| Tool | Before | After |
| --- | --- | --- |
| Pylint | 5.47/10 | 10.00/10 |
| Bandit | 4 issues (1 High, 1 Medium, 2 Low) | 0 |
| Flake8 | 4 issues | 0 |

Note: review ids and the stream address change by design (SHA-256, 127.0.0.1); the featured movie is random each run.
