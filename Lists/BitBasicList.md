# BitBasicList Component Reference

The **BitBasicList** component provides a foundational base for rendering large sets of items. It is layout agnostic and is not tied to any specific tile component or selection management, making it a versatile tool for displaying lists of data—whether simple or complex.

---

## Overview

`BitBasicList` is ideal for rendering large collections of items efficiently. It supports virtualization for performance improvement, custom templates for list rows, and is designed to be styled and extended as needed. This component is commonly used for displaying lists such as people, products, or any other item sets.

---

## Usage

### Basic Usage

The basic example demonstrates how to render a simple list of people. Each item is displayed with custom padding, margin, and background styling.

```html
<!-- Basic BitBasicList Example -->
<div id="ykhuss" style="border: 1px solid #a19f9d; border-radius: 4px;" class="bit-bsl" role="list">
  <div style="padding: 5px 20px; margin: 10px; background-color: #75737329;">
    Name: <strong>Person 1</strong>
  </div>
  <div style="padding: 5px 20px; margin: 10px; background-color: #75737329;">
    Name: <strong>Person 2</strong>
  </div>
  <div style="padding: 5px 20px; margin: 10px; background-color: #75737329;">
    Name: <strong>Person 3</strong>
  </div>
  <!-- Additional list items... -->
  <div style="padding: 5px 20px; margin: 10px; background-color: #75737329;">
    Name: <strong>Person 100</strong>
  </div>
</div>
```

---

### Virtualization

When working with large datasets, enabling virtualization ensures that only the items within the viewport (plus a buffer) are rendered. This improves scrolling performance and overall responsiveness.

```html
<!-- Virtualization Example -->
<div id="ctcp7d" style="border: 1px solid rgb(161, 159, 157); border-radius: 4px; overflow-anchor: none;" class="bit-bsl" role="list">
  <!-- A few virtualized list items -->
  <div style="border-bottom: 1px solid #8a8886; padding: 5px 20px; margin: 10px;">
    <img width="100" height="100" src="https://picsum.photos/100/100?random=1" alt="Random image">
    <div style="margin-left:3%; display: inline-block;">
      <p>Id: <strong>1</strong></p>
      <p>Full Name: <strong>Person 1 Person Family 1</strong></p>
      <p>Job: <strong>Programmer 1</strong></p>
    </div>
  </div>
  <!-- More items are loaded as the user scrolls -->
  <div style="height: 991362.3px; flex-shrink: 0;"></div>
</div>
```

---

### Style & Class Customization

Customize the appearance of the list by setting your own CSS classes or inline styles. This example demonstrates applying a custom class to the `BitBasicList` container as well as custom styling for individual list items.

```html
<!-- Style & Class Customization Example -->
<div id="om9c2a" style="border: 1px solid #a19f9d; border-radius: 4px;" class="bit-bsl custom-class" role="list">
  <div class="list-item">
    <span>Id: <strong>1</strong></span>
    <span>Full Name: <strong>Person 1</strong></span>
    <span>Job: <strong>Programmer 1</strong></span>
  </div>
  <div class="list-item">
    <span>Id: <strong>2</strong></span>
    <span>Full Name: <strong>Person 2</strong></span>
    <span>Job: <strong>Programmer 2</strong></span>
  </div>
  <!-- More list items... -->
</div>
```

---

### ItemsProvider

For dynamic data loading, `BitBasicList` supports an `ItemsProvider` callback. This approach is useful for asynchronously fetching data and displaying a custom placeholder when data is loading.

```html
<!-- ItemsProvider Example -->
<div id="di4yll" style="border: 1px solid #a19f9d; border-radius: 4px;" class="bit-bsl" role="list">
  <div style="border-bottom: 1px solid #8a8886; padding: 5px 20px;">
    <div>Id: <strong>1</strong></div>
    <div>Name: <strong>Product 1</strong></div>
    <div>Price: <strong>81</strong></div>
  </div>
  <div style="border-bottom: 1px solid #8a8886; padding: 5px 20px;">
    <div>Id: <strong>2</strong></div>
    <div>Name: <strong>Product 2</strong></div>
    <div>Price: <strong>22</strong></div>
  </div>
  <!-- More items loaded via ItemsProvider -->
</div>
```

---

### Grouped ItemsProvider

When your data is organized into categories, you can render group headers along with their respective items. The following example demonstrates grouping products by category.

```html
<!-- Grouped ItemsProvider Example -->
<div id="p2cw1s" style="border: 1px solid #a19f9d; border-radius: 4px;" class="bit-bsl" role="list">
  <!-- Group Header for Category 1 -->
  <div style="border-bottom: 1px solid #8a8886; padding: 5px 20px; background-color: #75737329;">
    <div>Category 1</div>
  </div>
  <!-- Items under Category 1 -->
  <div style="border-bottom: 1px solid #8a8886; padding: 5px 10px; display: flex; flex-flow: row;">
    <div style="width:184px;">Name: <strong>Product 1 at 1</strong></div>
    <div>Price: <strong>988</strong></div>
  </div>
  <!-- Additional items for Category 1 ... -->
  <!-- Group Header for Category 2 -->
  <div style="border-bottom: 1px solid #8a8886; padding: 5px 20px; background-color: #75737329;">
    <div>Category 2</div>
  </div>
  <!-- Items under Category 2 -->
  <div style="border-bottom: 1px solid #8a8886; padding: 5px 10px; display: flex; flex-flow: row;">
    <div style="width:184px;">Name: <strong>Product 1 at 2</strong></div>
    <div>Price: <strong>868</strong></div>
  </div>
  <!-- Additional grouped items... -->
</div>
```

