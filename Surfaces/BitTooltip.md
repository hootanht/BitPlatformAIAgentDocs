# BitTooltip Component

**Purpose:** This document provides a detailed reference for the `BitTooltip` Blazor UI component. It is intended to be used by an AI agent (like GitHub Copilot, Cursor, etc.) to understand the component's functionality, usage patterns, and API, enabling the agent to provide accurate code suggestions and assistance related to `BitTooltip`.

**Source:** This information is derived from the Bit Blazor UI documentation for the `BitTooltip` component.

---

## Overview

*   **Component:** `BitTooltip`
*   **Purpose:** Displays brief descriptive text or additional information when the user interacts (hovers, clicks, focuses) with an associated element (the anchor). Useful for explaining unlabeled controls or supplementing labeled ones.
*   **Library:** Bit Blazor UI (`Bit.BlazorUI`)

---

## Usage Examples

Here are common ways to use the `BitTooltip` component.

### 1. Basic Tooltip

The simplest usage involves wrapping the target element (anchor) with `BitTooltip` and providing the tooltip content via the `Text` parameter. The tooltip appears on hover by default.

```cshtml
<BitTooltip Text="This is the tooltip text">
    <BitButton Variant="BitVariant.Outline">Hover over me</BitButton>
</BitTooltip>
```

* **Note:** The element directly inside `BitTooltip` (or inside the `<Anchor>` tag) becomes the anchor element that triggers the tooltip.

### 2. Position

The `Position` parameter controls where the tooltip appears relative to the anchor element, using the `BitTooltipPosition` enum. `DefaultIsShown="true"` makes the tooltip visible initially for demonstration.

```cshtml
@* Top Position (Default) *@
<BitTooltip DefaultIsShown="true" Text="Text" Position="BitTooltipPosition.Top">
    <BitButton Variant="BitVariant.Outline">Top</BitButton>
</BitTooltip>

@* Right Position *@
<BitTooltip DefaultIsShown="true" Text="Text" Position="BitTooltipPosition.Right">
    <BitButton Variant="BitVariant.Outline">Right</BitButton>
</BitTooltip>

@* Left Position *@
<BitTooltip DefaultIsShown="true" Text="Text" Position="BitTooltipPosition.Left">
    <BitButton Variant="BitVariant.Outline">Left</BitButton>
</BitTooltip>

@* Bottom Position *@
<BitTooltip DefaultIsShown="true" Text="Text" Position="BitTooltipPosition.Bottom">
    <BitButton Variant="BitVariant.Outline">Bottom</BitButton>
</BitTooltip>
```

* **Note:** See the `BitTooltipPosition` enum definition in the API section for all available positions.

### 3. Custom Content (`Template` and `Anchor` Tags)

Instead of simple text, you can provide complex HTML content within the `<Template>` tag. The anchor element should then be placed within the `<Anchor>` tag.

```cshtml
<BitTooltip>
    <Template>
        @* Custom HTML content for the tooltip *@
        <ul style="padding: 0.5rem; margin: 0;">
            <li>1. One</li>
            <li>2. Two</li>
        </ul>
    </Template>
    <Anchor>
        @* The element that triggers the tooltip *@
        <BitButton Variant="BitVariant.Outline">Hover over me</BitButton>
    </Anchor>
</BitTooltip>
```

* **Note:** If `<Template>` is used, the `Text` parameter is ignored. If `<Anchor>` is used, `ChildContent` is ignored.

### 4. Advanced Options

Control visibility, behavior, and appearance using various parameters:

* `@bind-IsShown`: Programmatically control the tooltip's visibility (two-way binding).
* `HideArrow`: Removes the pointer arrow from the tooltip bubble.
* `HideDelay`: Delay in milliseconds before the tooltip hides after the trigger condition ceases (e.g., mouse leaves).
* `ShowOnClick`: Makes the tooltip appear only when the anchor is clicked.
* `ShowOnHover`: Makes the tooltip appear when the anchor is hovered (default is true).
* `ShowOnFocus`: Makes the tooltip appear when the anchor receives focus.
* `ShowDelay`: Delay in milliseconds before the tooltip appears after the trigger condition starts.
* `Position`: Sets the tooltip position dynamically.

