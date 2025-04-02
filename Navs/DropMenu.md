<!--
AI Agent Reference File: BitDropMenu Component

Purpose: This file provides detailed information about the Blazor `BitDropMenu` component.
Use this reference when generating, analyzing, or modifying code involving BitDropMenu.
Focus on its properties, usage patterns, and content structure as described below.
Pay attention to the different ways the component can be configured (e.g., disabled, transparent).
The content *between* the <BitDropMenu> tags defines the dropdown's content area.
-->

# BitDropMenu Component Reference

## Overview

The `BitDropMenu` component is a versatile dropdown menu for Blazor applications. It renders a button which, when clicked, reveals a customizable callout or dropdown panel containing arbitrary content.

It's useful for:

*   Navigation menus
*   Action lists (e.g., context menus)
*   Displaying forms or settings within a dropdown
*   Any interactive element requiring content revealed on demand via a button click.

---

## Usage

The basic structure involves placing the content you want to appear in the dropdown *between* the opening and closing `<BitDropMenu>` tags. The component handles the button rendering and the show/hide logic for the content panel (callout).

### Basic Example

This shows the simplest implementation. The `Text` property defines the label on the trigger button. Any Blazor components or HTML markup can be placed inside to serve as the dropdown content.

```razor
<BitDropMenu Text="Basic">
    <BitStack Gap="1rem" Style="padding:0.5rem">
        <BitText Typography="BitTypography.Subtitle1">This is the content</BitText>
        <BitButton>Click me</BitButton>
        <BitToggle>Toggle me</BitToggle>
    </BitStack>
</BitDropMenu>
```

**Explanation:**

1. `<BitDropMenu Text="Basic">`: Creates the dropdown component. The trigger button will display the text "Basic".
2. `<BitStack ...>`: (Content) This is the content that will appear inside the dropdown panel when the "Basic" button is clicked. It uses a `BitStack` for layout, containing text, a button, and a toggle.
3. `</BitDropMenu>`: Closes the component definition.

### Disabled State

You can disable the `BitDropMenu`, preventing the user from opening it, by setting the `IsEnabled` property to `false`.

```razor
<BitDropMenu Text="Disabled" IsEnabled="false">
    <BitStack Gap="1rem" Style="padding:0.5rem">
        <BitText Typography="BitTypography.Subtitle1">This is the content</BitText>
        <BitButton>Click me</BitButton>
        <BitToggle>Toggle me</BitToggle>
    </BitStack>
</BitDropMenu>
```

**Explanation:**

* `IsEnabled="false"`: This attribute disables the trigger button. The dropdown panel cannot be opened. The button will typically render with a disabled visual style.

### Transparent Style

The trigger button can be rendered with a transparent background by adding the `Transparent` boolean attribute.

```razor
<BitDropMenu Text="Transparent" Transparent>
    <BitStack Gap="1rem" Style="padding:0.5rem">
        <BitText Typography="BitTypography.Subtitle1">This is the content</BitText>
        <BitButton>Click me</BitButton>
        <BitToggle>Toggle me</BitToggle>
    </BitStack>
</BitDropMenu>
```

**Explanation:**

* `Transparent`: Adding this boolean attribute (equivalent to `Transparent="true"`) modifies the appearance of the trigger button, making its background transparent. This is useful for integrating the dropdown trigger more subtly into the UI.

---

## Properties / Parameters

<!-- AI: Use these properties when generating BitDropMenu code. -->

