# BitCard Component Reference

This document serves as a comprehensive guide for the **BitCard** component from bit BlazorUI. A Card is a container that wraps around a specific content area, keeping the design focused and clean by grouping related information.

---

## Overview

The **BitCard** component provides a flexible container for displaying content. It helps maintain a clear and organized UI by isolating content into distinct sections. Cards can be styled with custom backgrounds, borders, and sizing options to seamlessly fit within your design.

---

## Usage

### 1. Basic Card

A simple card example displaying a title, description, and a call-to-action link.

```razor
<BitCard>
    <h4>bit BlazorUI</h4>
    <p>bit BlazorUI components are native, easy-to-customize, and ...</p>
    <a href="https://blazorui.bitplatform.dev" target="_blank">Learn more</a>
</BitCard>
```

*This example uses the default background style (e.g., `bit-crd-sbg`) to create a clean and focused card.*

---

### 2. Card with Custom Background

You can change the background of the card by specifying a background color kind using the `Background` property.

```razor
<BitCard Background="BitColorKind.Primary">
    <h4>bit BlazorUI</h4>
    <p>bit BlazorUI components are native, easy-to-customize, and ...</p>
    <a href="https://blazorui.bitplatform.dev" target="_blank">Learn more</a>
</BitCard>
```

*In this example, the card uses the primary color kind for its background. Other options include Secondary, Tertiary, and Transparent.*

---

### 3. Card with Border

To add a border to the card, set the `Border` property with a desired color kind.

```razor
<BitCard Border="BitColorKind.Secondary">
    <h4>bit BlazorUI</h4>
    <p>bit BlazorUI components are native, easy-to-customize, and ...</p>
    <a href="https://blazorui.bitplatform.dev" target="_blank">Learn more</a>
</BitCard>
```

*This card example demonstrates how to highlight the card by applying a border color.*

---

### 4. FullSize Card Options

Control the dimensions of your card using the `FullSize`, `FullWidth`, and `FullHeight` properties. This is useful when you want the card to span the entire width or height of its parent container.

```razor
<BitCard FullSize="true">
    <h4>bit BlazorUI</h4>
    <p>bit BlazorUI components are native, easy-to-customize, and ...</p>
    <a href="https://blazorui.bitplatform.dev" target="_blank">Learn more</a>
</BitCard>
```

*Alternatively, you can use `FullWidth="true"` or `FullHeight="true"` to control only one dimension.*

---

### 5. Card with Border and Background Customization (Advanced)

You can combine the properties to create a card with both a custom background and border. Additionally, you may override the default styling by using custom CSS classes.

```razor
<BitCard Background="BitColorKind.Tertiary" Border="BitColorKind.Transparent" Class="custom-card-class">
    <h4>bit BlazorUI</h4>
    <p>Explore how BitCard can be fully customized to suit your UI design needs.</p>
    <a href="https://blazorui.bitplatform.dev" target="_blank">Learn more</a>
</BitCard>
```

---

## API Reference

### BitCard Component Parameters

| Name         | Type                | Default Value | Description                                                           |
| ------------ | ------------------- | ------------- | --------------------------------------------------------------------- |
| Background   | BitColorKind?       | null          | Sets the background color kind of the card.                           |
| Border       | BitColorKind?       | null          | Sets the border color kind of the card.                               |
| ChildContent | RenderFragment      | –             | The content displayed inside the card.                                |
| FullHeight   | bool?               | null          | If true, the card takes 100% of the parent's height.                    |
| FullSize     | bool?               | null          | If true, the card takes 100% of both width and height of its parent.     |
| FullWidth    | bool?               | null          | If true, the card takes 100% of the parent's width.                     |

### BitComponentBase Parameters

| Name           | Type                           | Default Value                             | Description                                                                  |
| -------------- | ------------------------------ | ----------------------------------------- | ---------------------------------------------------------------------------- |
| AriaLabel      | string?                        | null                                      | Aria-label for screen readers.                                               |
| Class          | string?                        | null                                      | Custom CSS class for the root element.                                      |
| Dir            | BitDir?                        | null                                      | Determines the text direction (LTR, RTL, Auto).                             |
| HtmlAttributes | Dictionary&lt;string, object&gt; | new Dictionary&lt;string, object&gt;()     | Additional HTML attributes for the component.                              |
| Id             | string?                        | null                                      | Custom id attribute; if null, a unique id is generated.                      |
| IsEnabled      | bool                           | true                                      | Specifies if the component is enabled.                                      |
| Style          | string?                        | null                                      | Custom inline style for the root element.                                   |
| Visibility     | BitVisibility                  | BitVisibility.Visible                     | Controls whether the component is visible, hidden, or collapsed.            |

### Public Members of BitComponentBase

| Name        | Type             | Default Value   | Description                                          |
| ----------- | ---------------- | --------------- | ---------------------------------------------------- |
| UniqueId    | Guid             | Guid.NewGuid()  | Unique identifier assigned upon component construction. |
| RootElement | ElementReference | –               | Reference to the root HTML element of the component. |

---

## Enumerations

### BitColorKind Enum

Defines the color kinds that can be used for the Card’s background or border.

| Name        | Value | Description                   |
| ----------- | ----- | ----------------------------- |
| Primary     | 0     | The primary color kind.       |
| Secondary   | 1     | The secondary color kind.     |
| Tertiary    | 2     | The tertiary color kind.      |
| Transparent | 3     | No background or border color. |

### BitVisibility Enum

| Name      | Value | Description                                                    |
| --------- | ----- | -------------------------------------------------------------- |
| Visible   | 0     | The component is visible.                                      |
| Hidden    | 1     | The component is hidden (visibility: hidden) but occupies space.|
| Collapsed | 2     | The component is removed from the layout (display: none).       |

### BitDir Enum

| Name | Value | Description                                                                                      |
| ---- | ----- | ---------------------------------------------------------------------------------------------- |
| Ltr  | 0     | Left-to-right; used for languages that read from left to right (e.g., English).                |
| Rtl  | 1     | Right-to-left; used for languages that read from right to left (e.g., Arabic).                 |
| Auto | 2     | Automatically determines direction based on the content.                                     |

---