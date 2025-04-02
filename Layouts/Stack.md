# BitStack Component Reference (Blazor UI)

## Overview

`BitStack` is a versatile container component in the Blazor UI library that simplifies the implementation of one-dimensional layouts using CSS Flexbox. It allows developers to easily arrange child elements (components or HTML tags) either vertically (default) or horizontally, control spacing, alignment, wrapping, and growth behavior without needing to write complex CSS flexbox rules directly.

It essentially acts as a configurable flex container (`display: flex`). The component documentation also mentions `WrapPanel`, likely referring to the wrapping capabilities provided by the `Wrap` parameter.

**Use Cases:**

*   Arranging items in a toolbar or header (horizontally).
*   Creating lists or menus (vertically).
*   Laying out form fields and labels.
*   Displaying sequences of cards or profiles.
*   Building button groups.
*   Creating responsive layouts that adjust flow direction or wrapping.
*   Implementing complex nested layouts by combining multiple `BitStack` components.

## Key Concepts

*   **Flexbox Abstraction:** `BitStack` hides the direct CSS (`display: flex`, `flex-direction`, `justify-content`, `align-items`, `gap`, `flex-wrap`, `flex-grow`) behind intuitive Blazor parameters.
*   **Direction:** Controls whether items stack vertically (`flex-direction: column` - default) or horizontally (`flex-direction: row` via the `Horizontal` parameter). The `Reversed` parameter can invert the stacking order (`column-reverse` or `row-reverse`).
*   **Spacing (`Gap`):** Defines the space between adjacent child items using the CSS `gap` property. It accepts standard CSS size values (e.g., `"1rem"`, `"10px"`). You can specify one value for both row and column gaps, or two values (`"row-gap column-gap"`).
*   **Alignment (Main Axis):** The `HorizontalAlign` parameter controls alignment along the main axis (`justify-content`). For a horizontal stack, this is horizontal alignment; for a vertical stack, it's vertical alignment. Uses the `BitAlignment` enum.
*   **Alignment (Cross Axis):** The `VerticalAlign` parameter controls alignment along the cross axis (`align-items`). For a horizontal stack, this is vertical alignment; for a vertical stack, it's horizontal alignment. Uses the `BitAlignment` enum.
*   **Wrapping (`Wrap`):** If set to `true`, child items that exceed the container's bounds along the main axis will wrap onto the next line (`flex-wrap: wrap`).
*   **Growth (`Grow`, `Grows`):** Controls how a `BitStack` itself (when nested) or its children (if applied directly, though typically done on children) expand to fill available space using `flex-grow`.
    *   `Grows` (boolean): Sets `flex-grow: 1`.
    *   `Grow` (string/number): Sets a specific `flex-grow` value, allowing for proportional growth relative to siblings.
*   **Sizing (`Auto*`, `Fit*`):** Parameters like `AutoHeight`, `AutoWidth`, `AutoSize`, `FitHeight`, `FitWidth`, `FitSize` influence the stack's own dimensions, often setting width/height to `auto` or `fit-content`.

## Usage

### Basic Stacking (Vertical, Horizontal, Reversed)

Demonstrates default vertical stacking, horizontal stacking, and reversing the order.

**CSHTML:**

```csharp
<style>
    .basic-stack div { /* Simple styling for items */
        padding: 0.5rem;
        background-color: #71afe5; /* Stack background */
        color: black;
        border: 1px solid #333;
        text-align: center;
    }
    .basic-stack { /* Add margin between stacks */
        margin-bottom: 1rem; 
    }
</style>

<div>Default (Vertical):</div>
<BitStack Class="basic-stack">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</BitStack>

<div>Horizontal:</div>
<BitStack Horizontal Class="basic-stack">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</BitStack>

<div>Reversed Vertical:</div>
<BitStack Reversed Class="basic-stack">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</BitStack>

<div>Reversed Horizontal:</div>
<BitStack Horizontal Reversed Class="basic-stack">
    <div>Item 1</div>
    <div>Item 2</div>
    <div>Item 3</div>
</BitStack>
```

**Explanation:**

* The first `BitStack` defaults to vertical (`flex-direction: column`).
* The second uses `Horizontal` for horizontal layout (`flex-direction: row`).
* The third uses `Reversed` for reversed vertical layout (`flex-direction: column-reverse`).
* The fourth uses both `Horizontal` and `Reversed` (`flex-direction: row-reverse`).

