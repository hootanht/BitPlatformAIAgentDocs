# BitCard Component

**Purpose:** This document provides a detailed reference for the `BitCard` Blazor UI component. It is intended to be used by an AI agent (like GitHub Copilot, Cursor, etc.) to understand the component's functionality, usage patterns, and API, enabling the agent to provide accurate code suggestions and assistance related to `BitCard`.

**Source:** This information is derived from the Bit Blazor UI documentation for the `BitCard` component.

---

## Overview

*   **Component:** `BitCard`
*   **Purpose:** Provides a container to wrap around specific content, typically focused on a single subject to maintain a clean design.
*   **Library:** Bit Blazor UI (`Bit.BlazorUI`)

A `BitCard` acts as a distinct visual surface or container for grouping related information or actions.

---

## Usage Examples

Here are common ways to use the `BitCard` component.

### 1. Basic Card

This example demonstrates the fundamental structure of a `BitCard`. It uses `BitStack` to arrange content vertically within the card.

```cshtml
<BitCard>
    <BitStack HorizontalAlign="BitAlignment.Start">
        <BitText Typography="BitTypography.H4">bit BlazorUI</BitText>
        <BitText Typography="BitTypography.Body1">
            bit BlazorUI components are native, easy-to-customize, and ...
        </BitText>
        <BitLink Href="https://blazorui.bitplatform.dev" Target="_blank">Learn more</BitLink>
    </BitStack>
</BitCard>
```

### 2. Background Customization

The `Background` parameter allows setting the card's background color using predefined `BitColorKind` options.

```cshtml
@* Component to select the background color *@
<BitChoiceGroup @bind-Value="backgroundColorKind" Horizontal
                TItem="BitChoiceGroupOption<BitColorKind>" TValue="BitColorKind">
    <BitChoiceGroupOption Text="Primary" Value="BitColorKind.Primary" />
    <BitChoiceGroupOption Text="Secondary" Value="BitColorKind.Secondary" />
    <BitChoiceGroupOption Text="Tertiary" Value="BitColorKind.Tertiary" />
    <BitChoiceGroupOption Text="Transparent" Value="BitColorKind.Transparent" />
</BitChoiceGroup>

<div style="padding:2rem; background:lightgray;"> @* Added container for contrast *@
    <BitCard Background="backgroundColorKind">
        <BitStack HorizontalAlign="BitAlignment.Start">
            <BitText Typography="BitTypography.H4">bit BlazorUI</BitText>
            <BitText Typography="BitTypography.Body1">
                bit BlazorUI components are native, easy-to-customize, and ...
            </BitText>
            <BitLink Href="https://blazorui.bitplatform.dev" Target="_blank">Learn more</BitLink>
        </BitStack>
    </BitCard>
</div>
```

```csharp
@code {
    private BitColorKind backgroundColorKind = BitColorKind.Primary;
}
```

* **Note:** `BitColorKind` is an enum with values like `Primary`, `Secondary`, `Tertiary`, `Transparent`. See the API section for details.

### 3. Border Customization

Similar to `Background`, the `Border` parameter controls the card's border color using `BitColorKind`.

```cshtml
@* Component to select the border color *@
<BitChoiceGroup @bind-Value="borderColorKind" Horizontal
                TItem="BitChoiceGroupOption<BitColorKind>" TValue="BitColorKind">
    <BitChoiceGroupOption Text="Primary" Value="BitColorKind.Primary" />
    <BitChoiceGroupOption Text="Secondary" Value="BitColorKind.Secondary" />
    <BitChoiceGroupOption Text="Tertiary" Value="BitColorKind.Tertiary" />
    <BitChoiceGroupOption Text="Transparent" Value="BitColorKind.Transparent" />
</BitChoiceGroup>

<BitCard Border="borderColorKind">
    <BitStack HorizontalAlign="BitAlignment.Start">
        <BitText Typography="BitTypography.H4">bit BlazorUI</BitText>
        <BitText Typography="BitTypography.Body1">
            bit BlazorUI components are native, easy-to-customize, and ...
        </BitText>
        <BitLink Href="https://blazorui.bitplatform.dev" Target="_blank">Learn more</BitLink>
    </BitStack>
</BitCard>
```

