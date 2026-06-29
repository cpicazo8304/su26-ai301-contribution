# Contribution [#3792]: [string expressions parity with pyspark]

**Contribution Number:** #3792
**Student:** Cesar Picazo
**Issue:** https://github.com/Eventual-Inc/Daft/issues/3792
**Status:** Phase III

---

## Why I Chose This Issue

This issue caught my attention since it seemed like a great start to my open source journey. It is not too complicated and requires me to provide pre-existing string functions to the Daft repository. It also connects to my strengths which are the AI field, machine learning, data pipelines, and Python. Daft is related to Pandas in terms of helping with data manipulation and pipeline, which I have worked with quite a bit. Since I can now relate Daft to Pandas, it removes an extra roadblock of having to take a lot of extra time trying to understand the library, so I can try fast forward to the brainstorming, testing, and solution stage. 

---

## Understanding the Issue

### Problem Description

Daft has a string expression API, which are operations that can be applied to a column of strings in a DataFrame. However, there are a lot of missing expressions that exist in PySpark. PySpark is Spark's Python API, and it has a very mature, extensive set of string functions built up over years.

### Expected Behavior

We want to be able to use multiple string expressions in a Daft environment. If not, we would have to switch to Pandas or Spark to do the string work. The goal is to just use Daft for all expressions, and keep it simple for users when working with strings. 

### Current Behavior

Currently, users cannot do multiple existing string expressions when using the Daft library, which is known to be fast and efficient, and able to work with large datasets. Since multiple string expressions aren't implemented in Daft, users have to move to Pandas or another library to be able to make changes to column of strings.

### Who is affected?

Users who are working with large datasets, which Daft is known to do well with, will be affected largely. Users who want to migrate from another library into Daft would have to do extra work of adding extra code to deal with the fact that Daft doesn't deal with certain string expressions. The mission of Daft is to be fast, efficient, and user-friendly, so not including string expressions affects that. 

---

## Reproduction Process

### Environment Setup

Getting the library set up was fairly easy:

```bash
pip install -U daft
```

### Steps to Reproduce

1. Install and import Daft library
2. Create a DataFrame with string columns to test avaible and unavailable string functions
3. See which functions work and which don't because of their non-existence

### Reproduction Evidence

- **Commit showing reproduction:** [82194fd](https://github.com/cpicazo8304/su26-ai301-contribution/commit/82194fd7abed3dc251bd21005bc537927e17b35f)
- **My findings:** I discovered that the functions I want to work on, "bit_length" and "octet_length" don't exist in the library. So, I must add them in. 

---

## Solution Approach

### Notes / Analysis

- So, the main computation of a function takes place in Rust. So, the code to calculate the "bit_length" would have to be written in Rust.
- Anything done in Python will be utilizing the Expression class to construct a new Expression that contains the information from the string function.
- I have to touch four places: the Rust implementation (daft-functions-utf8/src/lib.rs), a Python function wrapper (daft/functions/*.py), the Expression class method (daft/expressions/expressions.py), and a test file (tests/expressions/).
    - The split exists because Daft exposes the same operation three ways (expression API, SQL, and method-style like .str.x()) — Rust is the single source of truth, and each Python entry point is just a thin call into the same registered function, so the logic isn't duplicated.

### Proposed Solution

Implement bit_length as a new Rust scalar UDF in daft-functions-utf8 directory, following the pattern of the existing length_bytes implementation, then expose it through Daft's Python expression API and validate correctness with unit and integration tests.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** String expressions such as bit_length are not part of the Daft library. This could make it tough for people to migrate into Daft. For people starting from Daft, it could lead to extra work by having to use other libraries for string columns, which is not efficient. I will be focusing on the bit_length function that counts the length of a string in terms of bits. 

**Match:** There are other string functions like translate, to_binary, etc. There are also numerical functions that are part of Spark but not Daft. In terms of solutions, there are string functions such as length_bytes and a normal length function. They have been implemented in Rust and Python in the repository. With my inexperience in Rust, they could help come up with a way to design the bit_length function. 

**Plan:** [Step-by-step implementation plan]
1. The first step is to create a new file under the directory, src/daft-functions-utf8/src. This is where the rust implementation of bit_length will exist. 
2. Complete the rust implementation for bit_length.
3. Add the new function to the Expression class (daft/expressions/expressions.py) and to the string functions file (daft/functions/str.py)
4. Test the rust and python implementations by adding a test to the test/expressions directory.

**Implement:** [Link to commits](https://github.com/cpicazo8304/Daft)

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** I will evaluate in two ways: the test/expressions directory where I will add more own tests and by having a colab notebook in my local environment that will test the function's use.

---

## Testing Strategy

### Unit Tests

- [ ] **Test case 1 (ASCII strings)**:
Basic single-byte characters where every character is exactly 1 byte = 8 bits. Input "hello" (5 bytes) should return 40. Sanity check that the core byte × 8 math is correct.
- [ ] **Test case (Multi-byte UTF-8 characters)**:
Where bit_length diverges from character length. Input "café" should return 40 (5 bytes × 8), not 32 (4 chars × 8). Confirms bytes are being counted, not characters.
- [ ] **Test case 3 (Null handling)**:
A column with None values mixed in — e.g. ["hello", None, "world"]. The null row should return None, not crash or return 0. Critical since the val? pattern in the implementation is specifically designed to propagate nulls.
- [ ] **Test case 4 (Empty string)**:
Input "" should return 0. Edge case that is easy to accidentally break with off-by-one logic.
- [ ] **Test case 5 (Emoji / 4-byte characters)**:
Input "🚀" should return 32 (4 bytes × 8). Confirms the full UTF-8 byte range works, not just 2-byte characters.

### Integration Tests

- [ ] **Integration scenario 1 (DataFrame pipeline)**:
Create a Daft DataFrame with a string column, call bit_length via the expression API, collect results, and assert output column values match expected. Confirms the full Python → registry → Rust → result round-trip works end to end.
- [ ] **Integration scenario 2 (PySpark parity check)**:
Run the same input through both PySpark's bit_length and Daft's implementation and assert outputs match. Highest-confidence test that the behavior correctly matches the intended PySpark parity goal.

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [1] Progress

[What you built this week, challenges faced, decisions made]
I have gone through Rust documentation and spent a few days learning new terms in Rust. I know the basics of Rust after going through a 3-hour long tutorial video, but still need to figure out niche methods, functions, and interfaces. Currently, I am learning about Traits in Rust because the length_bytes function focuses on that a lot. Once I figure that out, I believe I can write the bit_length function and finish the pull request by next week. 

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Rust Documentation](https://doc.rust-lang.org/stable/std/index.html)
- [Rust Full Course](https://www.youtube.com/watch?v=rQ_J9WH6CGk)
- [GitHub issues or discussions that helped]
