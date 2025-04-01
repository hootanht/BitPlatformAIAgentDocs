# BitStack Component Documentation

The **BitStack** component is a container-type control that abstracts a flexbox layout to organize its children. It provides a flexible way to render items either vertically or horizontally, with options for wrapping, alignment, spacing, and growth. Additionally, it supports nested layouts and dynamic gap adjustments.

> **Note:** The BitStack component is sometimes referred to as a "WrapPanel" when used in certain contexts.

---

## Overview

- **Purpose:**  
  Provides a simplified abstraction over CSS flexbox to lay out child components.
  
- **Key Features:**  
  - Render children vertically (default) or horizontally.
  - Reverse the order of children (vertical or horizontal).
  - Customize the gap between items.
  - Support for wrapping when children overflow.
  - Ability to nest stacks for complex layouts.
  - Control over growth of items relative to siblings.
  - Adjustable alignment (both horizontal and vertical).

---

## Usage Examples

### 1. Basic Layout Variants

#### Default (Vertical)

The default behavior renders children in a vertical stack with a configurable gap.

```html
<!-- Default vertical stack -->
<div style="display:flex; flex-direction:column; gap:1rem; background:#71afe5" class="bit-stc">
  <div style="color:black">Item 1</div>
  <div style="color:black">Item 2</div>
  <div style="color:black">Item 3</div>
</div>
```

#### Horizontal

Render the items in a horizontal row.

```html
<!-- Horizontal stack -->
<div style="display:flex; flex-direction:row; gap:1rem; background:#71afe5" class="bit-stc">
  <div style="color:black">Item 1</div>
  <div style="color:black">Item 2</div>
  <div style="color:black">Item 3</div>
</div>
```

#### Reversed Vertical

Display the items in reverse order (bottom-to-top).

```html
<!-- Reversed vertical stack -->
<div style="display:flex; flex-direction:column-reverse; gap:1rem; background:#71afe5" class="bit-stc">
  <div style="color:black">Item 1</div>
  <div style="color:black">Item 2</div>
  <div style="color:black">Item 3</div>
</div>
```

#### Reversed Horizontal

Display the items in reverse order (right-to-left).

```html
<!-- Reversed horizontal stack -->
<div style="display:flex; flex-direction:row-reverse; gap:1rem; background:#71afe5" class="bit-stc">
  <div style="color:black">Item 1</div>
  <div style="color:black">Item 2</div>
  <div style="color:black">Item 3</div>
</div>
```

---

### 2. Gap Adjustment

You can control the spacing between children using the **Gap** parameter. For example, a slider might be used to adjust the gap dynamically.

```html
<!-- Example: Gap slider and stack with adjustable gap -->
<label>Gap between items</label>
<input type="range" min="0" max="5" step="0.1" style="--value: 1; --min: 0; --max: 5;">
<label>1.0 rem</label>

<div style="display:flex; flex-direction:column; gap:1rem; background:#71afe5" class="bit-stc">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>
```

---

### 3. Nesting Stacks

Stacks can be nested to create more complex layouts. In the example below, a horizontal stack contains nested vertical and horizontal stacks.

```html
<!-- Nested Stack Example -->
<div style="display:flex; flex-direction:row; gap:1rem; justify-content:space-around; background:#71afe5" class="bit-stc">
  <div class="item">Item 1</div>
  <div style="display:flex; flex-direction:column; gap:1rem" class="bit-stc">
    <div class="item">Item 2-1</div>
    <div class="item">Item 2-2</div>
    <div class="item">Item 2-3</div>
  </div>
  <div style="display:flex; flex-direction:row; gap:1rem" class="bit-stc">
    <div class="item">Item 3-1</div>
    <div class="item">Item 3-2</div>
    <div class="item">Item 3-3</div>
  </div>
</div>
```

---

### 4. Alignment & Direction

Adjust the alignment and orientation of the children using properties like **HorizontalAlign**, **VerticalAlign**, and **Reversed**. In this example, radio groups and toggle buttons simulate the control of these properties.