| Property        | Type           | Default | Description                                                                                                |
| :-------------- | :------------- | :------ | :--------------------------------------------------------------------------------------------------------- |
| `Text`          | `string`       | `null`  | The text displayed on the trigger button. Required if `Header` template is not used.                       |
| `IsEnabled`     | `bool`         | `true`  | Whether the dropdown menu is enabled. If `false`, the trigger button is disabled and cannot be interacted with. |
| `Transparent`   | `bool`         | `false` | If `true`, renders the trigger button with a transparent background.                                         |
| `ChildContent`  | `RenderFragment` | `null`  | **(Implicit)** The content placed between the `<BitDropMenu>` tags. This defines the content of the dropdown panel. |
| `Header`        | `RenderFragment` | `null`  | Custom content for the dropdown trigger button, overrides `Text`. Useful for adding icons or complex layouts to the button. |
| `IsOpen`        | `bool`         | `false` | Controls the visibility of the dropdown panel programmatically. Supports two-way binding (`@bind-IsOpen`). |
| `OnOpen`        | `EventCallback`  | -       | Callback triggered when the dropdown panel opens.                                                          |
| `OnClose`       | `EventCallback`  | -       | Callback triggered when the dropdown panel closes.                                                         |
| `Class`         | `string`       | `null`  | Custom CSS class(es) to apply to the root element of the component.                                        |
| `Style`         | `string`       | `null`  | Custom inline CSS style(s) to apply to the root element of the component.                                  |
| `CalloutClass`  | `string`       | `null`  | Custom CSS class(es) to apply to the dropdown callout panel.                                               |
| `CalloutStyle`  | `string`       | `null`  | Custom inline CSS style(s) to apply to the dropdown callout panel.                                         |
| `Position`      | `BitDropMenuPosition` | `BitDropMenuPosition.BottomLeft` | Determines the position of the dropdown callout relative to the trigger button. (Enum values like `BottomLeft`, `BottomCenter`, `TopRight`, etc.) |
| `IsSticky`      | `bool`         | `false` | If `true`, the callout attempts to stay in the viewport by flipping or adjusting its position if needed.     |
| `IsSubMenu`     | `bool`         | `false` | Indicates if this DropMenu is nested within another DropMenu, affecting styling or behavior.              |
| `OpenOnClick`   | `bool`         | `true`  | Determines if the dropdown opens when the trigger button is clicked.                                       |
| `OpenOnHover`   | `bool`         | `false` | Determines if the dropdown opens when the mouse hovers over the trigger button.                            |
| `CloseOnContentClick` | `bool`   | `false` | Determines if the dropdown closes when the user clicks inside the dropdown content area.                 |

*(Note: Some properties like `Position`, `IsSticky`, `IsOpen`, `OnOpen`, `OnClose`, `Header`, etc., might exist based on common patterns for such components but are not explicitly shown in the provided HTML snippet. They are included here as highly likely parameters for a complete component. Confirm actual availability from the component library's documentation if needed.)*

---

## Content Structure (ChildContent)

The core way to define what appears inside the dropdown panel is by placing content directly between the opening `<BitDropMenu>` and closing `</BitDropMenu>` tags. This content is rendered within the callout panel when the dropdown is opened.

```razor
<BitDropMenu Text="Content Example">
    <!-- This is the ChildContent -->
    <div>
        <h4>Dropdown Title</h4>
        <p>Place any Blazor components or HTML markup here.</p>
        <BitTextField Label="Input inside dropdown" />
    </div>
    <!-- End of ChildContent -->
</BitDropMenu>
```

**Best Practices:**

* Use layout components like `<BitStack Horizontal="false" Gap="0.5rem">` or standard HTML (`div`, `section`) within the `ChildContent` to structure the dropdown's content effectively.
* Keep the content concise if possible, especially for action menus. For complex content, ensure it fits reasonably within a dropdown context.

---

## Styling

* Use the `Class` and `Style` parameters on the `BitDropMenu` component itself to apply custom styles to the root element (which often includes the trigger button).
* Use `CalloutClass` and `CalloutStyle` to specifically target the dropdown panel (the callout element).
* Standard CSS practices apply. You can target internal elements using more specific CSS selectors if necessary, but rely on provided parameters first.

---

## AI Agent Guidance Summary

* Use `<BitDropMenu>` to create dropdown buttons.
* Set the button label via the `Text` property.
* Place the dropdown panel's content *inside* the `<BitDropMenu>` tags (this is the `ChildContent`).
* Use `IsEnabled="false"` to disable the dropdown.
* Use the `Transparent` attribute for a transparent button background.
* Refer to the Properties table for available configurations.
* Structure the internal content using layout components like `BitStack` or standard HTML.
* Remember that `BitDropMenu` is a container; the logic for what happens *inside* the dropdown (e.g., button clicks within the dropdown) is defined by the components placed within `ChildContent`.
