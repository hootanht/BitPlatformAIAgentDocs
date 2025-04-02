# BitGrid & BitGridItem Component Reference (Blazor UI)

## Overview

`BitGrid` is a powerful and flexible layout component for creating responsive grid structures in Blazor applications. It works in conjunction with the `BitGridItem` component to arrange content into rows and columns. Key features include customizable column counts, item spanning, horizontal alignment, spacing control, and built-in responsive breakpoints.

**Use Cases:**

*   Creating page layouts with distinct sections (e.g., sidebars, main content).
*   Arranging cards, images, or data points in a structured, multi-column format.
*   Building forms with aligned input fields and labels.
*   Designing dashboards with multiple widgets.
*   Implementing responsive layouts that adapt to different screen sizes.

## Key Concepts

*   **Container (`BitGrid`):** Defines the overall grid structure, including the total number of columns available, default spacing, and alignment of items within the grid.
*   **Item (`BitGridItem`):** Represents an individual cell within the `BitGrid`. It defines how many columns it should span.
*   **Columns:** The `BitGrid` is divided into a specific number of virtual columns (default is 12). `BitGridItem` components specify how many of these columns they occupy using `ColumnSpan`.
*   **Responsiveness (Breakpoints):** Both `BitGrid` (for total columns) and `BitGridItem` (for item span) support parameters (`Xs`, `Sm`, `Md`, `Lg`, `Xl`, `Xxl`) to adjust their behavior based on screen width. This allows layouts to adapt seamlessly to different devices.
*   **Spacing:** Control the gap between grid items using `Spacing`, `HorizontalSpacing`, and `VerticalSpacing` properties on the `BitGrid`.
*   **Alignment:** Align items horizontally within the `BitGrid` container using the `HorizontalAlign` property.

## Usage

### Basic Grid

Define a `BitGrid` with a specific number of `Columns` and place `BitGridItem` components inside it. Items will automatically wrap to the next row based on the available columns.

**CSHTML:**

```csharp
<style>
    /* Basic styling for visual clarity */
    .grid-item-basic {
        height: 75px;
        padding: 8px;
        text-align: center;
        border-radius: 2px;
        display: flex; /* Use flex to center content vertically */
        align-items: center;
        justify-content: center;
        border: 1px solid lightgray;
        background-color: #f0f0f0;
        min-width: 50px; /* Prevent excessive shrinking */
    }
</style>

<BitGrid Columns="4">
    @for (int i = 0; i < 8; i++)
    {
        var item = i + 1;
        <BitGridItem Class="grid-item-basic">
            Item @item
        </BitGridItem>
    }
</BitGrid>
```

**Explanation:**

* `BitGrid Columns="4"`: Creates a grid container divided into 4 columns per row.
* `BitGridItem`: Each item implicitly spans 1 column (`ColumnSpan` defaults to 1).
* Since there are 8 items and 4 columns, the items will form a 2x4 grid.
* The `.grid-item-basic` CSS provides visual styling.

### Column Spanning

Use the `ColumnSpan` parameter on `BitGridItem` to make an item occupy more than one column.

**CSHTML:**

```csharp
<style>
    .grid-item-span { height: 75px; padding: 8px; text-align: center; border-radius: 2px; display: flex; align-items: center; justify-content: center; border: 1px solid lightgray; background-color: #e0e8f0; min-width: 50px; }
</style>

<BitGrid Columns="4">
    <BitGridItem Class="grid-item-span" ColumnSpan="4">
        Span 4 (Full Width)
    </BitGridItem>
    <BitGridItem Class="grid-item-span" ColumnSpan="2">
        Span 2
    </BitGridItem>
    <BitGridItem Class="grid-item-span" ColumnSpan="2">
        Span 2
    </BitGridItem>
    <BitGridItem Class="grid-item-span"> <!-- Span 1 (default) -->
        Span 1
    </BitGridItem>
    <BitGridItem Class="grid-item-span"> <!-- Span 1 (default) -->
        Span 1
    </BitGridItem>
    <BitGridItem Class="grid-item-span"> <!-- Span 1 (default) -->
        Span 1
    </BitGridItem>
    <BitGridItem Class="grid-item-span"> <!-- Span 1 (default) -->
        Span 1
    </BitGridItem>
</BitGrid>
```

**Explanation:**

* The first item spans all 4 columns.
* The next two items each span 2 columns, filling the second row.
* The remaining items default to `ColumnSpan="1"`, filling the third row.

