# Contribution [#3792]: [string expressions parity with pyspark]

**Contribution Number:** #3792
**Student:** Cesar Picazo
**Issue:** https://github.com/Eventual-Inc/Daft/issues/3792
**Status:** Phase II

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

[Notes on setting up your local development environment - challenges you faced, how you solved them]

Have not started on creating solutions for string expressions, but going through the process of choosing which expressions I want to work on. The person that talked about this issue gave a list of string expressions we can choose from. It is not required to do all at once, but for different people to go in and choose to then work on it. So far, only three have been implemented. 

### Next Steps / Brainstorming

-Currently, I am thinking of choosing the regex expressions as I have experience of working with them when working with data. 

-Currently, I am looking at how the other contributions did the string expressions, so I can follow their same format. So far, it seems to me that they have added to expressions and functions folder/file under the Daft folder.



### Steps to Reproduce

1. [Step 1]
2. [Step 2]
3. [Observed result]

### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]

**Match:** [What similar patterns/solutions exist in the codebase?]

**Plan:** [Step-by-step implementation plan]
1. [Modify file X to do Y]
2. [Add function Z]
3. [Update tests]

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

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

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
