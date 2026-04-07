[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/T6sJM4w6)
# Week 5 — Midnight Mail Train

## Summary
This assignment implements a doubly linked list (`MidnightMailDLL`) to manage train cars,
supporting append, detach, and reverse traversal operations. It also includes a regex-based
ticket code validator and two recursive functions — one to count matching labels in a list,
and one to strip spaces from a string. Iterative stretch versions of both recursive functions
are also provided.

## Approach
- **Problem 1 — MidnightMailDLL:** Each method handles three cases: empty list, single node,
  and multiple nodes. `append_car` links the new node bidirectionally at the tail.
  `detach_last_car` moves the tail pointer back and severs the forward link.
  `to_reverse_list` walks from tail to head collecting IDs.
- **Problem 2 — is_valid_ticket_code:** Used `re.fullmatch` with the pattern `MM-.+\d{4}`
  so the entire string must match — prefix `MM-`, at least one character, ending in exactly 4 digits.
- **Problem 3 — count_priority_labels:** Recursive slice approach — check `labels[0]` against
  the target, add 1 or 0, then recurse on `labels[1:]`. Base case is an empty list returning 0.
- **Problem 4 — clean_radio_message:** Same recursive slice pattern — if `message[0]` is a space,
  contribute `""` to the result; otherwise keep it. Recurse on `message[1:]`. Base case is an empty string.

## Complexity
| Function | Time | Space | Reason |
|---|---|---|---|
| `append_car` | O(1) | O(1) | Direct tail pointer access, no traversal |
| `detach_last_car` | O(1) | O(1) | Direct tail pointer access, no traversal |
| `to_reverse_list` | O(n) | O(n) | Visits every node once; output list grows with n |
| `is_valid_ticket_code` | O(n) | O(1) | Regex scans the string once; n = length of code |
| `count_priority_labels` | O(n) | O(n) | One recursive call per element; call stack depth is n |
| `clean_radio_message` | O(n) | O(n) | One recursive call per character; call stack depth is n |

## Edge-case checklist
- [x] empty train — `detach_last_car` returns `None`; `to_reverse_list` returns `[]`
- [x] one train car — `detach_last_car` sets both `head` and `tail` to `None`
- [x] invalid ticket code — `is_valid_ticket_code` returns `False` for missing prefix, wrong digit count, or extra characters
- [x] empty label list — `count_priority_labels` hits the base case and returns `0`
- [x] empty message — `clean_radio_message` hits the base case and returns `""`
- [x] one-character or all-space message — handled correctly by the character-level recursion

## Assistance & Sources
- AI used? Y
- What it helped with: Code implementation and README writeup
- Other sources used: Course materials