### Alignment

Control the horizontal distribution of items within a row using the `HorizontalAlign` parameter on `BitGrid`. This uses the `BitAlignment` enum, corresponding to CSS `justify-content` values.

**CSHTML:**

```csharp
<style>
    .grid-item-align { height: 75px; padding: 8px; text-align: center; border-radius: 2px; display: flex; align-items: center; justify-content: center; border: 1px solid lightgray; background-color: #e0f0e8; min-width: 50px; }
</style>

@* --- Example Control --- *@
<BitChoiceGroup @bind-Value="selectedAlignment" Horizontal Label="Horizontal Align" TItem="BitChoiceGroupOption<BitAlignment>" TValue="BitAlignment">
    <BitChoiceGroupOption Text="Start" Value="BitAlignment.Start" />
    <BitChoiceGroupOption Text="Center" Value="BitAlignment.Center" />
    <BitChoiceGroupOption Text="End" Value="BitAlignment.End" />
    <BitChoiceGroupOption Text="SpaceBetween" Value="BitAlignment.SpaceBetween" />
    <BitChoiceGroupOption Text="SpaceAround" Value="BitAlignment.SpaceAround" />
    <BitChoiceGroupOption Text="SpaceEvenly" Value="BitAlignment.SpaceEvenly" />
    @* Baseline and Stretch might have less visual effect here without specific item content/heights *@
    @*<BitChoiceGroupOption Text="Baseline" Value="BitAlignment.Baseline" />*@
    @*<BitChoiceGroupOption Text="Stretch" Value="BitAlignment.Stretch" />*@
</BitChoiceGroup>
<br />

@* --- Grid --- *@
<BitGrid Columns="5" HorizontalAlign="selectedAlignment"> @* Use 5 columns to better see alignment effects *@
    @for (int i = 0; i < 3; i++) @* Only 3 items to show spacing/alignment *@
    {
        var item = i + 1;
        <BitGridItem Class="grid-item-align">
            Item @item
        </BitGridItem>
    }
</BitGrid>

@code {
    private BitAlignment selectedAlignment = BitAlignment.Start; // Default
}
```

**Explanation:**

* A `BitChoiceGroup` allows selecting a `BitAlignment` value.
* The `BitGrid`'s `HorizontalAlign` is bound to the `selectedAlignment` variable.
* Changing the selection in the `BitChoiceGroup` updates the grid's alignment (e.g., `Center` centers the 3 items within the 5-column space, `SpaceBetween` puts space between them).

### Spacing

Control the gaps between grid items. `Spacing` sets both horizontal and vertical gaps. `HorizontalSpacing` and `VerticalSpacing` allow setting them independently (they override `Spacing` if provided). Values should be valid CSS size strings (e.g., `"1rem"`, `"10px"`).

**CSHTML:**

```csharp
<style>
    .grid-item-space { height: 75px; padding: 8px; text-align: center; border-radius: 2px; display: flex; align-items: center; justify-content: center; border: 1px solid lightgray; background-color: #f0e8e0; min-width: 50px; }
</style>

@* --- Example Controls --- *@
<BitSlider Label="Vertical spacing" Max="3" ValueFormat="0.0 rem" Step="0.1" @bind-Value="vSpacing" />
<BitSlider Label="Horizontal spacing" Max="3" ValueFormat="0.0 rem" Step="0.1" @bind-Value="hSpacing" />
<br />

@* --- Grid --- *@
<BitGrid Columns="4"
         VerticalSpacing="@($"{vSpacing}rem")"
         HorizontalSpacing="@($"{hSpacing}rem")">
    @for (int i = 0; i < 8; i++)
    {
        var item = i + 1;
        <BitGridItem Class="grid-item-space">
            Item @item
        </BitGridItem>
    }
</BitGrid>

@code {
    private double vSpacing = 0.5;
    private double hSpacing = 0.5;
}
```

**Explanation:**

* `BitSlider` controls update `vSpacing` and `hSpacing` variables.
* `BitGrid`'s `VerticalSpacing` and `HorizontalSpacing` parameters are set using string interpolation to include the unit (`rem`).
* Changing the sliders dynamically adjusts the gaps between grid items.

### Responsive Breakpoints

Make the grid layout adapt to different screen sizes using breakpoint parameters. These can be applied to both the `BitGrid` (to change the total number of columns) and `BitGridItem` (to change how many columns an item spans).