```cshtml
<BitTooltip @bind-IsShown="isShown"
            Text="Text"
            HideArrow="hideArrow"
            HideDelay="(int)hideDelay"
            ShowOnClick="showOnClick"
            ShowOnHover="showOnHover"
            ShowOnFocus="showOnFocus" @* Added ShowOnFocus example *@
            ShowDelay="(int)showDelay" @* Added ShowDelay example *@
            Position="tooltipPosition">
    <BitButton Variant="BitVariant.Outline">Anchor</BitButton>
</BitTooltip>

@* Controls to modify tooltip behavior dynamically *@
<BitDropdown Label="Tooltip positions" Items="tooltipPositionList" @bind-Value="tooltipPosition" />
<BitNumberField Label="Show delay (ms)" @bind-Value="showDelay" Mode="BitSpinButtonMode.Inline" Step="50" Min="0"/>
<BitNumberField Label="Hide delay (ms)" @bind-Value="hideDelay" Mode="BitSpinButtonMode.Inline" Step="50" Min="0"/>
<BitToggle @bind-Value="isShown" Label="Is Shown (Manual Control)" />
<BitToggle @bind-Value="hideArrow" Label="Hide Arrow" />
<BitToggle @bind-Value="showOnClick" Label="Show On Click" />
<BitToggle @bind-Value="showOnHover" Label="Show On Hover" />
<BitToggle @bind-Value="showOnFocus" Label="Show On Focus" />

```

```csharp
@code {
    private bool isShown = false; // Default to hidden for manual control example
    private bool showOnClick = false;
    private bool showOnHover = true; // Default behavior
    private bool showOnFocus = false;
    private bool hideArrow = false;
    private double showDelay = 0; // Default: show immediately on trigger
    private double hideDelay = 0; // Default: hide immediately on trigger end

    private BitTooltipPosition tooltipPosition = BitTooltipPosition.Top; // Default position

    private readonly List<BitDropdownItem<BitTooltipPosition>> tooltipPositionList =
        Enum.GetValues(typeof(BitTooltipPosition))
            .Cast<BitTooltipPosition>()
            .Select(enumValue => new BitDropdownItem<BitTooltipPosition>
            {
                Value = enumValue,
                Text = enumValue.ToString()
            })
            .ToList();
}
```

### 5. Styles & Classes

Customize the appearance using inline styles or CSS classes.

* **`Styles`**: An object (`BitTooltipClassStyles`) to apply inline styles to specific parts (`Root`, `TooltipWrapper`, `Tooltip`, `Arrow`).
* **`Classes`**: An object (`BitTooltipClassStyles`) to apply CSS classes to specific parts.

```cshtml
<style>
    .custom-tooltip {
        color: tomato;
        border: 1px solid tomato; /* Adjusted border thickness */
        border-radius: 0.5rem;
        background-color: lightyellow; /* Added background for visibility */
        padding: 0.5rem; /* Added padding */
    }

    .custom-arrow {
        /* Style the arrow base/background */
        background-color: lightyellow;
    }
    .custom-arrow::before {
         /* Style the arrow borders */
        border-color: tomato transparent transparent tomato; /* Example for top position */
    }

    /* Example for different positions (adapt ::before border-color accordingly) */
    .bit-ttp-rgt .custom-arrow::before { border-color: transparent tomato tomato transparent; }
    .bit-ttp-btm .custom-arrow::before { border-color: transparent transparent tomato tomato; }
    .bit-ttp-lft .custom-arrow::before { border-color: tomato transparent transparent tomato; }
</style>

@* Using Styles *@
<BitTooltip Text="Styled tooltip text"
            Styles="@(new() { Tooltip = "box-shadow: aqua 0 0 0.5rem; background-color: navy; color: white;" })">
    <BitButton Variant="BitVariant.Outline">Hover (Inline Style)</BitButton>
</BitTooltip>

@* Using Classes *@
<BitTooltip Text="Classed tooltip text"
            Classes="@(new() { Tooltip = "custom-tooltip", Arrow = "custom-arrow" })">
    <BitButton Variant="BitVariant.Outline">Hover (CSS Classes)</BitButton>
</BitTooltip>
```

* **Note:** Styling the arrow often requires targeting the pseudo-element (`::before` or `::after`) depending on the specific implementation, which might be complex via `Styles` parameter. Using `Classes` is generally more robust for arrow styling. The example above simplifies arrow class styling.

### 6. RTL (Right-to-Left)

Set the `Dir="BitDir.Rtl"` parameter on the `BitTooltip` component for right-to-left language support. This affects text direction and potentially positioning logic.

