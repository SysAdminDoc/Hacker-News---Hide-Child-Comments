# Hacker News - Hide Child Comments

A RES-like feature to hide child comments on Hacker News posts.

-----

## Introduction

This browser extension enhances the Hacker News comment reading experience by adding the ability to collapse and expand comment threads. By default, all child comments are hidden, providing a cleaner, more readable top-level view of the discussion. Users can then selectively expand threads they are interested in, similar to the user experience found on Reddit with Reddit Enhancement Suite (RES). This script aims to improve navigation and focus when reading long and complex comment sections on Hacker News.

-----

## Features

### 1\. **Hide Child Comments by Default**

  * **What it does:** Automatically collapses all nested comment threads when a Hacker News item page is loaded.
  * **How it improves the target interface:** This declutters the page, making it easier to scan top-level comments and identify interesting discussion threads without being overwhelmed by a "wall of text."
  * **Example usage:** Upon loading a story, only the direct replies to the story are visible.

### 2\. **Toggle Comment Visibility with `[+]` / `[-]` Button**

  * **What it does:** Adds a clickable `[+]` (expand) or `[-]` (collapse) button next to the comment's metadata.
  * **How it improves the target interface:** Provides a clear and intuitive control, familiar to users of other forum software, to show or hide child comments for a specific parent comment.
  * **Example Code Snippet:** A toggle button is inserted into the comment's footer element.
    ```javascript
    const toggleBtn = document.createElement('a');
    toggleBtn.href = 'javascript:void(0)';
    toggleBtn.className = 'hn-toggle-btn';
    toggleBtn.textContent = '[+]'; // Default state is collapsed
    footer.appendChild(toggleBtn);
    ```

### 3\. **Clickable Reply Count**

  * **What it does:** Makes the reply count next to the toggle button clickable, performing the same collapse/expand action.
  * **How it improves the target interface:** Offers a larger, more accessible click target for toggling comment threads and provides a title attribute on hover to inform the user of the action.
  * **Example usage:** Clicking on the text "3 replies" will expand or collapse the three child comments.

-----

## Installation

### Prerequisites

  * A modern web browser (like Chrome, Firefox, or Edge).
  * A userscript manager extension, such as **Tampermonkey** or **Greasemonkey**.

### Step-by-step instructions

1.  **Install a Userscript Manager:** If you don't have one, install Tampermonkey from the extension store for your browser.
2.  **Install the Script:**
      * Open the `Hacker News - Hide Child Comments + Clickable Reply Count-1.5.user.js` file.
      * Your userscript manager should automatically detect the `.user.js` file and open a new tab for installation.
      * Click the **Install** button to add the script to your manager.

-----

## Usage

Once installed, the userscript runs automatically.

1.  Navigate to any Hacker News comment page (i.e., a URL matching `https://news.ycombinator.com/item?id=*`).
2.  Observe that all comment threads are collapsed by default, showing only top-level comments.
3.  To expand a thread, click the `[+]` button or the reply count text (e.g., `5 replies`).
4.  The button will change to `[-]`, and the child comments will appear.
5.  Click the `[-]` button or the reply count again to collapse the thread.

-----

## Configuration

This userscript requires no configuration. The features are enabled by default and there are no settings to adjust.

-----

## Screenshots

*(This section would contain screenshots or GIFs demonstrating the extension's features in action. For example, a before-and-after shot of a comment thread, or an animation showing the expand/collapse functionality.)*

-----

### Core modules and their responsibilities

The script is contained within a single Immediately Invoked Function Expression (IIFE) to avoid polluting the global namespace.

  * **Main IIFE `(function () { ... })();`**: Wraps the entire script to ensure 'use strict' compliance and encapsulation.
  * **`addToggleButtons()`**: The main function that runs on window load. It iterates through all comments on the page, identifies those with children, and injects the toggle button and clickable reply count.
  * **`toggleChildren()`**: The event handler that performs the show/hide logic for a comment thread. It finds all child comments and toggles their CSS `display` property.
  * **`getChildren()`**: A helper function that, given a parent comment's table row, finds and returns an array of all its direct and indirect child comment rows.
  * **`getDepth()`**: A helper function that determines the nesting level of a comment by reading the width of the indentation image.

-----

## API / Function Reference

### 1\. `getDepth(row)`

  * **Parameters:**
      * `row` (HTMLElement): The `<tr>` element of a comment.
  * **Return value:** (Number) The nesting depth of the comment, starting from 0.
  * **Purpose:** To determine the hierarchical relationship between comments.

### 2\. `getChildren(parentRow)`

  * **Parameters:**
      * `parentRow` (HTMLElement): The `<tr>` element of the parent comment.
  * **Return value:** (Array\<HTMLElement\>) A list of all `<tr>` elements that are children of the parent.
  * **Purpose:** To identify all comments in a thread that need to be hidden or shown.

### 3\. `toggleChildren(parentRow, toggleBtn, replyCountSpan)`

  * **Parameters:**
      * `parentRow` (HTMLElement): The `<tr>` element of the parent comment being toggled.
      * `toggleBtn` (HTMLElement): The `<a>` element that acts as the `[+]`/`[-]` button.
      * `replyCountSpan` (HTMLElement): The `<span>` element displaying the number of replies.
  * **Return value:** `void`
  * **Purpose:** To handle the click event, toggle the display of child comments, and update the button text.

### 4\. `addToggleButtons()`

  * **Parameters:** None
  * **Return value:** `void`
  * **Purpose:** To initialize the extension. It scans the page for comments and injects the necessary HTML and event listeners to enable the toggle functionality.

-----

## Contributing

### How to report issues

Please open an issue on the project's GitHub page. In your report, include:

  * A clear and descriptive title.
  * The browser and userscript manager versions you are using.
  * Steps to reproduce the bug.
  * Any relevant console errors.

### How to submit pull requests

1.  Fork the repository.
2.  Create a new branch for your feature or bug fix.
3.  Make your changes and commit them with a descriptive message.
4.  Push your branch to your fork.
5.  Open a pull request to the main repository.

### Coding style guidelines

Please follow the existing coding style. The script uses standard JavaScript with `'use strict'` enabled.

-----

## Changelog

### [1.5] - 2025-07-12

  * Initial public release version.
  * Hides child comments by default.
  * Adds `[+]`/`[-]` toggle buttons to comments with children.
  * Adds a clickable reply count for expanding/collapsing threads.

-----

## License

This project is licensed under the **MIT License**.

-----

## Disclosure

This is a third-party userscript and is not created by, affiliated with, or endorsed by Hacker News or Y Combinator. It is an independent open source project created to enhance the user experience of the website.
