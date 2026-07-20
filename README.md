# Substring Search Algorithm Comparison

Comparison of three substring search algorithms: **Boyer-Moore**, 
**Knuth-Morris-Pratt (KMP)** and **Rabin-Karp** on two text files.

Execution time was measured with the `timeit` module (average of 5 runs) for 
two types of substrings: one present in the text and one absent.

## Methodology

- **Metric:** average execution time in milliseconds (lower = better)
- **Runs per measurement:** 5 (`timeit`)
- **Combined score:** average of the present and absent substring searches

| Dataset | Present substring | Absent substring |
|---|---|---|
| Text 1 | `логарифмічний пошук` | `хроніки амбера` |
| Text 2 | `Постановка завдання` | `зоряне дитя` |

## Text 1 — Results

| Algorithm | Complexity | Found (ms) | Not Found (ms) | Average (ms) |
|---|---|---|---|---|
| Boyer-Moore algorithm **(fastest)** | O(n) / O(n x m) | 0.0508 | 0.1882 | 0.1195 |
| Knuth-Morris-Pratt algorithm | O(n+m) / O(n+m) | 0.1875 | 0.6907 | 0.4391 |
| Rabin-Karp algorithm | O(n+m) / O(n x m) | 0.3755 | 1.2723 | 0.8239 |

**Fastest on this text:** Boyer-Moore algorithm

## Text 2 — Results

| Algorithm | Complexity | Found (ms) | Not Found (ms) | Average (ms) |
|---|---|---|---|---|
| Boyer-Moore algorithm **(fastest)** | O(n) / O(n x m) | 0.0520 | 0.2960 | 0.1740 |
| Knuth-Morris-Pratt algorithm | O(n+m) / O(n+m) | 0.2284 | 0.9419 | 0.5852 |
| Rabin-Karp algorithm | O(n+m) / O(n x m) | 0.4800 | 1.7257 | 1.1028 |

**Fastest on this text:** Boyer-Moore algorithm

## Overall Result

Average time of each algorithm across both texts:

| Algorithm | Average time (ms) |
|---|---|
| Boyer-Moore algorithm **(fastest)** | 0.1468 |
| Knuth-Morris-Pratt algorithm | 0.5121 |
| Rabin-Karp algorithm | 0.9633 |

## Conclusions

1. **The fastest algorithm overall is Boyer-Moore algorithm.** It achieved the best average time on both texts.

2. **Boyer-Moore leads thanks to its shift heuristic.** The shift table lets it skip over sections of text without comparing every character. The longer the pattern and the larger the alphabet, the bigger the shifts - and the faster the search.

3. **KMP is stable but slower than Boyer-Moore.** Its guaranteed O(n+m) complexity is data-independent, but it inspects every character of the text, whereas Boyer-Moore skips them.

4. **Rabin-Karp is the slowest in this test.** Continuously recomputing the hash for every position adds overhead that does not pay off on texts of this size. Its advantage (searching for many patterns at once) is not used here.

5. **An absent substring takes longer to search than a present one** for all algorithms - because searching for a present pattern terminates early on the first match, while an absent one requires scanning the whole text.
