# BitElement Component

**Purpose:** This document provides a reference for the `BitElement` Blazor UI component. It is intended to be used by an AI agent (like GitHub Copilot, Cursor, etc.) to understand its basic functionality, how to customize the rendered HTML tag, and its available API, enabling the agent to provide accurate code suggestions.

**Source:** This information is derived from the Bit Blazor UI documentation for the `BitElement` component.

---

## Overview

*   **Component:** `BitElement`
*   **Purpose:** A versatile utility component that renders a standard HTML element whose tag name can be specified. It provides a way to create basic HTML structures within the Blazor component model, allowing full control over attributes, styling, and content while integrating with base component features like visibility and directionality.
*   **Library:** Bit Blazor UI (`Bit.BlazorUI`)
*   **Default Tag:** Renders as a `<div>` element by default if the `Element` parameter is not specified.

---

## Usage Examples

### 1. Basic Usage (Default Div)

By default, `BitElement` renders a `div` tag containing its `ChildContent`.

```cshtml
<BitElement>This is default (div)</BitElement>
```

**Renders approximately:**

```html
<div id="..." class="bit-elm">This is default (div)</div>
```

### 2. Specifying the HTML Element (`Element` Parameter)

Use the `Element` parameter to define which HTML tag should be rendered. You can then apply standard HTML attributes relevant to that tag directly to the `BitElement` component. These attributes are passed through to the rendered element via Blazor's attribute splatting (`HtmlAttributes`).

```cshtml
@* Render an input element *@
<BitElement Element="input" placeholder="Input" />
<br /><br />

@* Render an anchor (link) element *@
<BitElement Element="a" href="https://bitplatform.dev/" target="_blank">
    Anchor (Link)
</BitElement>
<br /><br />

@* Render a button element with a Blazor event handler *@
<BitElement Element="button" @onclick="() => counter++">
    Button (Click count @counter)
</BitElement>
```

```csharp
@code {
    private int counter;
}
```

**Key Point:** Attributes like `placeholder`, `href`, `target`, and event handlers like `@onclick` are applied directly to the `BitElement` component and will be rendered on the resulting HTML tag specified by the `Element` parameter.

### 3. Dynamic Element Tag

The `Element` parameter can be bound to a variable, allowing the rendered HTML tag to be changed dynamically.

```cshtml
<BitElement Element="@element"
            placeholder="@($"Placeholder for {element}")" @* Example: dynamic attribute *@
            target="_blank"                             @* Will only apply if element is 'a' *@
            href="https://bitplatform.dev/"             @* Will only apply if element is 'a' *@ >
    Rendered as: @element
</BitElement>

<br /><br />
<BitDropdown Label="Select Element" Items="elementsList" @bind-Value="element" Style="width: 8rem;" />
```

```csharp
@code {
    private string element = "div"; // Initial element

    private List<BitDropdownItem<string>> elementsList = new()
    {
            new() { Text = "div", Value = "div" },
            new() { Text = "a", Value = "a" },
            new() { Text = "input", Value = "input" },
            new() { Text = "button", Value = "button" },
            new() { Text = "textarea", Value = "textarea" },
            new() { Text = "progress", Value = "progress" }
    };
}
```

**Note:** Attributes passed to `BitElement` will only have an effect if they are valid for the HTML tag ultimately rendered via the `Element` parameter.

---

## API Reference

### `BitElement` Parameters

| Name         | Type            | Default Value | Description                                                              |
| :----------- | :-------------- | :------------ | :----------------------------------------------------------------------- |
| `ChildContent`| `RenderFragment?`| `null`        | The content to be rendered inside the element.                           |
| `Element`    | `string?`       | `"div"`       | The HTML tag name to render for the root node. Defaults to `"div"`.      |

### Inherited Parameters (`BitComponentBase`)

These parameters provide common functionality inherited from the base class.

