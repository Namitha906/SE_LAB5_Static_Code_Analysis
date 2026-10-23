# Lab 5: Static Code Analysis — Issue Documentation

## Objective

To improve the quality, security, readability, and maintainability of the `music_catalog.py` program using Pylint, Bandit, and Flake8.

## Static Analysis Results

| Tool | Before Fixes | After Fixes |
|---|---|---|
| Pylint | 4.57/10 | 10.00/10 |
| Bandit | 4 findings: 2 Low, 2 Medium | 0 issues |
| Flake8 | 7 violations | 0 violations |

## Issues Identified and Fixes Applied

| Issue | Type | Original Line(s) | Description | Fix Approach |
|---|---|---|---|---|
| SQL injection risk (B608) | Security | 10 | SQL query was constructed using string formatting, which can allow malicious input to alter the query. | Replaced string formatting with parameterized SQL queries using `?` placeholders. |
| Unsafe pickle import (B403) | Security | 1 | The `pickle` module can introduce security risks when used with untrusted data. | Replaced pickle serialization with JSON serialization. |
| Unsafe deserialization (B301) | Security | 33 | `pickle.loads()` can execute malicious code when processing untrusted serialized data. | Replaced `pickle.loads()` with JSON deserialization. |
| Inappropriate random generator warning (B311) | Security finding | 17 | The standard `random` generator is not intended for cryptographic purposes. | Replaced `random.choice()` with `secrets.choice()`. |
| Mutable default argument (W0102) | Bug prevention | 9 | The default argument `playlist=[]` could retain changes across function calls. | Changed the default to `None` and initialized a new list inside the function when needed. |
| Missing module docstring (C0114) | Maintainability | 1 | The module lacked a description of its purpose. | Added a module-level docstring. |
| Missing function docstrings (C0116) | Maintainability | 9, 15, 20, 28, 32, 36, 43 | Functions lacked documentation describing their purpose. | Added descriptive docstrings to the functions. |
| Invalid function names (C0103) | Naming convention | 9, 15, 28, 32, 36 | Names such as `addSong`, `shufflePick`, and `totalPlays` did not follow snake_case conventions. | Renamed functions using snake_case, such as `add_song`, `shuffle_pick`, and `total_plays`. |
| SQL line too long (C0301, E501) | Style | 10 | The SQL statement exceeded the configured line-length limits. | Split the statement across multiple lines. |
| Bare exception (W0702, E722) | Error handling | 39 | A bare `except:` caught all exception types and could hide unexpected errors. | Replaced it with a specific `sqlite3.Error` handler. |
| Unnecessary else after return (R1705) | Readability | 22 | An `else` branch was unnecessary after a return statement. | Removed the unnecessary `else` and returned directly. |
| Ambiguous variable name (E741) | Readability | 47 | The variable `l` was difficult to distinguish from the number `1`. | Renamed it to `loaded_playlist`. |
| Multiple statements on one line (C0321, E701) | Style | 48 | Multiple statements on a single line reduced readability. | Moved statements onto separate lines. |
| Long lines (E501) | Style | 6, 21, 49 | Several lines exceeded Flake8's 79-character limit. | Reformatted long statements across multiple lines. |
| Empty song catalog handling | Robustness | 17 | Selecting a random ID from an empty list could raise an exception. | Added an empty-list check and returned `None` when no songs exist. |

*Note: Line numbers refer to the original version of `music_catalog.py`. Some findings overlap across tools.*

## Conclusion

Static analysis helped identify security risks, coding-standard violations, and maintainability issues. After applying the fixes, Pylint improved from 4.57/10 to 10.00/10, Bandit reported no issues, and Flake8 reported no violations.