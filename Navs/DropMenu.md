# DropMenu Component Reference

This document serves as a comprehensive guide to the **DropMenu** component. It is designed for Blazor applications and explains how to implement and customize the dropdown menu. Use this reference file for integrating DropMenu in your projects, similar to how you’d use cursor rules or GitHub Copilot reference files.

---

## Overview

**DropMenu** is a versatile dropdown menu component that allows you to create a button which, when clicked, opens a callout or dropdown menu. This makes it ideal for building navigation menus, action lists, or any interactive element that requires a dropdown. Its flexible design and extensive customization options make it easy to integrate into your UI.

---

## Usage

### Basic Example

The following example demonstrates a basic implementation of the DropMenu. In this example, a button labeled **"Basic"** is used as the trigger. When clicked, it opens a dropdown callout that displays custom content.

```html
<div id="0by5hh" type="button" class="bit-drm" tabindex="0">
  <!-- DropMenu Button -->
  <button type="button" class="bit-drm-btn">
    <div class="bit-drm-txt">Basic</div>
    <i class="bit-icon bit-icon--ChevronRight bit-ico-r90"></i>
  </button>
  
  <!-- Hidden overlay (for click outside detection, etc.) -->
  <div style="display:none;" class="bit-drm-ovl"></div>
  
  <!-- Dropdown Callout -->
  <div id="BitDropMenu-0by5hh-callout" class="bit-drm-cal">
    <div style="display: flex; flex-direction: column; gap: 1rem; padding: 0.5rem" class="bit-stc">
      <h6 class="bit-txt bit-txt-subtitle1">This is the content</h6>
      <button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md" type="button">
        <div class="bit-btn-tcn">
          <div class="bit-btn-prt">Click me</div>
        </div>
      </button>
    </div>
  </div>
</div>
```

### Explanation

- **Root Container (`bit-drm`):**  
  This is the main container for the DropMenu and acts as the trigger. It’s assigned a `tabindex="0"` so that it can receive keyboard focus.

- **Button Element (`bit-drm-btn`):**  
  The clickable button contains:
  - A text label (inside `bit-drm-txt`) displaying "Basic".
  - An icon (using classes `bit-icon--ChevronRight` and `bit-ico-r90`) indicating that this element is a dropdown.

- **Overlay (`bit-drm-ovl`):**  
  This hidden element is used for detecting clicks outside the menu to close it when necessary.

- **Callout Container (`bit-drm-cal`):**  
  This section holds the dropdown content. In the example, it contains a subtitle and an additional button. The callout content is styled with flex properties to arrange its elements vertically with spacing.

---

## API Reference

Below is a summary of the primary properties and events available for the DropMenu component:

| Name           | Type                   | Default                  | Description                                                                              |
| -------------- | ---------------------- | ------------------------ | ---------------------------------------------------------------------------------------- |
| `ChildContent` | `RenderFragment?`      | `null`                   | The content that appears within the dropdown callout.                                    |
| `IsOpen`       | `bool`                 | `false`                  | Indicates whether the dropdown menu is currently open.                                   |
| `OnToggle`     | `EventCallback<bool>`  |                          | Callback that is invoked when the dropdown menu opens or closes.                         |
| `CssClass`     | `string?`              | `null`                   | Custom CSS classes for additional styling of the DropMenu container.                      |
| `Style`        | `string?`              | `null`                   | Inline styles for the DropMenu container.                                                |

*For a full API reference, please consult the component source code or the official documentation.*

---

## Customization

### Styling

You can tailor the appearance of the DropMenu by:

- **CSS Classes:** Use the `CssClass` parameter to add custom classes.
- **Inline Styles:** Override default styles with the `Style` parameter.
- **Element-specific Customization:** Override or extend the styles of sub-elements such as the callout container (`bit-drm-cal`), button (`bit-drm-btn`), or text (`bit-drm-txt`).

### Behavior

- **Toggling:**  
  The DropMenu is designed to toggle open and closed on button click. You can manage the open state using the `IsOpen` property and respond to state changes with the `OnToggle` event callback.

- **Content Flexibility:**  
  By providing your own `ChildContent`, you can populate the dropdown with any interactive elements such as lists, forms, or additional buttons.

---

## Accessibility

- **Keyboard Navigation:**  
  Ensure that the DropMenu trigger is focusable (using `tabindex`) so that users can open the menu via keyboard.
- **Aria Attributes:**  
  Consider adding appropriate `aria` attributes to the button and callout elements to improve screen reader support.
- **Focus Management:**  
  Properly manage focus when the menu is opened or closed, so that keyboard users have a smooth navigation experience.

---