---

### RTL (Right-to-Left)

For right-to-left language support, such as for Arabic or Hebrew, you can configure `BitBasicList` to render its content in RTL mode.

```html
<!-- RTL BitBasicList Example -->
<div id="wrpcf" style="border: 1px solid #a19f9d; border-radius: 4px;" class="bit-bsl bit-rtl" dir="rtl" role="list">
  <div style="padding: 5px 20px; margin: 10px; background-color: #75737329;">
    <p>شناسه: <strong>1</strong></p>
    <p>نام کامل: <strong>شخص 1 نام خانواگی شخص 1</strong></p>
    <p>شغل: <strong>برنامه نویس 1</strong></p>
  </div>
  <!-- Additional RTL list items... -->
</div>
```

---

## API Reference

### BitBasicList Parameters

| **Name**               | **Type**                                      | **Default Value**                  | **Description**                                                                                             |
|------------------------|-----------------------------------------------|------------------------------------|-------------------------------------------------------------------------------------------------------------|
| `EmptyContent`         | `RenderFragment?`                             | `null`                             | Custom content rendered when there are no items.                                                          |
| `EnableVirtualization` | `bool`                                        | `false`                            | Enables virtualization for efficient rendering of large lists.                                            |
| `Items`                | `ICollection<TItem>`                          | `new Array.Empty<TItem>()`         | The list of items to render.                                                                                |
| `ItemSize`             | `float`                                       | `50`                               | The size (in pixels) of each item. Defaults to 50px.                                                        |
| `OverscanCount`        | `int`                                         | `3`                                | Number of additional items rendered before and after the visible region to smooth scrolling.                |
| `Role`                 | `string`                                      | `"list"`                           | Specifies the role attribute of the list element.                                                         |
| `RowTemplate`          | `RenderFragment<TItem>?`                       | `null`                             | Template for rendering each row/item.                                                                     |
| `ItemsProvider`        | `BitBasicListItemsProvider<TItem>?`           | `null`                             | A callback that supplies data for the list. Use either `Items` or `ItemsProvider`, but not both.             |
| `VirtualizePlaceholder`| `RenderFragment<PlaceholderContext>?`         | `null`                             | Custom template for the virtualization placeholder (displayed while loading new data).                       |

### Inherited BitComponentBase Parameters

| **Name**         | **Type**                       | **Default Value**                  | **Description**                                                                                         |
|------------------|--------------------------------|------------------------------------|---------------------------------------------------------------------------------------------------------|
| `AriaLabel`      | `string?`                      | `null`                             | An accessible label for the list.                                                                       |
| `Class`          | `string?`                      | `null`                             | Additional CSS class(es) for the root element.                                                          |
| `Dir`            | `BitDir?`                      | `null`                             | Sets the text direction (e.g., LTR, RTL, or Auto).                                                      |
| `HtmlAttributes` | `Dictionary<string, object>`   | `new Dictionary<string, object>()` | Additional HTML attributes to be added to the root element.                                             |
| `Id`             | `string?`                      | `null`                             | Custom identifier for the root element. A unique id is generated if not provided.                       |
| `IsEnabled`      | `bool`                         | `true`                             | Determines whether the component is enabled.                                                          |
| `Style`          | `string?`                      | `null`                             | Inline CSS styles for the root element.                                                                 |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`            | Controls the overall visibility of the component.                                                     |

### Public Members (BitComponentBase)

| **Name**       | **Type**           | **Default Value**     | **Description**                                                      |
|----------------|--------------------|-----------------------|----------------------------------------------------------------------|
| `UniqueId`     | `Guid`             | `Guid.NewGuid()`      | A read-only unique identifier for the component’s root element.      |
| `RootElement`  | `ElementReference` | –                     | A reference to the root HTML element of the component.                |

---

## Enumerations

### BitVisibility Enum

Defines the visibility state of the component.

| **Name**    | **Value** | **Description**                                                                           |
|-------------|-----------|-------------------------------------------------------------------------------------------|
| `Visible`   | `0`       | The component is visible.                                                                 |
| `Hidden`    | `1`       | The component is hidden (using CSS `visibility: hidden`), but space is still reserved.     |
| `Collapsed` | `2`       | The component is collapsed (using CSS `display: none`), and no space is allocated.          |

### BitDir Enum

Specifies the text direction.

| **Name** | **Value** | **Description**                                                           |
|----------|-----------|---------------------------------------------------------------------------|
| `Ltr`    | `0`       | Left-to-right (for languages such as English).                           |
| `Rtl`    | `1`       | Right-to-left (for languages such as Arabic or Hebrew).                  |
| `Auto`   | `2`       | Automatically detects direction based on the content.                     |

---