### Using Gap for Spacing

Control the space between items using the `Gap` parameter.

**CSHTML:**

```csharp
<style>
    .gap-item {
        color: white;
        padding: 0.5rem;
        background-color: #0078d4;
        text-align: center;
    }
</style>

<BitSlider Label="Gap (rem)" Min="0" Max="5" Step="0.1" @bind-Value="gapValue" ValueFormat="0.0 rem" />
<br/>

<BitStack Gap="@($"{gapValue}rem")" Style="background:#eee; padding: 5px;">
    <div class="gap-item">Item 1</div>
    <div class="gap-item">Item 2</div>
    <div class="gap-item">Item 3</div>
</BitStack>
<br/>
<BitStack Horizontal Gap="@($"{gapValue}rem")" Style="background:#eee; padding: 5px;">
    <div class="gap-item">Item A</div>
    <div class="gap-item">Item B</div>
    <div class="gap-item">Item C</div>
</BitStack>

@code {
    private double gapValue = 1.0;
}
```

**Explanation:**

* The `Gap` parameter is dynamically set using the `BitSlider`.
* It accepts any valid CSS `gap` value (e.g., `"1rem"`, `"10px"`).
* The spacing is applied between items in both vertical and horizontal stacks.

### Nesting Stacks

`BitStack` components can be nested to create more complex layouts.

**CSHTML:**

```csharp
<style>
    .nest-item { color: white; padding: 0.5rem; background-color: #0078d4; border: 1px solid #005a9e; text-align: center;}
    .outer-stack { background: #71afe5; padding: 10px; }
    .inner-stack-v { background: #a1cafe; padding: 5px; }
    .inner-stack-h { background: #a1cafe; padding: 5px; }
</style>

<BitStack Horizontal HorizontalAlign="BitAlignment.SpaceAround" Class="outer-stack">
    <div class="nest-item">Outer 1</div>
    
    @* Nested Vertical Stack *@
    <BitStack Class="inner-stack-v">
        <div class="nest-item">Nested V 2-1</div>
        <div class="nest-item">Nested V 2-2</div>
    </BitStack>

    @* Nested Horizontal Stack *@
    <BitStack Horizontal Class="inner-stack-h">
        <div class="nest-item">Nested H 3-1</div>
        <div class="nest-item">Nested H 3-2</div>
    </BitStack>

     <div class="nest-item">Outer 4</div>
</BitStack>
```

**Explanation:**

* An outer horizontal `BitStack` contains regular items and two nested `BitStack`s (one vertical, one horizontal).
* Alignment and gap properties apply independently at each level of nesting.

### Alignment (Horizontal and Vertical)

Use `HorizontalAlign` and `VerticalAlign` to control item positioning within the stack.

**CSHTML:**

```csharp
<style>
    .align-item { color: white; padding: 0.5rem 1rem; background-color: #0078d4; }
    .align-stack { background: #71afe5; min-height: 10rem; border: 1px solid #005a9e; margin-bottom: 1rem; }
</style>

@* Controls - Select Alignment Values *@
<BitChoiceGroup @bind-Value="hAlign" Horizontal Label="Horizontal Align" TItem="BitChoiceGroupOption<BitAlignment>" TValue="BitAlignment">
    <BitChoiceGroupOption Text="Start" Value="BitAlignment.Start" />
    <BitChoiceGroupOption Text="Center" Value="BitAlignment.Center" />
    <BitChoiceGroupOption Text="End" Value="BitAlignment.End" />
    <BitChoiceGroupOption Text="SpaceBetween" Value="BitAlignment.SpaceBetween" />
    <BitChoiceGroupOption Text="SpaceAround" Value="BitAlignment.SpaceAround" />
    <BitChoiceGroupOption Text="SpaceEvenly" Value="BitAlignment.SpaceEvenly" />
</BitChoiceGroup>
<BitChoiceGroup @bind-Value="vAlign" Horizontal Label="Vertical Align" TItem="BitChoiceGroupOption<BitAlignment>" TValue="BitAlignment">
    <BitChoiceGroupOption Text="Start" Value="BitAlignment.Start" />
    <BitChoiceGroupOption Text="Center" Value="BitAlignment.Center" />
    <BitChoiceGroupOption Text="End" Value="BitAlignment.End" />
    <BitChoiceGroupOption Text="Stretch" Value="BitAlignment.Stretch" />
    <BitChoiceGroupOption Text="Baseline" Value="BitAlignment.Baseline" />
</BitChoiceGroup>
<br/>

<div>Horizontal Stack Alignment:</div>
<BitStack Horizontal 
          HorizontalAlign="hAlign" 
          VerticalAlign="vAlign" 
          Class="align-stack">
    <div class="align-item">Item 1</div>
    <div class="align-item" style="padding-bottom: 2rem;">Item 2<br/>(Taller)</div> @* Taller item to show vertical alignment *@
    <div class="align-item">Item 3</div>
</BitStack>

<div>Vertical Stack Alignment:</div>
<BitStack VerticalAlign="vAlign" 
          HorizontalAlign="hAlign" 
          Class="align-stack">
    <div class="align-item">Item A</div>
    <div class="align-item" style="padding-right: 2rem;">Item B (Wider)</div> @* Wider item to show horizontal alignment *@
    <div class="align-item">Item C</div>
</BitStack>

@code {
    private BitAlignment hAlign = BitAlignment.Start;
    private BitAlignment vAlign = BitAlignment.Start;
}
```