```html
<!-- Alignment Controls Example -->
<div style="display:flex; flex-direction:row; gap:2rem; flex-wrap:wrap" class="bit-stc">
  <!-- Toggle for horizontal layout -->
  <div class="bit-tgl">
    <button role="switch" type="button" class="bit-tgl-btn" aria-checked="false"></button>
    <label>Horizontal</label>
  </div>
  <!-- Toggle for reversed layout -->
  <div class="bit-tgl">
    <button role="switch" type="button" class="bit-tgl-btn" aria-checked="false"></button>
    <label>Reversed</label>
  </div>
</div>

<!-- Radio groups for alignment -->
<div role="radiogroup" class="bit-chg">
  <label><span>Direction</span></label>
  <div class="bit-chg-cnt">
    <label><span>LTR</span></label>
    <input type="radio" value="Ltr">
    <label><span>RTL</span></label>
    <input type="radio" value="Rtl">
    <label><span>Auto</span></label>
    <input type="radio" value="Auto">
  </div>
</div>

<div role="radiogroup" class="bit-chg">
  <label><span>Horizontal Align</span></label>
  <div class="bit-chg-cnt">
    <label><span>Start</span></label>
    <input type="radio" value="Start">
    <label><span>Center</span></label>
    <input type="radio" value="Center">
    <label><span>End</span></label>
    <input type="radio" value="End">
    <label><span>SpaceBetween</span></label>
    <input type="radio" value="SpaceBetween">
    <label><span>SpaceAround</span></label>
    <input type="radio" value="SpaceAround">
    <label><span>SpaceEvenly</span></label>
    <input type="radio" value="SpaceEvenly">
    <label><span>Baseline</span></label>
    <input type="radio" value="Baseline">
    <label><span>Stretch</span></label>
    <input type="radio" value="Stretch">
  </div>
</div>

<div role="radiogroup" class="bit-chg">
  <label><span>Vertical Align</span></label>
  <div class="bit-chg-cnt">
    <label><span>Start</span></label>
    <input type="radio" value="Start">
    <label><span>Center</span></label>
    <input type="radio" value="Center">
    <label><span>End</span></label>
    <input type="radio" value="End">
    <label><span>SpaceBetween</span></label>
    <input type="radio" value="SpaceBetween">
    <label><span>SpaceAround</span></label>
    <input type="radio" value="SpaceAround">
    <label><span>SpaceEvenly</span></label>
    <input type="radio" value="SpaceEvenly">
    <label><span>Baseline</span></label>
    <input type="radio" value="Baseline">
    <label><span>Stretch</span></label>
    <input type="radio" value="Stretch">
  </div>
</div>
```

---

### 5. Wrap Behavior

Enable wrapping so that children move onto multiple rows or columns when they overflow.

```html
<!-- Wrap Example with adjustable Stack height -->
<label>Stack height</label>
<input type="range" min="10" max="20" step="0.1" style="--value: 15; --min: 10; --max: 20;">
<label>15.0 rem</label>

<div style="display:flex; flex-direction:column; gap:1rem; flex-wrap:wrap; height:15rem; background:#71afe5" class="bit-stc">
  <div class="item">Item 0</div>
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <!-- Additional items... -->
  <div class="item">Item 19</div>
</div>
```

---

### 6. Grow Behavior

Control how each child grows relative to its siblings by setting the **Grow** or **Grows** parameters.

#### Vertical Grow

```html
<!-- Vertical stack with different grow values -->
<div style="display:flex; flex-direction:column; gap:0.5rem; background:#71afe5; height:15rem" class="bit-stc">
  <div style="flex-grow:3; display:flex; align-items:center; justify-content:center" class="item">
    Grow is 3
  </div>
  <div style="flex-grow:2; display:flex; align-items:center; justify-content:center" class="item">
    Grow is 2
  </div>
  <div style="flex-grow:1; display:flex; align-items:center; justify-content:center" class="item">
    Grow is 1
  </div>
</div>
```

#### Horizontal Grow

```html
<!-- Horizontal stack with an item that grows -->
<div style="display:flex; flex-direction:row; gap:0.5rem; background:#71afe5; height:15rem" class="bit-stc">
  <div style="display:flex; align-items:center; justify-content:center" class="item">
    Normal
  </div>
  <div style="flex-grow:1; display:flex; align-items:center; justify-content:center" class="item">
    Grows
  </div>
  <div style="display:flex; align-items:center; justify-content:center" class="item">
    Normal
  </div>
</div>
```

---

## API Reference

### BitStack Parameters