**Breakpoints:** `Xs` (Extra Small), `Sm` (Small), `Md` (Medium), `Lg` (Large), `Xl` (Extra Large), `Xxl` (Extra Extra Large).

**CSHTML:**

```csharp
<style>
    .grid-item-resp { height: 75px; padding: 8px; text-align: center; border-radius: 2px; display: flex; align-items: center; justify-content: center; border: 1px solid lightgray; background-color: #e8e0f0; min-width: 50px; }
</style>

<h4>Grid Item Breakpoints:</h4>
<BitGrid Columns="12"> @* Use a 12-column base for flexibility *@
    <BitGridItem Class="grid-item-resp" Xs="12" Sm="6" Md="4" Lg="3">
        Item 1 (Xs=12, Sm=6, Md=4, Lg=3)
    </BitGridItem>
    <BitGridItem Class="grid-item-resp" Xs="6" Sm="6" Md="4" Lg="3">
        Item 2 (Xs=6, Sm=6, Md=4, Lg=3)
    </BitGridItem>
    <BitGridItem Class="grid-item-resp" Xs="6" Sm="6" Md="4" Lg="3">
        Item 3 (Xs=6, Sm=6, Md=4, Lg=3)
    </BitGridItem>
     <BitGridItem Class="grid-item-resp" Xs="12" Sm="12" Md="12" Lg="3">
        Item 4 (Xs=12, Sm=12, Md=12, Lg=3)
    </BitGridItem>
</BitGrid>

<br/>

<h4>Grid Container Breakpoints:</h4>
<BitGrid Columns="6"    @* Default columns (Large screens and up) *@
         ColumnsLg="5"
         ColumnsMd="4"
         ColumnsSm="3"
         ColumnsXs="2">
    @for (int i = 0; i < 10; i++) @* More items to show wrapping *@
    {
        var item = i + 1;
        <BitGridItem Class="grid-item-resp">
            Item @item
        </BitGridItem>
    }
</BitGrid>
```

**Explanation:**

1. **Grid Item Breakpoints:**
    * The first `BitGrid` has a fixed 12 columns.
    * `BitGridItem` components use `Xs`, `Sm`, `Md`, `Lg` to define their `ColumnSpan` at different screen sizes. For example, Item 1 takes the full width (`12`) on extra-small screens, half width (`6`) on small, a third (`4`) on medium, and a quarter (`3`) on large screens.
2. **Grid Container Breakpoints:**
    * The second `BitGrid` changes its *total* number of columns based on the screen size using `ColumnsXs`, `ColumnsSm`, etc.
    * It has 2 columns on extra-small, 3 on small, 4 on medium, 5 on large, and defaults to 6 on extra-large and above. The items inside simply take up 1 column each (default span) relative to the *current total* number of columns.

## API Reference

### `BitGrid` Parameters

| Parameter           | Type                  | Default Value      | Description                                                            |
| ------------------- | --------------------- | ------------------ | ---------------------------------------------------------------------- |
| `ChildContent`      | `RenderFragment?`     | `null`             | The content of the Grid, typically `BitGridItem` components.           |
| `Columns`           | `int`                 | `12`               | Default number of columns the grid is divided into.                    |
| `ColumnsXs`         | `int?`                | `null`             | Number of columns at the extra-small breakpoint. Overrides `Columns`.  |
| `ColumnsSm`         | `int?`                | `null`             | Number of columns at the small breakpoint. Overrides `Columns`.      |
| `ColumnsMd`         | `int?`                | `null`             | Number of columns at the medium breakpoint. Overrides `Columns`.     |
| `ColumnsLg`         | `int?`                | `null`             | Number of columns at the large breakpoint. Overrides `Columns`.      |
| `ColumnsXl`         | `int?`                | `null`             | Number of columns at the extra-large breakpoint. Overrides `Columns`.  |
| `ColumnsXxl`        | `int?`                | `null`             | Number of columns at the extra-extra-large breakpoint. Overrides `Columns`. |
| `HorizontalAlign`   | `BitAlignment`        | `BitAlignment.Start` | Defines the horizontal alignment of items within the grid (like CSS `justify-content`). |
| `Spacing`           | `string`              | `"4px"`            | Default spacing (both horizontal and vertical) between grid items. Valid CSS size (e.g., "1rem", "8px"). |
| `HorizontalSpacing` | `string?`             | `null`             | Specific horizontal spacing between items. Overrides `Spacing`. Valid CSS size. |
| `VerticalSpacing`   | `string?`             | `null`             | Specific vertical spacing between items. Overrides `Spacing`. Valid CSS size. |
| `Span` *(`Obsolete?`)*| `int`                 | `1`                | *Seems less relevant for the container; likely related to older/internal implementation. Focus on `Columns`.* |
| *(Inherited)*       |                       |                    | Inherits parameters from `BitComponentBase` (see below).                 |

