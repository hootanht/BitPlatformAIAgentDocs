# BitGrid Component Documentation

The **BitGrid** component is a flexible and customizable grid layout designed for presenting structured content in a responsive manner. It offers control over the number of columns, spacing between items, responsive breakpoints, and horizontal alignment. This component is ideal for dashboards, galleries, lists, and any interface requiring a structured grid.

---

## Overview

The BitGrid component allows you to:
- **Organize content:** Arrange items in a defined grid structure.
- **Customize columns:** Specify how many columns to display overall and at various breakpoints.
- **Control spacing:** Adjust both horizontal and vertical spacing between grid items.
- **Align content:** Set horizontal alignment for grid items (e.g., start, center, end).

It uses CSS custom properties (variables) to control layout behavior, making it highly customizable with standard CSS.

---

## Usage

### Basic Example

This example demonstrates a basic grid layout with a fixed number of columns and multiple grid items.

```html
<div style="justify-content:flex-start; --span:1; --columns:4; --spacing:4px" class="bit-grd">
  <div style="--span:1" class="bit-grd-itm grid-item">Grid Item1</div>
  <div style="--span:1" class="bit-grd-itm grid-item">Grid Item2</div>
  <div style="--span:1" class="bit-grd-itm grid-item">Grid Item3</div>
  <div style="--span:1" class="bit-grd-itm grid-item">Grid Item4</div>
  <div style="--span:1" class="bit-grd-itm grid-item">Grid Item5</div>
  <div style="--span:1" class="bit-grd-itm grid-item">Grid Item6</div>
  <div style="--span:1" class="bit-grd-itm grid-item">Grid Item7</div>
  <div style="--span:1" class="bit-grd-itm grid-item">Grid Item8</div>
</div>
```

### Columns Example

You can customize the column span of individual grid items using the `--span` custom property:

```html
<div style="justify-content:flex-start; --span:1; --columns:4; --spacing:4px" class="bit-grd">
  <div style="--span:4" class="bit-grd-itm grid-item">
    Column span 4
  </div>
  <div style="--span:2" class="bit-grd-itm grid-item">
    Column span 2
  </div>
  <div style="--span:2" class="bit-grd-itm grid-item">
    Column span 2
  </div>
  <div style="--span:1" class="bit-grd-itm grid-item">
    Column span 1
  </div>
  <div style="--span:1" class="bit-grd-itm grid-item">
    Column span 1
  </div>
  <div style="--span:1" class="bit-grd-itm grid-item">
    Column span 1
  </div>
  <div style="--span:1" class="bit-grd-itm grid-item">
    Column span 1
  </div>
</div>
```

### Alignment

The BitGrid supports horizontal alignment of its items. You can set the `HorizontalAlign` parameter to control whether the grid items are aligned to the start, center, end, or distributed with space between them.

A radio group (such as BitChoiceGroup) can be used to let users select the desired alignment option:

```html
<div id="horizontalAlignSelector" role="radiogroup" class="bit-chg bit-chg-wcr">
  <label id="horizontalAlignLabel" class="bit-chg-lbl">Horizontal Align</label>
  <div class="bit-chg-cnt bit-chg-hor">
    <div class="bit-chg-icn bit-chg-ich">
      <label for="align-start"><span class="bit-chg-itx">Start</span></label>
      <input hidden type="radio" id="align-start" value="Start">
    </div>
    <div class="bit-chg-icn">
      <label for="align-center"><span class="bit-chg-itx">Center</span></label>
      <input hidden type="radio" id="align-center" value="Center">
    </div>
    <div class="bit-chg-icn">
      <label for="align-end"><span class="bit-chg-itx">End</span></label>
      <input hidden type="radio" id="align-end" value="End">
    </div>
    <!-- Additional alignment options... -->
  </div>
</div>
```

### Spacings

You can adjust the spacing between grid items using the `Spacing`, `HorizontalSpacing`, and `VerticalSpacing` properties. In the example below, sliders are used to dynamically adjust these spacing values.

```html
<!-- Vertical Spacing Slider -->
<div class="bit-sld bit-sld-hrz">
  <label class="bit-sld-lbl">Vertical spacing between items</label>
  <div class="bit-sld-cnt">
    <input type="range" min="0" max="5" step="0.1" style="--value: 0.5; --min: 0; --max: 5;">
    <label class="bit-sld-vlb">0.5 rem</label>
  </div>
</div>

<!-- Horizontal Spacing Slider -->
<div class="bit-sld bit-sld-hrz">
  <label class="bit-sld-lbl">Horizontal spacing between items</label>
  <div class="bit-sld-cnt">
    <input type="range" min="0" max="5" step="0.1" style="--value: 0.5; --min: 0; --max: 5;">
    <label class="bit-sld-vlb">0.5 rem</label>
  </div>
</div>
```

### Breakpoints

The BitGrid component supports responsive breakpoints by letting you define different column counts at various screen sizes. You can specify:

- **ColumnsXs**: Number of columns in the extra small breakpoint.
- **ColumnsSm**: Number of columns in the small breakpoint.
- **ColumnsMd**: Number of columns in the medium breakpoint.
- **ColumnsLg**: Number of columns in the large breakpoint.
- **ColumnsXl**: Number of columns in the extra large breakpoint.
- **ColumnsXxl**: Number of columns in the extra extra large breakpoint.

Example:

