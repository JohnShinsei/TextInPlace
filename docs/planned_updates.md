# Planned Optimization Directions

This fork is maintained for graduation-research experiments based on the original TextInPlace repository. The current plan is to keep the original method reproducible first, then add focused improvements around scene-text filtering, reranking, and evaluation.

## 1. Reproducible Baseline

- Reproduce the original TextInPlace evaluation on Maze-with-Text.
- Record per-floor and all-floor R@1, R@5, and R@10 results.
- Keep the original visual-only and text-reranked results as the main baseline.
- Document environment details, checkpoints, dataset paths, and exact commands.

## 2. TextRerank++

- Improve the current digit-only exact-match text reranking logic.
- Add text normalization for case, punctuation, full-width characters, and common OCR confusions.
- Introduce fuzzy matching for OCR errors such as `401` vs `4O1`.
- Parse structured indoor text patterns such as floors, room numbers, basement labels, and door signs.
- Use OCR recognition confidence when computing text similarity.
- Combine visual retrieval distance and text similarity instead of sorting candidates by text score only.

## 3. LLM-Free Discriminative Text Selection

- Replace online LLM-based filtering with a deterministic local selector.
- Downweight common indoor signs such as `Exit`, `Fire`, `Hydrant`, and `Emergency`.
- Use database frequency or IDF-style weights to reduce the impact of non-distinctive text.
- Keep the optional LLM path for comparison, but avoid requiring API access for standard evaluation.
- Report selector latency and compare it with the LLM-assisted mode.

## 4. Evaluation Cache and Error Analysis

- Cache OCR outputs, recognition scores, database descriptors, and query descriptors.
- Save top-K candidate lists before and after reranking.
- Track which queries are improved, unchanged, or degraded by text reranking.
- Build failure-case summaries for OCR errors, repeated room numbers, floor conflicts, and missing text.
- Add scripts for producing tables that can be used directly in the thesis.

## 5. Strong Visual Baseline

- Add a DINOv2/AnyLoc-style visual descriptor baseline if time allows.
- Compare original TextInPlace descriptors with stronger foundation-model descriptors.
- Test whether text reranking remains useful when the visual baseline is stronger.
- Keep this as an additional validation experiment rather than the first implementation target.

## 6. Expected Research Outcome

The expected outcome is a more robust and reproducible version of TextInPlace for indoor visual place recognition. The main contribution will be a confidence-aware and fuzzy scene-text verification module that improves reranking in repetitive indoor environments while keeping the system lightweight and practical.