```csharp
@code {
    private BitColorKind borderColorKind = BitColorKind.Primary;
}
```

### 4. Sizing (FullSize, FullWidth, FullHeight)

These boolean parameters control whether the card expands to fill its parent container's dimensions.

* `FullWidth`: Makes the card take 100% width of its parent.
* `FullHeight`: Makes the card take 100% height of its parent. Requires the parent to have a defined height.
* `FullSize`: A shorthand for setting both `FullWidth` and `FullHeight` to true.

```cshtml
@* Component to select the sizing option *@
<BitChoiceGroup @bind-Value="sizeMode" Horizontal
                TItem="BitChoiceGroupOption<int>" TValue="int">
    <BitChoiceGroupOption Text="FullSize" Value="0" />
    <BitChoiceGroupOption Text="FullWidth" Value="1" />
    <BitChoiceGroupOption Text="FullHeight" Value="2" />
    <BitChoiceGroupOption Text="Default" Value="3" /> @* Added default option for clarity *@
</BitChoiceGroup>

<div style="padding:2rem; background:lightgray; height:300px; width: 400px; border: 1px dashed blue;"> @* Parent container with defined dimensions *@
    <BitCard FullSize="sizeMode == 0"
             FullWidth="sizeMode == 1"
             FullHeight="sizeMode == 2">
        <BitStack HorizontalAlign="BitAlignment.Start">
            <BitText Typography="BitTypography.H4">bit BlazorUI</BitText>
            <BitText Typography="BitTypography.Body1">
                bit BlazorUI components are native, easy-to-customize, and ...
            </BitText>
            <BitLink Href="https://blazorui.bitplatform.dev" Target="_blank">Learn more</BitLink>
        </BitStack>
    </BitCard>
</div>
```

```csharp
@code {
    private int sizeMode = 3; // Default to normal size
}
```

---

## API Reference

### `BitCard` Parameters

These are parameters specific to the `BitCard` component.

| Name         | Type             | Default Value | Description                                                        |
| :----------- | :--------------- | :------------ | :----------------------------------------------------------------- |
| `Background` | `BitColorKind?`  | `null`        | The color kind of the background of the card.                      |
| `Border`     | `BitColorKind?`  | `null`        | The color kind of the border of the card.                          |
| `ChildContent`| `RenderFragment`| `null`        | The content to be rendered inside the card.                        |
| `FullHeight` | `bool`           | `false`       | Makes the card height 100% of its parent container.                |
| `FullSize`   | `bool`           | `false`       | Makes the card width **and** height 100% of its parent container. |
| `FullWidth`  | `bool`           | `false`       | Makes the card width 100% of its parent container.                 |

### Inherited Parameters (`BitComponentBase`)

These parameters are inherited from the base component class and are available on `BitCard`.

| Name             | Type                          | Default Value                         | Description                                                                                    |
| :--------------- | :---------------------------- | :------------------------------------ | :--------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                     | `null`                                | The `aria-label` attribute for accessibility.                                                  |
| `Class`          | `string?`                     | `null`                                | Custom CSS class(es) for the root element.                                                     |
| `Dir`            | `BitDir?`                     | `null`                                | Specifies the text direction (`Ltr`, `Rtl`, `Auto`).                                           |
| `HtmlAttributes` | `Dictionary<string, object>`  | `new Dictionary<string, object>()`    | Allows capturing and rendering additional HTML attributes.                                     |
| `Id`             | `string?`                     | `null`                                | Custom `id` attribute for the root element. If `null`, a unique ID (`UniqueId`) is generated. |
| `IsEnabled`      | `bool`                        | `true`                                | Whether the component is enabled. Affects styling (e.g., opacity) but not direct interaction unless combined with other logic. |
| `Style`          | `string?`                     | `null`                                | Custom inline CSS style(s) for the root element.                                               |
| `Visibility`     | `BitVisibility`               | `BitVisibility.Visible`               | Controls the component's visibility (`Visible`, `Hidden`, `Collapsed`).                          |