```cshtml
<BitTooltip Dir="BitDir.Rtl">
    <Template>
        <ul style="padding: 0.5rem; margin: 0;">
            <li>۱. یک</li>
            <li>۲. دو</li>
        </ul>
    </Template>
    <Anchor>
        <BitButton Variant="BitVariant.Outline">نشانگر ماوس را روی من بیاورید</BitButton>
    </Anchor>
</BitTooltip>
```

---

## API Reference

### `BitTooltip` Parameters

| Name             | Type                     | Default Value            | Description                                                                                                |
| :--------------- | :----------------------- | :----------------------- | :--------------------------------------------------------------------------------------------------------- |
| `Anchor`         | `RenderFragment?`        | `null`                   | The target component or element that the tooltip is anchored to. Used when `<Template>` is specified.      |
| `ChildContent`   | `RenderFragment?`        | `null`                   | The target component or element that the tooltip is anchored to. Used when `Text` is specified (default).    |
| `Classes`        | `BitTooltipClassStyles?` | `null`                   | Custom CSS classes for different parts (`Root`, `TooltipWrapper`, `Tooltip`, `Arrow`). See class definition. |
| `DefaultIsShown` | `bool`                   | `false`                  | Initial visibility state of the tooltip (uncontrolled).                                                    |
| `HideArrow`      | `bool`                   | `false`                  | Hides the pointer arrow of the tooltip.                                                                    |
| `HideDelay`      | `int`                    | `0`                      | Delay in milliseconds before hiding the tooltip after the trigger condition ends.                          |
| `IsShown`        | `bool`                   | `false`                  | Controls the visibility state of the tooltip (controlled). Use `@bind-IsShown` for two-way binding.         |
| `IsShownChanged` | `EventCallback<bool>`    |                          | Callback invoked when the `IsShown` state changes.                                                         |
| `Position`       | `BitTooltipPosition`     | `BitTooltipPosition.Top` | Specifies the position of the tooltip relative to the anchor. See enum definition.                         |
| `ShowOnClick`    | `bool`                   | `false`                  | If true, the tooltip appears when the anchor element is clicked.                                           |
| `ShowDelay`      | `int`                    | `0`                      | Delay in milliseconds before showing the tooltip after the trigger condition starts.                       |
| `ShowOnFocus`    | `bool`                   | `false`                  | If true, the tooltip appears when the anchor element receives focus.                                       |
| `ShowOnHover`    | `bool`                   | `true`                   | If true, the tooltip appears when the mouse pointer hovers over the anchor element.                        |
| `Styles`         | `BitTooltipClassStyles?` | `null`                   | Custom inline CSS styles for different parts (`Root`, `TooltipWrapper`, `Tooltip`, `Arrow`). See class def. |
| `Template`       | `RenderFragment?`        | `null`                   | Custom `RenderFragment` content to display inside the tooltip. Overrides the `Text` parameter.             |
| `Text`           | `string?`                | `null`                   | The simple text content to display inside the tooltip. Ignored if `Template` is provided.                  |

### Inherited Parameters (`BitComponentBase`)

These parameters are inherited from the base component class and are available on `BitTooltip`.

| Name             | Type                          | Default Value              | Description                                                                                    |
| :--------------- | :---------------------------- | :------------------------- | :--------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                     | `null`                     | The aria-label for the tooltip content itself (may not be needed if content describes anchor). |
| `Class`          | `string?`                     | `null`                     | Custom CSS class(es) for the root element of the tooltip component structure.                  |
| `Dir`            | `BitDir?`                     | `null`                     | Sets the text direction (`Ltr`, `Rtl`, `Auto`) for the tooltip content. See `BitDir` enum.     |
| `HtmlAttributes` | `Dictionary<string, object>`  | `new Dictionary<>()`       | Allows capturing and rendering additional HTML attributes on the root element.                 |
| `Id`             | `string?`                     | `null`                     | Custom `id` attribute for the root element. If `null`, a unique ID (`UniqueId`) is generated. |
| `IsEnabled`      | `bool`                        | `true`                     | If false, the tooltip might not appear (behavior depends on specific triggers).                |
| `Style`          | `string?`                     | `null`                     | Custom inline CSS style(s) for the root element of the tooltip component structure.            |
| `Visibility`     | `BitVisibility`               | `BitVisibility.Visible`    | Controls the component's root element visibility. `IsShown` controls the tooltip popup itself. |

### Public Members (`BitComponentBase`)

These are public properties available on the component instance.

