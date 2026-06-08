# Contribution [#2730]: [Issue: geemap cartoee.get_map() ignores region parameter and results in low resolution when using ax.set_extent()]

**Contribution Number:** #2730
**Student:** Cesar Picazo
**Issue:** https://github.com/gee-community/geemap/issues/2730
**Status:** Phase I

---

## Why I Chose This Issue

This issue caught my attention because it sits at the intersection of two areas I have been actively developing skills in: Python-based geospatial analysis and data visualization. I have been building GIS skills through ArcGIS Pro and working on a data science project analyzing traffic data in Austin, Texas, so the idea of working with satellite imagery and geographic datasets through Python feels like a natural next step. The cartoee bug is intriguing because it has a clear, well-diagnosed proble: a region parameter being silently ignored. This makes it approachable as a first open source contribution while still being a meaningful fix that affects real research workflows.

---

## Understanding the Issue

### Problem Description

The cartoee.get_map() function in geemap has a region parameter that is supposed to limit the rendered map to a specific geographic area. However, the parameter is silently ignored and the function renders the entire globe instead. As a workaround, users can manually crop the map afterward using ax.set_extent(), but this produces a low resolution result because the full global image was already downloaded and rendered at low resolution before being cropped down.

### Expected Behavior

When a user passes a bounding box to the region parameter, the function should fetch and render only that geographic area from Google Earth Engine at full resolution. The output image should be sharp and detailed, matching the resolution expected for that region size.

### Current Behavior

The region parameter is ignored entirely, causing the function to default to a global extent regardless of what the user specifies. When users try to work around this by cropping the plot manually with ax.set_extent(), the image appears pixelated because it was originally rendered at global scale and then scaled down to a small region.

### Affected Components

The get_map() function in geemap/cartoee.py, where the region parameter is not being correctly passed to the underlying Earth Engine image fetch call (likely getThumbURL or equivalent export logic)

---

## Reproduction Process

### Environment Setup

[Notes on setting up your local development environment - challenges you faced, how you solved them]

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