```html
<div style="justify-content:flex-start; --span:1; --columns:4; --spacing:4px" class="bit-grd">
  <div style="--md:1; --span:4" class="bit-grd-itm grid-item">
    Md = 1
  </div>
  <div style="--xs:3; --md:2; --span:1" class="bit-grd-itm grid-item">
    Xs = 3, Md = 2
  </div>
  <div style="--lg:2; --span:1" class="bit-grd-itm grid-item">
    Lg = 2
  </div>
  <!-- Additional grid items... -->
</div>
```

---

## API Reference

### BitGrid Parameters

| Name                | Type              | Default Value | Description                                                     |
|---------------------|-------------------|---------------|-----------------------------------------------------------------|
| **ChildContent**    | `RenderFragment?` | `null`        | Content to be rendered within the grid container.             |
| **Columns**         | `int`             | `12`          | Total number of columns in the grid layout.                     |
| **ColumnsXs**       | `int?`            | `null`      | Number of columns for extra small screens.                      |
| **ColumnsSm**       | `int?`            | `null`      | Number of columns for small screens.                            |
| **ColumnsMd**       | `int?`            | `null`      | Number of columns for medium screens.                           |
| **ColumnsLg**       | `int?`            | `null`      | Number of columns for large screens.                            |
| **ColumnsXl**       | `int?`            | `null`      | Number of columns for extra large screens.                      |
| **ColumnsXxl**      | `int?`            | `null`      | Number of columns for extra extra large screens.                |
| **HorizontalAlign** | `BitAlignment?`   | `BitAlignment.Start` | Sets horizontal alignment of grid items.               |
| **HorizontalSpacing** | `string?`       | `null`      | Custom horizontal spacing between grid items (e.g., "4px").       |
| **Spacing**         | `string`          | `"4px"`       | Default spacing between grid items.                             |
| **Span**            | `int`             | `1`           | Default number of columns each grid item occupies.              |
| **VerticalSpacing** | `string?`         | `null`      | Custom vertical spacing between grid items.                       |

### Inherited BitComponentBase Parameters

| Name              | Type                         | Default Value                        | Description                                                       |
|-------------------|------------------------------|--------------------------------------|-------------------------------------------------------------------|
| **AriaLabel**     | `string?`                    | `null`                               | ARIA label for accessibility.                                     |
| **Class**         | `string?`                    | `null`                               | Custom CSS classes for the grid container.                        |
| **Dir**           | `BitDir?`                    | `null`                               | Sets text direction (LTR, RTL, or Auto).                           |
| **HtmlAttributes**| `Dictionary<string, object>` | `new Dictionary<string, object>()`   | Additional attributes for the grid container.                     |
| **Id**            | `string?`                    | `null`                               | Custom id for the grid; if not provided, a unique id is generated.  |
| **IsEnabled**     | `bool`                       | `true`                               | Determines if the grid is enabled.                                  |
| **Style**         | `string?`                    | `null`                               | Inline CSS styles for the grid container.                           |
| **Visibility**    | `BitVisibility`              | `BitVisibility.Visible`              | Controls the visibility state of the grid.                         |

---

## BitGridItem Properties

Each grid item can be individually configured to control how many columns it spans at various breakpoints.

| Name          | Type             | Default Value | Description                                                   |
|---------------|------------------|---------------|---------------------------------------------------------------|
| **ChildContent** | `RenderFragment?` | `null`      | Content rendered inside the grid item.                        |
| **ColumnSpan**   | `int`           | `1`           | Number of columns the grid item spans.                        |
| **Xs**           | `int?`          | `null`      | Column span for extra small screens.                           |
| **Sm**           | `int?`          | `null`      | Column span for small screens.                                 |
| **Md**           | `int?`          | `null`      | Column span for medium screens.                                |
| **Lg**           | `int?`          | `null`      | Column span for large screens.                                 |
| **Xl**           | `int?`          | `null`      | Column span for extra large screens.                           |
| **Xxl**          | `int?`          | `null`      | Column span for extra extra large screens.                     |

---

## Enumerations

### BitAlignment Enum

Used for setting the horizontal alignment of grid items.

| Name           | Value | Description                                      |
|----------------|-------|--------------------------------------------------|
| **Start**      | 0     | Aligns items to the start (left for LTR).         |
| **Center**     | 2     | Centers the grid items.                           |
| **End**        | 1     | Aligns items to the end (right for LTR).          |
| **SpaceBetween** | 3   | Distributes items with space between them.       |
| **SpaceAround** | 4    | Distributes items with equal space around them.  |
| **SpaceEvenly** | 5    | Evenly spaces items within the container.        |
| **Baseline**    | 6    | Aligns items based on their baseline.            |
| **Stretch**     | 7    | Stretches items to fill the container.           |

### BitDir Enum

Defines the text direction.

| Name  | Value | Description                                         |
|-------|-------|-----------------------------------------------------|
| **Ltr** | 0   | Left-to-right direction (e.g., English).            |
| **Rtl** | 1   | Right-to-left direction (e.g., Arabic).             |
| **Auto**| 2   | Auto-detects direction based on content.            |

### BitVisibility Enum

Determines the visibility state.

| Name       | Value | Description                                                      |
|------------|-------|------------------------------------------------------------------|
| **Visible**   | 0   | The grid is visible.                                            |
| **Hidden**    | 1   | The grid is hidden but occupies its space (using CSS visibility).|
| **Collapsed** | 2   | The grid is not rendered (using CSS display: none).             |

### BitSize Enum

Defines sizing options (can be applied to grid items or the grid).

| Name    | Value | Description       |
|---------|-------|-------------------|
| **Small**  | 0   | Small size.      |
| **Medium** | 1   | Medium size.     |
| **Large**  | 2   | Large size.      |

---