| Name          | Type               | Default Value    | Description                                                                           |
| :------------ | :----------------- | :--------------- | :------------------------------------------------------------------------------------ |
| `UniqueId`    | `string`           | `Guid.NewGuid()` | Readonly unique identifier generated for the component instance. Used if `Id` is null. |
| `RootElement` | `ElementReference` |                  | A reference to the root HTML element of the component (available after rendering).      |

### Supporting Classes and Enums

#### `BitTooltipClassStyles` Class

Used for the `Classes` and `Styles` parameters.

| Property       | Type      | Description                                                    |
| :------------- | :-------- | :------------------------------------------------------------- |
| `Root`         | `string?` | CSS class(es) or style(s) for the root container element.      |
| `TooltipWrapper`| `string?` | CSS class(es) or style(s) for the wrapper around the tooltip popup. |
| `Tooltip`      | `string?` | CSS class(es) or style(s) for the main tooltip popup container.  |
| `Arrow`        | `string?` | CSS class(es) or style(s) for the tooltip's pointer arrow.     |

#### `BitTooltipPosition` Enum

Used for the `Position` parameter.

| Name          | Value | Description                              |
| :------------ | :---- | :--------------------------------------- |
| `Top`         | `0`   | Above the anchor, centered.              |
| `TopLeft`     | `1`   | Above the anchor, aligned left.          |
| `TopRight`    | `2`   | Above the anchor, aligned right.         |
| `RightTop`    | `3`   | Right of the anchor, aligned top.        |
| `Right`       | `4`   | Right of the anchor, centered.           |
| `RightBottom` | `5`   | Right of the anchor, aligned bottom.     |
| `BottomRight` | `6`   | Below the anchor, aligned right.         |
| `Bottom`      | `7`   | Below the anchor, centered.              |
| `BottomLeft`  | `8`   | Below the anchor, aligned left.          |
| `LeftBottom`  | `9`   | Left of the anchor, aligned bottom.      |
| `Left`        | `10`  | Left of the anchor, centered.            |
| `LeftTop`     | `11`  | Left of the anchor, aligned top.         |

#### `BitVisibility` Enum

Used for the inherited `Visibility` parameter.

| Name        | Value | Description                                                        |
| :---------- | :---- | :----------------------------------------------------------------- |
| `Visible`   | `0`   | Component is visible (default).                                    |
| `Hidden`    | `1`   | Component is hidden (`visibility: hidden;`), still occupies space. |
| `Collapsed` | `2`   | Component is hidden (`display: none;`), does not occupy space.     |

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

1.  **Standard Header:** Includes the component name (`BitTooltip`) and the purpose statement for the AI agent.
2.  **Overview:** Briefly summarizes the component's function based on the source HTML description.
3.  **Usage Examples:**
    *   Each example from the HTML (`Basic`, `Position`, `Custom content`, `Advanced`, `Styles & Classes`, `RTL`) gets its own subsection (`###`).
    *   A short explanation introduces the feature demonstrated.
    *   `cshtml` and `csharp` code blocks are provided, extracted directly from the source, with minor cleanup/additions (like adding `ShowOnFocus`/`ShowDelay` to the advanced example for completeness based on API parameters).
    *   Key parameters (`Text`, `Position`, `Template`, `Anchor`, `@bind-IsShown`, `HideDelay`, `ShowOnClick`, `Styles`, `Classes`, `Dir`) are highlighted either in the explanation or within the code itself.
    *   Notes clarify concepts like the default anchor, the precedence of `Template` over `Text`, and the complexity of arrow styling.
4.  **API Reference:**
    *   Sections for `BitTooltip` parameters, inherited `BitComponentBase` parameters, and public members use Markdown tables for structured data.
    *   Parameter details (Name, Type, Default Value, Description) are meticulously copied from the HTML API tables. Types like `RenderFragment?`, `BitTooltipPosition`, `EventCallback<bool>`, and `BitTooltipClassStyles?` are correctly represented.
    *   Default values are clearly stated.
5.  **Supporting Classes and Enums:**
    *   Detailed breakdowns of the `BitTooltipClassStyles` class properties and the `BitTooltipPosition`, `BitVisibility`, and `BitDir` enums are provided using tables, ensuring the AI understands the structure and possible values for complex parameters.
6.  **Formatting:** Consistent use of Markdown headings, code blocks (with language identifiers), tables, and backticks enhances readability and parseability for the AI.

This comprehensive structure ensures the AI agent has access to typical usage patterns, advanced configurations, styling options, and the complete API definition, enabling it to generate helpful and accurate code suggestions for the `BitTooltip` component.