**Explanation:**

* `HorizontalAlign` corresponds to `justify-content` (main axis alignment).
* `VerticalAlign` corresponds to `align-items` (cross axis alignment).
* Their effect depends on whether the stack is `Horizontal` or vertical (default). The examples show both scenarios.

### Wrapping Items

Use the `Wrap` parameter to allow items to flow onto multiple lines if they don't fit.

**CSHTML:**

```csharp
<style>
    .wrap-item {
        display: flex;
        width: 5rem; /* Fixed width to force wrapping */
        height: 3rem;
        align-items: center;
        justify-content: center;
        background-color: dodgerblue;
        color: white;
        border: 1px solid navy;
    }
    .wrap-stack { background: #71afe5; padding: 0.5rem; border: 1px solid #005a9e; }
</style>

<BitStack Horizontal Wrap Gap="0.5rem" Class="wrap-stack">
    @for (int i = 1; i <= 15; i++)
    {
        <div class="wrap-item">Item @i</div>
    }
</BitStack>
```

**Explanation:**

* `Horizontal` makes the stack flow left-to-right.
* `Wrap` enables `flex-wrap: wrap`.
* Since items have a fixed `width` and the container width is limited, items wrap to the next line. `Gap` applies spacing in both dimensions when wrapping.

### Item Growth (`Grow` / `Grows`)

Control how nested `BitStack` components expand to fill the space in their parent stack.

**CSHTML:**

```csharp
<style>
    .grow-item {
        color: white;
        padding: 0.5rem;
        background-color: #0078d4;
        border: 1px solid navy;
        display: flex; /* Needed for alignment within the item */
        align-items: center;
        justify-content: center;
    }
    .grow-stack { background:#71afe5; height:15rem; margin-bottom: 1rem; }
</style>

<div>Using Grow (Proportional):</div>
<BitStack Gap="0.5rem" Class="grow-stack">
    <BitStack Grow="3" AutoHeight Class="grow-item">Grow = 3</BitStack> @* Takes 3 parts of available space *@
    <BitStack Grow="2" AutoHeight Class="grow-item">Grow = 2</BitStack> @* Takes 2 parts of available space *@
    <BitStack Grow="1" AutoHeight Class="grow-item">Grow = 1</BitStack> @* Takes 1 part of available space *@
</BitStack>

<div>Using Grows (Boolean):</div>
<BitStack Gap="0.5rem" Class="grow-stack">
    <BitStack AutoHeight Class="grow-item">Normal</BitStack>
    <BitStack Grows AutoHeight Class="grow-item">Grows (flex-grow: 1)</BitStack> @* Takes available space *@
    <BitStack AutoHeight Class="grow-item">Normal</BitStack>
</BitStack>

<div>Using Grows (Horizontal):</div>
<BitStack Horizontal Gap="0.5rem" Class="grow-stack">
    <BitStack AutoWidth Class="grow-item">Normal</BitStack>
    <BitStack Grows AutoWidth Class="grow-item">Grows (flex-grow: 1)</BitStack> @* Takes available space *@
    <BitStack AutoWidth Class="grow-item">Normal</BitStack>
</BitStack>

```

