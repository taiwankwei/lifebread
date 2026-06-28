---
name: manage-bible-verses
description: Manage and update the Bible verses list in the G12 fellowship webpage (index.html). Use when the user asks to add, remove, or modify scripture references, or queries a verse's presence in the project.
---

# Manage Bible Verses Skill

This skill guides the agent in searching, updating, and maintaining the Bible verses list (`BIBLE_VERSES` array) within the G12 Fellowship webpage (`index.html`).

## Trigger Conditions

Use this skill when:
- The user provides a bible verse or reference and asks to add it to the webpage.
- The user queries if a specific verse exists in the project.
- The user requests modifications or updates to the existing Bible verses collection.

## Procedures

### 1. Search for Existing Verses
Before adding any new verse, check if it already exists in the `BIBLE_VERSES` array in [index.html](file:///c:/Users/User/中三區G12/index.html):
- Use a case-insensitive search for keywords, book name, or chapter/verse references (e.g., searching for `約翰福音` or `3:16`).

### 2. Locate the BIBLE_VERSES Array
The Bible verses are stored in a JavaScript array named `BIBLE_VERSES` inside [index.html](file:///c:/Users/User/中三區G12/index.html):
```javascript
const BIBLE_VERSES = [
  ['約翰福音 3:16','神愛世人，甚至將他的獨生子賜給他們，叫一切信他的，不至滅亡，反得永生。'],
  ...
];
```

### 3. Add or Modify Verses
When adding a new verse, ensure it matches the standard format:
```javascript
['書名 章:節', '經文內容。'],
```
*Note: Make sure to include proper punctuation and commas between elements.*

### 4. Verify Syntax
- Ensure that the syntax of the JavaScript array is not broken.
- Ensure every element is correctly comma-separated and closed with brackets.

## Reference Files
- [index.html](file:///c:/Users/User/中三區G12/index.html)