| Name             | Type                          | Default Value              | Description                                                                                    |
| :--------------- | :---------------------------- | :------------------------- | :--------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                     | `null`                     | The `aria-label` attribute for accessibility.                                                  |
| `Class`          | `string?`                     | `null`                     | Custom CSS class(es) applied to the rendered element.                                          |
| `Dir`            | `BitDir?`                     | `null`                     | Sets the text direction (`Ltr`, `Rtl`, `Auto`). See `BitDir` enum below.                       |
| `HtmlAttributes` | `Dictionary<string, object>`  | `new Dictionary<>()`       | Captures and renders additional HTML attributes not explicitly defined as parameters.          |
| `Id`             | `string?`                     | `null`                     | Custom `id` attribute for the rendered element. If `null`, a unique ID (`UniqueId`) is used.  |
| `IsEnabled`      | `bool`                        | `true`                     | Whether the component is enabled (affects styling and potentially behavior like `disabled` attribute). |
| `Style`          | `string?`                     | `null`                     | Custom inline CSS style(s) applied to the rendered element.                                    |
| `Visibility`     | `BitVisibility`               | `BitVisibility.Visible`    | Controls the element's visibility using CSS (`Visible`, `Hidden`, `Collapsed`). See enum below. |

### Public Members (`BitComponentBase`)

These are public properties available on the component instance.

| Name          | Type               | Default Value    | Description                                                                           |
| :------------ | :----------------- | :--------------- | :------------------------------------------------------------------------------------ |
| `UniqueId`    | `string`           | `Guid.NewGuid()` | Readonly unique identifier generated for the component instance. Used if `Id` is null. |
| `RootElement` | `ElementReference` |                  | A reference to the rendered HTML element (available after rendering).                 |

### Supporting Enums

#### `BitVisibility` Enum

Used for the inherited `Visibility` parameter.

| Name        | Value | Description                                                        |
| :---------- | :---- | :----------------------------------------------------------------- |
| `Visible`   | `0`   | Element is visible (default).                                      |
| `Hidden`    | `1`   | Element is hidden (`visibility: hidden;`), still occupies space.   |
| `Collapsed` | `2`   | Element is hidden (`display: none;`), does not occupy space.       |

#### `BitDir` Enum

Used for the inherited `Dir` parameter.

| Name   | Value | Description                                     |
| :----- | :---- | :---------------------------------------------- |
| `Ltr`  | `0`   | Left-to-right text direction.                   |
| `Rtl`  | `1`   | Right-to-left text direction.                   |
| `Auto` | `2`   | Browser determines direction based on content. |

---

**End of Reference**

**Explanation of the Markdown File:**

1.  **Standard Header:** Identifies the component (`BitElement`) and its purpose as an AI reference file.
2.  **Overview:** Summarizes the component's core function – rendering a customizable HTML tag – and notes its default behavior (`div`).
3.  **Usage Examples:**
    *   **Basic:** Shows the simplest use case and clarifies the default rendered tag. Includes an approximate HTML output for clarity.
    *   **Element Parameter:** Demonstrates how to change the tag (`input`, `a`, `button`) using the `Element` parameter. Crucially, it highlights that standard HTML attributes and Blazor event handlers (`placeholder`, `href`, `@onclick`) are passed directly to `BitElement` and rendered appropriately on the resulting tag.
    *   **Dynamic Element:** Shows binding the `Element` parameter to a C# variable, enabling dynamic tag rendering. Reinforces the concept of attribute applicability based on the rendered tag.
4.  **API Reference:**
    *   Uses Markdown tables for clear presentation of parameters.
    *   **`BitElement` Parameters:** Lists parameters specific to `BitElement` (`ChildContent`, `Element`). The default for `Element` is explicitly stated as `"div"` based on the overview/examples, overriding the `null` listed in the source table's default column (as the description/behavior is more informative).
    *   **Inherited Parameters:** Details parameters from `BitComponentBase`, explaining their general purpose in the context of this component. `HtmlAttributes` is noted for handling arbitrary attributes.
    *   **Public Members:** Lists `UniqueId` and `RootElement`.
    *   **Supporting Enums:** Defines `BitVisibility` and `BitDir` as they are relevant inherited parameters.
5.  **Formatting and Clarity:** Uses standard Markdown features (headings, code blocks with language tags, tables, bold text, backticks) to structure the information logically and make it easy for both humans and AI to parse and understand. Key concepts like attribute passthrough and the default tag are emphasized.

This structure provides the AI agent with:
*   A clear understanding of what `BitElement` does.
*   Concrete examples of how to use it for different HTML tags.
*   An explanation of how standard HTML attributes and Blazor events integrate.
*   A complete list of its own and inherited parameters.
*   Definitions of relevant enums.