**Explanation:**

* **`Grow="value"`:** Nested stacks use `Grow` with a number to specify their growth factor relative to siblings. The available space is divided proportionally. `AutoHeight` is used so the stack fills the allocated vertical space.
* **`Grows`:** A boolean shorthand for `Grow="1"`. The nested stack with `Grows` expands to fill the available space not taken by non-growing siblings. `AutoHeight` (or `AutoWidth` for horizontal) allows the stack to fill the grown space.

## API Reference

### `BitStack` Parameters

| Parameter         | Type            | Default Value      | Description                                                                                                                                              | CSS Equivalent        |
| ----------------- | --------------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| `ChildContent`    | `RenderFragment?` | `null`             | The content (items) to be rendered inside the stack.                                                                                                     |                       |
| `Horizontal`      | `bool`          | `false`            | If `true`, stack children horizontally (`row`). If `false` (default), stack vertically (`column`).                                                       | `flex-direction`      |
| `Reversed`        | `bool`          | `false`            | If `true`, reverses the direction of stacking (`column-reverse` or `row-reverse`).                                                                       | `flex-direction`      |
| `Gap`             | `string?`       | `null` (effectively `1rem` based on examples?) | Defines spacing between children. Accepts CSS `gap` values (e.g., `"1rem"`, `"10px"`, `"1rem 0.5rem"`).                                         | `gap`                 |
| `HorizontalAlign` | `BitAlignment?` | `null` (effectively `Start`) | Aligns children along the main axis (Horizontally for `Horizontal` stack, Vertically for vertical stack). See `BitAlignment` enum.              | `justify-content`     |
| `VerticalAlign`   | `BitAlignment?` | `null` (effectively `Start`) | Aligns children along the cross axis (Vertically for `Horizontal` stack, Horizontally for vertical stack). See `BitAlignment` enum.                 | `align-items`         |
| `Alignment`       | `BitAlignment?` | `null`             | **Deprecated/Ambiguous:** Use `HorizontalAlign` and `VerticalAlign` instead for clarity. Seems to set both `justify-content` and `align-items`.        | `justify-content`, `align-items` |
| `Wrap`            | `bool`          | `false`            | If `true`, allows children to wrap onto multiple lines/columns if they overflow.                                                                         | `flex-wrap: wrap`     |
| `Grow`            | `string?`       | `null`             | Sets the `flex-grow` factor for the stack itself (when nested). Allows proportional sizing relative to siblings.                                         | `flex-grow`           |
| `Grows`           | `bool`          | `false`            | Shorthand for `Grow="1"`. Makes the stack grow to fill available space relative to non-growing siblings.                                                   | `flex-grow: 1`        |
| `FillContent`     | `bool`          | `false`            | **Potentially affects children:** May make direct children stretch to fill the cross-axis (similar to `align-items: stretch` on parent?). Requires testing. | `align-items: stretch`?|
| `AutoHeight`      | `bool`          | `false`            | Sets the stack's `height` to `auto`. Useful with `Grow`/`Grows` in a vertical parent stack.                                                              | `height: auto`        |
| `AutoWidth`       | `bool`          | `false`            | Sets the stack's `width` to `auto`. Useful with `Grow`/`Grows` in a horizontal parent stack.                                                             | `width: auto`         |
| `AutoSize`        | `bool`          | `false`            | Sets both `width` and `height` to `auto`.                                                                                                                | `width: auto`, `height: auto` |
| `FitHeight`       | `bool`          | `false`            | Sets the stack's `height` possibly to `fit-content`. Exact behavior might need verification.                                                             | `height: fit-content`?|
| `FitWidth`        | `bool`          | `false`            | Sets the stack's `width` possibly to `fit-content`. Exact behavior might need verification.                                                              | `width: fit-content`? |
| `FitSize`         | `bool`          | `false`            | Sets both `width` and `height` possibly to `fit-content`. Exact behavior might need verification.                                                        | `width: fit-content`, `height: fit-content`? |
| `Element`         | `string?`       | `null` (renders `div`) | Specifies the HTML tag for the root element (e.g., `"section"`, `"nav"`). Defaults to `div`.                                                           |                       |
| *(Inherited)*     |                 |                    | Inherits parameters from `BitComponentBase` (see below).                                                                                                 |                       |

