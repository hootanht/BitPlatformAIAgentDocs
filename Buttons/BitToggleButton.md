# BitToggleButton Component Reference

This document provides a comprehensive reference for the `BitToggleButton` component. It is intended for developers and AI agents alike and covers everything from basic usage to advanced customization, API details, and event handling.

---

## Overview

**ToggleButton** is a type of button that stores and displays a status representing the toggle state of a feature (e.g., muting/unmuting audio). This component offers multiple visual variants, sizes, color themes, and customization options, making it adaptable to diverse UI requirements.

---

## Usage

### Basic

The simplest example of a ToggleButton uses an icon and text to indicate the state (e.g., "Unmuted"). For example:

```html
<button class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-fil" type="button">
  <i class="bit-tgb-ico bit-icon bit-icon--Microphone"></i>
  <span class="bit-tgb-btx">Unmuted</span>
</button>
```

---

### Variant

The ToggleButton supports three visual variants:

- **Fill** (default)
- **Outline**
- **Text**

**Enabled Examples:**

```html
<button class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-fil" type="button">Fill</button>
<button class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-otl" type="button">Outline</button>
<button class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-txt" type="button">Text</button>
```

**Disabled Examples:**

```html
<button class="bit-tgb bit-dis bit-tgb-pri bit-tgb-md bit-tgb-fil" type="button" tabindex="-1">Fill</button>
<button class="bit-tgb bit-dis bit-tgb-pri bit-tgb-md bit-tgb-otl" type="button" tabindex="-1">Outline</button>
<button class="bit-tgb bit-dis bit-tgb-pri bit-tgb-md bit-tgb-txt" type="button" tabindex="-1">Text</button>
```

---

### Size

ToggleButton sizes can be adjusted to fit your design needs.

**Fill Variant:**

```html
<button class="bit-tgb bit-tgb-pri bit-tgb-sm bit-tgb-fil" type="button">Small</button>
<button class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-fil" type="button">Medium</button>
<button class="bit-tgb bit-tgb-pri bit-tgb-lg bit-tgb-fil" type="button">Large</button>
```

**Outline Variant:**

```html
<button class="bit-tgb bit-tgb-pri bit-tgb-sm bit-tgb-otl" type="button">Small</button>
<button class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-otl" type="button">Medium</button>
<button class="bit-tgb bit-tgb-pri bit-tgb-lg bit-tgb-otl" type="button">Large</button>
```

**Text Variant:**

```html
<button class="bit-tgb bit-tgb-pri bit-tgb-sm bit-tgb-txt" type="button">Small</button>
<button class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-txt" type="button">Medium</button>
<button class="bit-tgb bit-tgb-pri bit-tgb-lg bit-tgb-txt" type="button">Large</button>
```

---

### Color

The toggle button offers a wide range of color variants to indicate state and hierarchy:

- **Primary**
- **Secondary**
- **Tertiary**
- **Info**
- **Success**
- **Warning**
- **SevereWarning**
- **Error**
- **Background Colors**: PrimaryBackground, SecondaryBackground, TertiaryBackground
- **Foreground Colors**: PrimaryForeground, SecondaryForeground, TertiaryForeground
- **Border Colors**: PrimaryBorder, SecondaryBorder, TertiaryBorder

**Example:**

```html
<!-- Primary color -->
<button class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-fil" type="button">Primary</button>

<!-- Secondary color -->
<button class="bit-tgb bit-tgb-sec bit-tgb-md bit-tgb-fil" type="button">Secondary</button>

<!-- Tertiary color -->
<button class="bit-tgb bit-tgb-ter bit-tgb-md bit-tgb-fil" type="button">Tertiary</button>

<!-- Disabled example -->
<button class="bit-tgb bit-dis bit-tgb-pri bit-tgb-md bit-tgb-fil" type="button" tabindex="-1">Primary</button>
```

---

### Style & Class

Override the default styles and classes to tailor the appearance of the ToggleButton.

**Inline Styling Example:**

```html
<button style="background-color: transparent; border-color: blueviolet; color: blueviolet;"
        class="bit-tgb bit-tgb-pri bit-tgb-md bit-tgb-otl" type="button">
  <i class="bit-tgb-ico bit-icon bit-icon--Microphone"></i>
  <span class="bit-tgb-btx">Styled Button: Unmuted</span>
</button>
```

**Using Custom Classes:**

```html
<button class="bit-tgb custom-class bit-tgb-pri bit-tgb-md bit-tgb-fil" type="button">
  <i class="bit-tgb-ico bit-icon bit-icon--Microphone"></i>
  <span class="bit-tgb-btx">Classed Button: Unmuted</span>
</button>
```

You can also customize the internal parts (icon, text, etc.) by overriding the default CSS using the component’s style and class properties.

---

### Binding

The `BitToggleButton` supports various binding scenarios:

#### Default Checked State

