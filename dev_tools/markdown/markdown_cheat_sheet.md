# Markdown cheat sheet

Markdown is a plain-text format for technical documentation. This guide covers
headings, lists, links, figures, code, and tables, with examples for documenting
a computational method and its results. GitHub renders README files automatically;
in VS Code, use **Markdown: Open Preview** to inspect a document while editing.

**Contents:** [Headings](#headings) · [Emphasis](#emphasis) · [Lists](#lists)
· [Links](#links) · [Images](#images) · [Code](#code-blocks) · [Tables](#tables)
· [Examples](#examples)

## Headings

Use one `#` heading for the document title and `##` headings for its main sections.
Add a blank line before and after headings, paragraphs, lists, and fenced code blocks.

```markdown
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
```

## Emphasis

- **Bold**

  ```markdown
  **This text is bold**
  ```

- *Italic*

  ```markdown
  *This text is italic*
  ```

- ***Bold and Italic***

  ```markdown
  ***This text is bold and italic***
  ```

## Lists

- **Unordered List**

  ```markdown
  - Item 1
  - Item 2
    - Subitem 2a
    - Subitem 2b
  ```

- **Ordered List**

  ```markdown
  1. First item
  2. Second item
     1. Subitem 2a
     2. Subitem 2b
  ```

## Links

- **Inline Link**

  ```markdown
  [Link Text](https://www.example.com)
  ```

- **Reference Link**

  ```markdown
  [Link Text][1]

  [1]: https://www.example.com
  ```

## Images

- **Embedding an Image**

  ```markdown
  ![Alt Text](path/to/image.png "Optional Title")
  ```

  Example path, assuming an `images` subfolder beside the document:

  ```markdown
  ![Generated Pattern](images/pattern_example1.png "Pattern Example 1")
  ```

## Code Blocks

- **Inline Code**

  ```markdown
  Use the `print()` function to display output.
  ```

- **Fenced Code Block**

  Surround the code with triple backticks and identify the language:

  ````markdown
  ```python
  import numpy as np
  array = np.zeros((100, 100, 3))
  ```
  ````

- **Indented Code Block**

  ```markdown
      This is an indented code block.
  ```

## Blockquotes

```markdown
> This is a blockquote.
>
> It can span multiple lines.
```

## Horizontal Rule

```markdown
---

```

## Tables

```markdown
| Column 1 | Column 2 | Column 3 |
| -------- | -------- | -------- |
| Data 1   | Data 2   | Data 3   |
| Data 4   | Data 5   | Data 6   |
```

## Task Lists

```markdown
- [x] Task 1
- [ ] Task 2
- [ ] Task 3
```

## Footnotes

```markdown
Here's a sentence with a footnote.[^1]

[^1]: This is the footnote.
```

## Strikethrough

```markdown
~~This text is crossed out.~~
```

---

## Examples

### Including an Image in Your Documentation

For a document with an `images` subfolder, use a path relative to that document.
The filename below is illustrative; replace it with an image in your project:

```markdown
![Pattern Example](images/pattern_example1.png "Generated Pattern")
```

### Creating a Table to Summarize Results

```markdown
| Method            | Description                               |
| ----------------- | ----------------------------------------- |
| `np.zeros()`      | Creates an array filled with zeros        |
| `np.random.rand()`| Generates random numbers between 0 and 1  |
```

---

## Tips

- **Preview Your Markdown**: Use a Markdown editor or GitHub's preview feature to check your formatting.
- **Keep It Simple**: Clarity is more important than complex formatting.
- **Use Headings**: Organize your document with headings for easy navigation.