### `BitGridItem` Parameters

| Parameter     | Type              | Default Value | Description                                                               |
| ------------- | ----------------- | ------------- | ------------------------------------------------------------------------- |
| `ChildContent`| `RenderFragment?` | `null`        | The content displayed within the grid item.                               |
| `ColumnSpan`  | `int`             | `1`           | Default number of columns this item should span.                          |
| `Xs`          | `int?`            | `null`        | Number of columns to span at the extra-small breakpoint. Overrides `ColumnSpan`. |
| `Sm`          | `int?`            | `null`        | Number of columns to span at the small breakpoint. Overrides `ColumnSpan`. |
| `Md`          | `int?`            | `null`        | Number of columns to span at the medium breakpoint. Overrides `ColumnSpan`. |
| `Lg`          | `int?`            | `null`        | Number of columns to span at the large breakpoint. Overrides `ColumnSpan`. |
| `Xl`          | `int?`            | `null`        | Number of columns to span at the extra-large breakpoint. Overrides `ColumnSpan`. |
| `Xxl`         | `int?`            | `null`        | Number of columns to span at the extra-extra-large breakpoint. Overrides `ColumnSpan`. |
| *(Inherited)* |                   |               | Inherits parameters from `BitComponentBase` (see below).                  |

### Inherited Parameters (from `BitComponentBase` for both `BitGrid` and `BitGridItem`)

| Parameter        | Type                           | Default Value                       | Description                                                                                 |
| ---------------- | ------------------------------ | ----------------------------------- | ------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                      | `null`                              | The `aria-label` attribute for the root element, improving accessibility for screen readers. |
| `Class`          | `string?`                      | `null`                              | Custom CSS class(es) to apply to the root element (`div`).                                  |
| `Dir`            | `BitDir?`                      | `null`                              | Specifies the text direction (`Ltr`, `Rtl`, `Auto`) for the component content.              |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<string, object>()`  | Allows capturing and rendering additional HTML attributes on the root element (`div`).      |
| `Id`             | `string?`                      | `null`                              | Sets a custom `id` attribute for the root element.                                          |
| `IsEnabled`      | `bool`                         | `true`                              | Whether the component and its contents are enabled (visually affects styling).              |
| `Style`          | `string?`                      | `null`                              | Custom inline CSS styles to apply to the root element (`div`).                              |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`             | Controls the visibility of the component (`Visible`, `Hidden`, `Collapsed`).                |

### Public Members (from `BitComponentBase`)

| Member        | Type               | Default Value      | Description                                                                                                |
| ------------- | ------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()`   | A read-only unique identifier (`Guid`) generated for each component instance. Useful for internal referencing. |
| `RootElement` | `ElementReference` | *(N/A)*            | An `ElementReference` pointing to the root DOM element (`div`) of the component. Useful for JS interop. |

## Related Enums

### `BitAlignment` Enum

Used for `HorizontalAlign`. Corresponds to CSS `justify-content` values.

| Name          | Value | Description                                                                                    | CSS `justify-content` Equivalent |
| ------------- | ----- | ---------------------------------------------------------------------------------------------- | -------------------------------- |
| `Start`       | `0`   | Items align to the start of the container.                                                     | `flex-start`                     |
| `End`         | `1`   | Items align to the end of the container.                                                       | `flex-end`                       |
| `Center`      | `2`   | Items align to the center of the container.                                                    | `center`                         |
| `SpaceBetween`| `3`   | Items align with equal space between them; first/last items touch container edges.              | `space-between`                  |
| `SpaceAround` | `4`   | Items align with equal space around them (half-space at ends).                                 | `space-around`                   |
| `SpaceEvenly` | `5`   | Items align with equal space between them and at the ends.                                     | `space-evenly`                   |
| `Baseline`    | `6`   | Items align based on their text baseline. (Effect depends on content).                         | `baseline`                       |
| `Stretch`     | `7`   | Items stretch to fill the container (if applicable, often needs specific item sizing).        | `stretch`                        |

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
* Review/Edit the [Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Layouts/Grid/BitGridDemo.razor).
* Review/Edit the [Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Layouts/Grid/BitGrid.razor).