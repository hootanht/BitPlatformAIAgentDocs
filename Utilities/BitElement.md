# BitElement Component Documentation

This document serves as a comprehensive reference for the **BitElement** component. It is intended for AI agents, developers, or documentation tools that need to understand the full scope of the component, including its usage, API parameters, and configuration options.

---

## Overview

The **BitElement** component is a simple yet versatile element that allows full control over its underlying HTML tag, styling, attributes, and directional flow. It is designed to integrate seamlessly into the Bit BlazorUI framework. By setting the `Element` property, you can render any valid HTML tag while maintaining consistency with your overall UI design.

---

## Usage

The component can be used in various ways. Below are some usage examples:

### Basic Usage

The default behavior of the component is to render a standard `<div>` element. For example:

```html
<!-- Renders a default div element -->
<div>This is default (div)</div>
```

### Element Example

You can change the rendered HTML element by setting the `Element` property. This example demonstrates rendering different HTML tags like `input`, `a` (anchor), and `button`:

```html
<!-- Render a text input -->
<input placeholder="Input" spellcheck="false">

<!-- Render an anchor (link) element -->
<a href="https://bitplatform.dev/" target="_blank">Anchor (Link)</a>

<!-- Render a button element -->
<button>Button (Click count 0)</button>
```

### Advanced Usage

For dynamic scenarios, you can change the HTML tag at runtime using a dropdown control. This is particularly useful when you need the component to adapt to different contexts. The following example shows a placeholder element and a dropdown that lets the user select between tags such as `div`, `a`, `input`, `button`, etc.

```html
<!-- Placeholder element that will be updated dynamically -->
<div placeholder="div">div</div>

<!-- Dropdown for selecting the HTML element -->
<div style="width: 8rem; margin-top: 0.5rem;">
  <label>Elements</label>
  <div tabindex="0">
    <span>div</span>
    <span><i class="icon-chevron"></i></span>
  </div>
  <!-- Dropdown options -->
  <div role="listbox">
    <button type="button" aria-selected="true"><span>div</span></button>
    <button type="button" aria-selected="false"><span>a</span></button>
    <button type="button" aria-selected="false"><span>input</span></button>
    <button type="button" aria-selected="false"><span>button</span></button>
    <button type="button" aria-selected="false"><span>textarea</span></button>
    <button type="button" aria-selected="false"><span>progress</span></button>
  </div>
</div>
```

---

## API

The component exposes several parameters and public members for customization. The API is split into two main parts: **BitElement parameters** and **BitComponentBase parameters**.

### BitElement Parameters

| **Name**       | **Type**            | **Default value** | **Description**                                            |
| -------------- | ------------------- | ----------------- | ---------------------------------------------------------- |
| ChildContent   | `RenderFragment?`   | `null`            | The content of the element.                              |
| Element        | `string?`           | `null`            | The custom HTML element used for the root node (default is `div`). |

### BitComponentBase Parameters

| **Name**       | **Type**                          | **Default value**                            | **Description**                                                                 |
| -------------- | --------------------------------- | -------------------------------------------- | ------------------------------------------------------------------------------- |
| AriaLabel      | `string?`                         | `null`                                       | The aria-label of the control for the benefit of screen readers.                |
| Class          | `string?`                         | `null`                                       | Custom CSS class for the root element of the component.                         |
| Dir            | `BitDir?`                         | `null`                                       | Determines the component direction (e.g., Ltr, Rtl, Auto).                      |
| HtmlAttributes | `Dictionary<string, object>`      | `new Dictionary<string, object>()`           | Additional attributes to be captured and rendered on the component.             |
| Id             | `string?`                         | `null`                                       | Custom id attribute for the root element (if `null`, a unique ID is generated).   |
| IsEnabled      | `bool`                            | `true`                                       | Indicates whether the component is enabled.                                     |
| Style          | `string?`                         | `null`                                       | Custom CSS style for the root element of the component.                         |
| Visibility     | `BitVisibility`                   | `BitVisibility.Visible`                      | Controls whether the component is visible, hidden, or collapsed.                |

### Public Members of BitComponentBase

| **Name**     | **Type**         | **Default value**     | **Description**                                                                           |
| ------------ | ---------------- | --------------------- | ----------------------------------------------------------------------------------------- |
| UniqueId     | `Guid`           | `Guid.NewGuid()`      | Read-only unique identifier assigned when the component instance is created.              |
| RootElement  | `ElementReference` | *(none)*              | The `ElementReference` of the root element.                                               |

---

## Enums

### BitVisibility Enum

| **Name**  | **Value** | **Description**                                                                 |
| --------- | --------- | ------------------------------------------------------------------------------- |
| Visible   | `0`       | The content of the component is visible.                                        |
| Hidden    | `1`       | The content is hidden but the space remains (using `visibility: hidden`).         |
| Collapsed | `2`       | The component is completely hidden (using `display: none`).                      |

### BitDir Enum

| **Name** | **Value** | **Description**                                                                                   |
| -------- | --------- | ------------------------------------------------------------------------------------------------- |
| Ltr      | `0`       | Left-to-right; for languages like English.                                                       |
| Rtl      | `1`       | Right-to-left; for languages like Arabic.                                                        |
| Auto     | `2`       | Auto-detects directionality based on content (uses a basic algorithm to determine the direction). |

---

## Explanation for AI Agent Usage

This Markdown file is intended as a full reference document for the BitElement component. An AI agent using this file should be able to:

- **Understand Component Purpose:**  
  Recognize that BitElement is designed to offer customizable HTML rendering with built-in support for styling, directionality, and accessibility.

- **Generate Examples:**  
  Use the provided usage examples to generate similar component implementations or demonstrate variations in HTML element rendering.

- **Access API Details:**  
  Reference the tables to extract parameter names, types, default values, and descriptions for integration, debugging, or dynamic documentation generation.

- **Interpret Enumerations:**  
  Utilize the enum details (for BitVisibility and BitDir) to offer precise control over UI behavior in different contexts.

- **Provide Feedback Links:**  
  Direct users to the appropriate GitHub pages for reviewing, editing, or providing feedback on the component.

This comprehensive reference ensures that both human developers and automated tools have all the necessary information to correctly implement, customize, and extend the BitElement component within the Bit BlazorUI framework.