### Inherited Parameters (from `BitComponentBase`)

| Parameter        | Type                           | Default Value                       | Description                                                                                             |
| ---------------- | ------------------------------ | ----------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                      | `null`                              | The `aria-label` attribute for the root element, improving accessibility, especially if used semantically. |
| `Class`          | `string?`                      | `null`                              | Custom CSS class(es) to apply to the root element.                                                      |
| `Dir`            | `BitDir?`                      | `null`                              | Specifies the text direction (`Ltr`, `Rtl`, `Auto`). Influences layout in `Rtl` mode.                     |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<string, object>()`  | Allows capturing and rendering additional HTML attributes on the root element.                          |
| `Id`             | `string?`                      | `null`                              | Sets a custom `id` attribute for the root element.                                                      |
| `IsEnabled`      | `bool`                         | `true`                              | Whether the component appears enabled visually.                                                           |
| `Style`          | `string?`                      | `null`                              | Custom inline CSS styles to apply to the root element.                                                  |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`             | Controls the visibility of the entire `BitStack` component (`Visible`, `Hidden`, `Collapsed`).            |

### Public Members (from `BitComponentBase`)

| Member        | Type               | Default Value      | Description                                                                                                |
| ------------- | ------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()`   | A read-only unique identifier (`Guid`) generated for each component instance.                              |
| `RootElement` | `ElementReference` | *(N/A)*            | An `ElementReference` pointing to the root DOM element (default `div`) of the component. Useful for JS interop. |

## Related Enums

### `BitAlignment` Enum

Used for `HorizontalAlign` and `VerticalAlign`. Corresponds to CSS `justify-content` (main axis) and `align-items` (cross axis) values.

| Name          | Value | Description                                                                                    | CSS `justify-content` / `align-items` Equivalent |
| ------------- | ----- | ---------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| `Start`       | `0`   | Items align to the start of the container.                                                     | `flex-start`                                      |
| `End`         | `1`   | Items align to the end of the container.                                                       | `flex-end`                                        |
| `Center`      | `2`   | Items align to the center of the container.                                                    | `center`                                          |
| `SpaceBetween`| `3`   | (Main Axis Only) Items align with equal space between them; first/last items touch container edges. | `space-between`                                   |
| `SpaceAround` | `4`   | (Main Axis Only) Items align with equal space around them (half-space at ends).                  | `space-around`                                    |
| `SpaceEvenly` | `5`   | (Main Axis Only) Items align with equal space between them and at the ends.                      | `space-evenly`                                    |
| `Baseline`    | `6`   | (Cross Axis Only) Items align based on their text baseline.                                    | `baseline`                                        |
| `Stretch`     | `7`   | (Cross Axis Only - Default for `align-items`) Items stretch to fill the container's cross dimension. | `stretch`                                         |

### `BitVisibility` Enum

Defines how the component is displayed.

| Name        | Value | Description                                                                                    | CSS Equivalent         |
| ----------- | ----- | ---------------------------------------------------------------------------------------------- | ---------------------- |
| `Visible`   | `0`   | The component is rendered and visible.                                                         | `visibility: visible;` |
| `Hidden`    | `1`   | The component is hidden, but it still occupies space in the layout.                            | `visibility: hidden;`  |
| `Collapsed` | `2`   | The component is hidden and does not occupy any space in the layout (removed from flow).       | `display: none;`       |

### `BitDir` Enum

Defines the text directionality.

| Name   | Value | Description                                                                                                                                                   | HTML `dir` Attribute |
| ------ | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| `Ltr`  | `0`   | Left-to-right text direction (e.g., English).                                                                                                                 | `ltr`                |
| `Rtl`  | `1`   | Right-to-left text direction (e.g., Arabic, Hebrew).                                                                                                          | `rtl`                |
| `Auto` | `2`   | The browser determines the direction based on the content.                                                                                                    | `auto`               |

## Feedback

* Provide feedback via [GitHub Issues](https://github.com/bitfoundation/bitplatform/issues/new/choose).
* Start a discussion on [GitHub Discussions](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
* Review/Edit the [Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Layouts/Stack/BitStackDemo.razor).
* Review/Edit the [Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Layouts/Stack/BitStack.cs).