| Name             | Type                  | Default Value | Description                                                                                                                                                                                                                                              |
|------------------|-----------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Alignment**    | `BitAlignment?`       | `null`        | Defines how to align Stack children (both horizontally and vertically).                                                                                                                                                                                 |
| **AutoHeight**   | `bool`                | `false`       | Makes the height of the stack automatically adjust to fit its content.                                                                                                                                                                                 |
| **AutoSize**     | `bool`                | `false`       | Makes both the width and height of the stack adjust automatically to fit its content.                                                                                                                                                                  |
| **AutoWidth**    | `bool`                | `false`       | Makes the width of the stack automatically adjust to fit its content.                                                                                                                                                                                  |
| **ChildContent** | `RenderFragment?`     | `null`        | The render fragment representing the content of the stack.                                                                                                                                                                                             |
| **Element**      | `string?`             | `null`        | The custom HTML element to be used for the root node (default is `"div"`).                                                                                                                                                                               |
| **FillContent**  | `bool`                | `false`       | Expands the direct children so they occupy the full width of the root element.                                                                                                                                                                           |
| **FitHeight**    | `bool`                | `false`       | Sets the height of the stack to fit its content.                                                                                                                                                                                                       |
| **FitSize**      | `bool`                | `false`       | Sets both the width and height of the stack to fit its content.                                                                                                                                                                                          |
| **FitWidth**     | `bool`                | `false`       | Sets the width of the stack to fit its content.                                                                                                                                                                                                          |
| **Gap**          | `string?`             | `null`        | Defines the spacing between Stack children. Specify a value for the row gap, optionally followed by a value for the column gap. If the column gap is omitted, it will use the same value as the row gap.                                             |
| **Grow**         | `string?`             | `null`        | Defines how much the Stack should grow in proportion to its siblings.                                                                                                                                                                                    |
| **Grows**        | `bool`                | `false`       | When set to true, makes the stack grow in proportion to its siblings.                                                                                                                                                                                    |
| **Horizontal**   | `bool`                | `false`       | If true, renders the Stack children horizontally instead of vertically.                                                                                                                                                                                |
| **HorizontalAlign** | `BitAlignment?`    | `null`        | Defines the horizontal alignment of the Stack children.                                                                                                                                                                                                |
| **Reversed**     | `bool`                | `false`       | If true, renders the Stack children in the reverse order (bottom-to-top for vertical stacks, right-to-left for horizontal stacks).                                                                                                                      |
| **VerticalAlign**   | `BitAlignment?`    | `null`        | Defines the vertical alignment of the Stack children.                                                                                                                                                                                                  |
| **Wrap**         | `bool`                | `false`       | If true, Stack children will wrap onto multiple rows or columns when they overflow the size of the Stack.                                                                                                                                               |

---

### Inherited from BitComponentBase

| Name             | Type                           | Default Value                           | Description                                                                                                                        |
|------------------|--------------------------------|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| **AriaLabel**    | `string?`                      | `null`                                  | The aria-label of the component for accessibility purposes.                                                                      |
| **Class**        | `string?`                      | `null`                                  | Custom CSS class for the root element of the component.                                                                            |
| **Dir**          | `BitDir?`                      | `null`                                  | Determines the text direction (left-to-right, right-to-left, or auto).                                                             |
| **HtmlAttributes** | `Dictionary<string, object>` | `new Dictionary<string, object>()`      | Additional HTML attributes to be applied to the root element.                                                                      |
| **Id**           | `string?`                      | `null`                                  | Custom id attribute for the root element; if `null`, a unique id is automatically generated.                                       |
| **IsEnabled**    | `bool`                         | `true`                                  | Indicates whether the component is enabled.                                                                                        |
| **Style**        | `string?`                      | `null`                                  | Custom CSS style for the root element of the component.                                                                            |
| **Visibility**   | `BitVisibility`                | `BitVisibility.Visible`                 | Controls whether the component is visible, hidden, or collapsed.                                                                   |

---

### BitComponentBase Public Members

| Name         | Type             | Default Value    | Description                                                                                           |
|--------------|------------------|------------------|-------------------------------------------------------------------------------------------------------|
| **UniqueId** | `Guid`           | `Guid.NewGuid()` | The read-only unique identifier for the root element, generated at component instantiation.           |
| **RootElement** | `ElementReference` | –           | Reference to the root DOM element of the component.                                                  |

---

## Enumerations

### BitAlignment Enum

Defines the alignment options for arranging children.

| Name           | Value | Description                                                              |
|----------------|-------|--------------------------------------------------------------------------|
| **Start**      | `0`   | Aligns children to the start (left or top).                              |
| **End**        | `1`   | Aligns children to the end (right or bottom).                            |
| **Center**     | `2`   | Centers the children.                                                    |
| **SpaceBetween** | `3` | Distributes children evenly, with the first item at the start and the last at the end. |
| **SpaceAround** | `4`  | Distributes children evenly with equal space around them.                |
| **SpaceEvenly** | `5`  | Distributes children so that the space between any two items (and around the edges) is equal. |
| **Baseline**   | `6`   | Aligns children based on their text baselines.                           |
| **Stretch**    | `7`   | Stretches children to fill the available space.                          |

---

### BitVisibility Enum

Specifies the visibility state of a component.

| Name      | Value | Description                                                              |
|-----------|-------|--------------------------------------------------------------------------|
| **Visible**   | `0`   | The component is fully visible.                                      |
| **Hidden**    | `1`   | The component is hidden, but its space remains (`visibility:hidden`).   |
| **Collapsed** | `2`   | The component is hidden and does not occupy any space (`display:none`). |

---

### BitDir Enum

Determines the text direction of the component.

| Name   | Value | Description                                                                                          |
|--------|-------|------------------------------------------------------------------------------------------------------|
| **Ltr**| `0`   | Left-to-right: use for languages written from left to right (e.g., English).                         |
| **Rtl**| `1`   | Right-to-left: use for languages written from right to left (e.g., Arabic).                          |
| **Auto**| `2`  | Automatically determines direction based on the content's character analysis.                      |

---