Set the initial checked state with `DefaultIsChecked`:

```razor
<BitToggleButton DefaultIsChecked="true" />
```

#### Two-Way Binding

Bind the checked state to a property:

```razor
<BitToggleButton @bind-IsChecked="isMuted" OnChange="OnToggleChanged" />

@code {
  private bool isMuted = false;
  private void OnToggleChanged(bool newValue)
  {
    isMuted = newValue;
    // Handle the state change here...
  }
}
```

#### Handling Change Events

Display or react to changes in the toggle state:

```razor
<label>Check status is: @isMuted</label>
<BitToggleButton IsChecked="@isMuted" OnChange="@((bool value) => isMuted = value)" />
```

---

### Templates

Override default templates to further customize the ToggleButton appearance.

```razor
<BitToggleButton>
  <HeaderTemplate>
    <div style="font-weight: bold;">Custom Toggle Header</div>
  </HeaderTemplate>
  <ChildContent>
    <BitToggleButtonOption Text="Option 1" />
    <BitToggleButtonOption Text="Option 2" />
  </ChildContent>
</BitToggleButton>
```

---

### Events

Manage the events triggered by the ToggleButton.

**OnClick Event:**

```razor
<BitToggleButton OnClick="HandleToggleClick">
  <!-- Button content -->
</BitToggleButton>

@code {
  private void HandleToggleClick(MouseEventArgs e)
  {
    // Process the click event
  }
}
```

**OnChange Event:**

Use the `OnChange` event to react when the checked state changes.

---

### RTL (Right-to-Left)

For languages that require a right-to-left layout, use the `dir` attribute or set the `Dir` parameter:

```razor
<BitToggleButton dir="rtl" Text="صدا وصل">
  <BitToggleButtonOption Text="گزینه ۱" />
  <BitToggleButtonOption Text="گزینه ۲" />
</BitToggleButton>
```

---

## API Reference

### BitToggleButton Parameters

| **Name**              | **Type**                           | **Default Value**           | **Description**                                                                                   |
|-----------------------|------------------------------------|-----------------------------|---------------------------------------------------------------------------------------------------|
| `AllowDisabledFocus`  | `bool`                           | `false`                     | Determines whether the toggle button can receive focus when disabled.                             |
| `AriaDescription`     | `string?`                        | `null`                      | Detailed description for screen readers.                                                         |
| `AriaHidden`          | `bool`                           | `false`                     | If true, adds an `aria-hidden` attribute so screen readers ignore the button.                      |
| `ChildContent`        | `RenderFragment?`                | `null`                      | Content to display inside the toggle button.                                                     |
| `Classes`             | `BitToggleButtonClassStyles?`    | `null`                      | Custom CSS classes for various parts of the toggle button.                                        |
| `Color`               | `BitColor?`                      | `null`                      | Sets the general color theme of the toggle button.                                               |
| `DefaultIsChecked`    | `bool?`                         | `null`                      | The initial checked state of the toggle button.                                                  |
| `IconName`            | `string?`                        | `null`                      | Icon displayed when the toggle button is in its default state.                                   |
| `IsChecked`           | `bool`                           | `false`                     | Indicates whether the toggle button is checked.                                                  |
| `OnChange`            | `EventCallback<bool>`            | —                           | Callback invoked when the `IsChecked` state changes.                                             |
| `OnClick`             | `EventCallback<MouseEventArgs>`  | —                           | Callback invoked when the toggle button is clicked.                                              |
| `OffIconName`         | `string?`                        | `null`                      | Icon displayed when the toggle button is not checked.                                            |
| `OffText`             | `string?`                        | `null`                      | Text displayed when the toggle button is not checked.                                            |
| `OffTitle`            | `string?`                        | `null`                      | Tooltip text when the toggle button is not checked.                                              |
| `OnIconName`          | `string?`                        | `null`                      | Icon displayed when the toggle button is checked.                                                |
| `OnText`              | `string?`                        | `null`                      | Text displayed when the toggle button is checked.                                                |
| `OnTitle`             | `string?`                        | `null`                      | Tooltip text when the toggle button is checked.                                                  |
| `Size`                | `BitSize?`                       | `null`                      | The size of the toggle button (Small, Medium, Large).                                            |
| `Styles`              | `BitToggleButtonClassStyles?`    | `null`                      | Custom CSS styles for various parts of the toggle button.                                        |
| `Text`                | `string?`                        | `null`                      | The text label of the toggle button.                                                             |
| `Title`               | `string?`                        | `null`                      | Tooltip text for the toggle button.                                                              |
| `Variant`             | `BitVariant?`                    | `null`                      | Visual variant of the toggle button (Fill, Outline, Text).                                       |

### BitComponentBase Parameters

Inherited from the base component:

