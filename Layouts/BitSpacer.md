# BitSpacer Component Documentation

The **BitSpacer** component is used to generate space between other UI components. It supports both fixed spacing (using a specified width in pixels) and flexible spacing that adjusts dynamically.

This documentation is intended for AI agents and developers as a reference guide, providing detailed explanations of the component’s usage, API, parameters, and related enums.

---

## Overview

The **BitSpacer** serves a simple but important role:
- **Purpose:** Generate space between components.
- **Usage:** Create a fixed space by specifying a pixel width or allow the space to adjust flexibly.

The component inherits from `BitComponentBase`, which adds additional parameters for accessibility, styling, and behavior control.

---

## Usage Examples

### Basic Example

The following example demonstrates the basic usage of **BitSpacer** in a layout. It shows how the spacer is placed between buttons and text to provide balanced spacing.

```html
<div style="display: flex; width: 100%;">
  <!-- Left button -->
  <button class="bit-btn bit-btn-pri bit-btn-md">
    <i class="bit-btn-icn bit-icon bit-icon--GlobalNavButton"></i>
  </button>
  
  <!-- Spacer component without fixed width (flexible space) -->
  <div class="bit-spc"></div>
  
  <!-- Title text -->
  <h6 class="bit-txt bit-txt-h6">Title</h6>
  
  <!-- Another flexible spacer -->
  <div class="bit-spc"></div>
  
  <!-- Right button -->
  <button class="bit-btn bit-btn-ntx bit-btn-txt bit-btn-pri bit-btn-md">
    <i class="bit-btn-icn bit-icon bit-icon--Contact"></i>
  </button>
</div>
```

### Adjusting Spacer Width

If a fixed spacing is required, you can set the spacer’s width by passing a width parameter. This example shows how to use a spacer with a fixed margin to separate elements:

```html
<div style="display: flex; width: 100%;">
  <!-- First component -->
  <div class="bit-prb">
    <!-- Icon or content -->
    <svg class="bit-prb-cir" height="12px" width="12px">
      <circle class="bit-prb-crt" r="40%" cx="50%" cy="50%"></circle>
      <circle class="bit-prb-cri" r="40%" cx="50%" cy="50%"></circle>
    </svg>
  </div>
  
  <!-- Spacer with fixed width (using inline style for demonstration) -->
  <div class="bit-spc" style="margin-inline-start:64px"></div>
  
  <!-- Second component -->
  <div class="bit-prb">
    <svg class="bit-prb-cir" height="12px" width="12px">
      <circle class="bit-prb-crt" r="40%" cx="50%" cy="50%"></circle>
      <circle class="bit-prb-cri" r="40%" cx="50%" cy="50%"></circle>
    </svg>
  </div>
  
  <!-- Another spacer with fixed width -->
  <div class="bit-spc" style="margin-inline-start:64px"></div>
  
  <!-- Third component -->
  <div class="bit-prb">
    <svg class="bit-prb-cir" height="12px" width="12px">
      <circle class="bit-prb-crt" r="40%" cx="50%" cy="50%"></circle>
      <circle class="bit-prb-cri" r="40%" cx="50%" cy="50%"></circle>
    </svg>
  </div>
</div>
```

---

## API Reference

### BitSpacer Parameters

| Name  | Type  | Default Value | Description                                           |
|-------|-------|---------------|-------------------------------------------------------|
| Width | int?  | `null`        | Gets or sets the width of the spacer (in pixels).     |

### Inherited from BitComponentBase

The **BitSpacer** inherits the following parameters from `BitComponentBase`:

| Name           | Type                         | Default Value                          | Description                                                                                           |
|----------------|------------------------------|----------------------------------------|-------------------------------------------------------------------------------------------------------|
| AriaLabel      | string?                      | `null`                                 | The aria-label for the component, supporting screen reader accessibility.                           |
| Class          | string?                      | `null`                                 | Custom CSS class for the root element.                                                              |
| Dir            | BitDir?                      | `null`                                 | Determines the text direction (e.g., left-to-right or right-to-left).                                |
| HtmlAttributes | Dictionary<string, object>   | `new Dictionary<string, object>()`     | Additional HTML attributes to be applied to the root element.                                       |
| Id             | string?                      | `null`                                 | Custom id for the root element. If `null`, a unique identifier is generated automatically.          |
| IsEnabled      | bool                         | `true`                                 | Indicates whether the component is enabled.                                                         |
| Style          | string?                      | `null`                                 | Custom CSS styles for the root element.                                                             |
| Visibility     | BitVisibility                | `BitVisibility.Visible`                | Controls whether the component is visible, hidden, or collapsed.                                    |

### Public Members from BitComponentBase

| Name       | Type             | Default Value      | Description                                                                             |
|------------|------------------|--------------------|-----------------------------------------------------------------------------------------|
| UniqueId   | Guid             | `Guid.NewGuid()`   | Readonly unique identifier for the root element, generated upon component instantiation.|
| RootElement| ElementReference | (Not applicable)   | Reference to the root DOM element of the component.                                     |

---

## Enumerations

### BitVisibility Enum

Defines the visibility state of a component.

| Name      | Value | Description                                                                           |
|-----------|-------|---------------------------------------------------------------------------------------|
| Visible   | 0     | The component is fully visible.                                                       |
| Hidden    | 1     | The component is hidden, but the space it occupies remains (using CSS `visibility:hidden`). |
| Collapsed | 2     | The component is hidden and does not occupy space (using CSS `display:none`).           |

### BitDir Enum

Specifies the text direction for the component.

| Name | Value | Description                                                                                                               |
|------|-------|---------------------------------------------------------------------------------------------------------------------------|
| Ltr  | 0     | Left-to-right: Use for languages written from left to right (e.g., English).                                              |
| Rtl  | 1     | Right-to-left: Use for languages written from right to left (e.g., Arabic).                                               |
| Auto | 2     | Auto: The user agent determines the direction based on the content’s character analysis.                                 |

---