### Public Members (`BitComponentBase`)

These are public properties available on the component instance.

| Name          | Type               | Default Value    | Description                                                                           |
| :------------ | :----------------- | :--------------- | :------------------------------------------------------------------------------------ |
| `UniqueId`    | `string`           | `Guid.NewGuid()` | Readonly unique identifier generated for the component instance. Used if `Id` is null. |
| `RootElement` | `ElementReference` |                  | A reference to the root HTML element of the component (available after rendering).      |

### Supporting Enums

#### `BitColorKind` Enum

Used for `Background` and `Border` parameters.

| Name          | Value | Description                 |
| :------------ | :---- | :-------------------------- |
| `Primary`     | `0`   | The primary color theme.    |
| `Secondary`   | `1`   | The secondary color theme.  |
| `Tertiary`    | `2`   | The tertiary color theme.   |
| `Transparent` | `3`   | Transparent color.          |

#### `BitVisibility` Enum

Used for the `Visibility` parameter.

| Name        | Value | Description                                                              |
| :---------- | :---- | :----------------------------------------------------------------------- |
| `Visible`   | `0`   | Component is visible (default).                                          |
| `Hidden`    | `1`   | Component is hidden (`visibility: hidden;`), still occupies space.       |
| `Collapsed` | `2`   | Component is hidden (`display: none;`), does not occupy space.           |

#### `BitDir` Enum

Used for the `Dir` parameter.

| Name   | Value | Description                                                                                                                  |
| :----- | :---- | :--------------------------------------------------------------------------------------------------------------------------- |
| `Ltr`  | `0`   | Left-to-right text direction.                                                                                                |
| `Rtl`  | `1`   | Right-to-left text direction.                                                                                                |
| `Auto` | `2`   | Lets the browser determine the direction based on content.                                                                   |

---

**End of Reference**

**Explanation of the Markdown File:**

1.  **Header and Purpose:** Clearly states the document's goal – to be an AI reference for the `BitCard` component.
2.  **Overview:** Provides a quick summary of the component's purpose and library.
3.  **Usage Examples:**
    *   Each example has a clear heading (`###`).
    *   A brief explanation describes the purpose of the example.
    *   Code blocks (```cshtml` and ```csharp`) contain the relevant Blazor component markup and C# code-behind logic.
    *   Important parameters demonstrated in the examples (like `Background`, `Border`, `FullSize`) are mentioned.
4.  **API Reference:**
    *   Structured using headings (`###`) for different categories of parameters/members (Component-specific, Inherited, Public Members, Enums).
    *   Markdown tables (`| Name | Type | ... |`) are used for easy parsing of parameter details (Name, Type, Default Value, Description). This is a format that AI models can often process effectively.
    *   Code formatting (backticks `` ` ``) is used for parameter names, types, and enum values for clarity.
    *   Default values are explicitly mentioned.
    *   Descriptions are concise and explain the function of each parameter/member/enum value.
5.  **Supporting Enums:** Dedicated tables explain the possible values for enums like `BitColorKind`, `BitVisibility`, and `BitDir`, which are crucial for using related parameters correctly.
6.  **Markdown Formatting:** Uses standard Markdown syntax (headings, code blocks, tables, bold/italic text, backticks) for structure and readability, making it suitable for various Markdown renderers and AI interpretation.

This structure allows an AI agent to quickly find information about:
*   How to instantiate a basic `BitCard`.
*   How to apply common customizations like background, border, and sizing.
*   What parameters are available, their types, defaults, and descriptions.
*   What inherited features are accessible.
*   The valid values for specific enum-based parameters.