| **Name**         | **Type**                           | **Default Value**                        | **Description**                                                                   |
|------------------|------------------------------------|------------------------------------------|-----------------------------------------------------------------------------------|
| `AriaLabel`      | `string?`                          | `null`                                   | Aria-label for the component.                                                     |
| `Class`          | `string?`                          | `null`                                   | Custom CSS class for the root element.                                            |
| `Dir`            | `BitDir?`                          | `null`                                   | Specifies the component direction (LTR, RTL, Auto).                              |
| `HtmlAttributes` | `Dictionary<string, object>`       | `new Dictionary<string, object>()`       | Additional HTML attributes for the root element.                                  |
| `Id`             | `string?`                          | `null`                                   | Custom id; if null, a unique id is generated.                                     |
| `IsEnabled`      | `bool`                             | `true`                                   | Indicates whether the component is enabled.                                       |
| `Style`          | `string?`                          | `null`                                   | Inline CSS styles for the component.                                              |
| `Visibility`     | `BitVisibility`                    | `BitVisibility.Visible`                  | Visibility state (Visible, Hidden, Collapsed).                                    |

### Public Members (BitComponentBase)

| **Name**     | **Type**             | **Default Value**         | **Description**                                                     |
|--------------|----------------------|---------------------------|---------------------------------------------------------------------|
| `UniqueId`   | `Guid`               | `Guid.NewGuid()`          | Read-only unique id assigned during component construction.        |
| `RootElement`| `ElementReference`   | —                         | Reference to the component's root HTML element.                     |

### BitToggleButtonClassStyles Properties

Customize internal styling of the toggle button:

| **Name**  | **Type**  | **Default Value** | **Description**                                                         |
|-----------|-----------|-------------------|-------------------------------------------------------------------------|
| `Root`    | `string?` | `null`            | Custom CSS classes/styles for the root element.                         |
| `Checked` | `string?` | `null`            | Styles for the checked state.                                           |
| `Icon`    | `string?` | `null`            | Styles for the icon element.                                            |
| `Text`    | `string?` | `null`            | Styles for the text element.                                            |

---

## Enumerations

### BitButtonType Enum

| **Name**  | **Value** | **Description**                     |
|-----------|-----------|-------------------------------------|
| `Button`  | `0`       | Standard clickable button.          |
| `Submit`  | `1`       | A button that submits form data.    |
| `Reset`   | `2`       | A button that resets form data.     |

### BitColor Enum

| **Name**              | **Value** | **Description**                                    |
|-----------------------|-----------|----------------------------------------------------|
| `Primary`             | `0`       | Primary (default) color.                           |
| `Secondary`           | `1`       | Secondary color.                                   |
| `Tertiary`            | `2`       | Tertiary color.                                    |
| `Info`                | `3`       | Info color.                                        |
| `Success`             | `4`       | Success color.                                     |
| `Warning`             | `5`       | Warning color.                                     |
| `SevereWarning`       | `6`       | Severe warning color.                              |
| `Error`               | `7`       | Error color.                                       |
| `PrimaryBackground`   | `8`       | Primary background color.                          |
| `SecondaryBackground` | `9`       | Secondary background color.                        |
| `TertiaryBackground`  | `10`      | Tertiary background color.                         |
| `PrimaryForeground`   | `11`      | Primary foreground color.                          |
| `SecondaryForeground` | `12`      | Secondary foreground color.                        |
| `TertiaryForeground`  | `13`      | Tertiary foreground color.                         |
| `PrimaryBorder`       | `14`      | Primary border color.                              |
| `SecondaryBorder`     | `15`      | Secondary border color.                            |
| `TertiaryBorder`      | `16`      | Tertiary border color.                             |

### BitSize Enum

| **Name**  | **Value** | **Description**           |
|-----------|-----------|---------------------------|
| `Small`   | `0`       | Small size.               |
| `Medium`  | `1`       | Medium size (default).    |
| `Large`   | `2`       | Large size.               |

### BitVariant Enum

| **Name**  | **Value** | **Description**             |
|-----------|-----------|-----------------------------|
| `Fill`    | `0`       | Fill style variant.         |
| `Outline` | `1`       | Outline style variant.      |
| `Text`    | `2`       | Text style variant.         |

### BitVisibility Enum

| **Name**    | **Value** | **Description**                                                 |
|-------------|-----------|-----------------------------------------------------------------|
| `Visible`   | `0`       | The component is visible.                                       |
| `Hidden`    | `1`       | The component is hidden (using `visibility: hidden`).           |
| `Collapsed` | `2`       | The component is collapsed (using `display: none`).             |

### BitDir Enum

| **Name** | **Value** | **Description**                                                                        |
|----------|-----------|----------------------------------------------------------------------------------------|
| `Ltr`    | `0`       | Left-to-right direction (for languages like English).                                  |
| `Rtl`    | `1`       | Right-to-left direction (for languages like Arabic).                                   |
| `Auto`   | `2`       | Automatically determines direction based on the content.                               |

---