# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file Korean shopping list web app. No build system, no dependencies, no package manager.

## Running the App

Open `shopping-list.html` directly in a browser. No server required.

For a quick local server if needed:
```
npx serve .
# or
python -m http.server
```

## Architecture

Everything lives in `shopping-list.html` — HTML structure, CSS styles, and JavaScript logic are all in one file.

**State management:** A single `items` array (objects with `text` and `checked` fields) is the source of truth. It is persisted to `localStorage` under the key `shoppingList` on every mutation.

**Render pattern:** Mutations always follow the same sequence: update `items` → call `save()` → call `render()`. `render()` does a full DOM rebuild of `<ul id="list">` on each call.

**Entry point:** `render()` is called once on page load to hydrate from localStorage.
