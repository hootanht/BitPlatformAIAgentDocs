# ButtonGroup Component Reference

The **ButtonGroup** component is used to group related buttons together. It provides multiple APIs for supplying its items (using the BitButtonGroupItem class, a custom generic, or the BitButtonGroupOption component) and supports various visual variants, sizes, colors, and layout options (horizontal, vertical, full-width, RTL, etc.). This reference covers its usage, customization, API parameters, and the enumerated types used to control its behavior and appearance.

---

## Overview

ButtonGroup allows you to combine buttons into a single, cohesive unit. Use it when you want to:
- Present a set of related actions (such as **Add**, **Edit**, **Delete**).
- Enable toggle behavior for selecting one of many options.
- Ensure consistent spacing and styling across a collection of buttons.

---

## Notes

- **Multi-API Support:**  
  The ButtonGroup supports three different item APIs:
  1. Using the **BitButtonGroupItem** class.
  2. A custom generic item.
  3. The **BitButtonGroupOption** component.
- This flexibility allows you to choose the approach that best suits your data model and UI needs.

---

## Usage

### Basic Usage

Place your buttons inside the ButtonGroup component to group them together. In its simplest form, the ButtonGroup renders a toolbar of buttons:

```html
<!-- A basic ButtonGroup with three buttons -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md">
  <button tabindex="0" class="bit-btg-itm">
    <span class="bit-btg-btx">Add</span>
  </button>
  <button tabindex="0" class="bit-btg-itm">
    <span class="bit-btg-btx">Edit</span>
  </button>
  <button tabindex="0" class="bit-btg-itm">
    <span class="bit-btg-btx">Delete</span>
  </button>
</div>
```

### Variants

The ButtonGroup can be rendered in different visual styles:

- **Fill (Default):** Uses filled background styling.
- **Outline:** Renders with an outline.
- **Text:** Displays as text-only buttons.

For example:

```html
<!-- Fill variant (default) -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md">
  <button class="bit-btg-itm"><span class="bit-btg-btx">Add</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Edit</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Delete</span></button>
</div>

<!-- Outline variant -->
<div role="group" class="bit-btg bit-btg-otl bit-btg-pri bit-btg-md">
  <button class="bit-btg-itm"><span class="bit-btg-btx">Add</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Edit</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Delete</span></button>
</div>

<!-- Text variant -->
<div role="group" class="bit-btg bit-btg-txt bit-btg-pri bit-btg-md">
  <button class="bit-btg-itm"><span class="bit-btg-btx">Add</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Edit</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Delete</span></button>
</div>
```

### Icon and IconOnly

Each button within a group can display an icon. You may choose to show both an icon and text or set the button to “icon-only” mode for a more minimalistic design.

```html
<!-- ButtonGroup with icons -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md">
  <button class="bit-btg-itm">
    <i class="bit-icon bit-icon--Add"></i>
    <span class="bit-btg-btx">Add</span>
  </button>
  <button class="bit-btg-itm">
    <i class="bit-icon bit-icon--Edit"></i>
    <span class="bit-btg-btx">Edit</span>
  </button>
  <button class="bit-btg-itm">
    <i class="bit-icon bit-icon--Delete"></i>
    <span class="bit-btg-btx">Delete</span>
  </button>
</div>

<!-- IconOnly ButtonGroup (no text) -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md">
  <button class="bit-btg-itm">
    <i class="bit-icon bit-icon--Add"></i>
  </button>
  <button class="bit-btg-itm">
    <i class="bit-icon bit-icon--Edit"></i>
  </button>
  <button class="bit-btg-itm">
    <i class="bit-icon bit-icon--Delete"></i>
  </button>
</div>
```

### ReversedIcon

When needed, you can reverse the position of the icon and the text inside a button by enabling the reversed icon mode:

```html
<!-- Reversed Icon: icon appears after text -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md">
  <button tabindex="0" class="bit-btg-itm bit-btg-rvi">
    <span class="bit-btg-btx">Add</span>
    <i class="bit-icon bit-icon--Add"></i>
  </button>
</div>
```

### Toggle Mode

The ButtonGroup can also be set into toggle mode. In this mode, each button behaves like a toggle switch and provides visual feedback on its active/inactive state.

```html
<!-- ButtonGroup with toggle behavior -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md">
  <button class="bit-btg-itm" onclick="onItemClick('Add')">
    <span class="bit-btg-btx">Add</span>
  </button>
  <button class="bit-btg-itm" onclick="onItemClick('Edit')">
    <span class="bit-btg-btx">Edit</span>
  </button>
  <button class="bit-btg-itm" onclick="onItemClick('Delete')">
    <span class="bit-btg-btx">Delete</span>
  </button>
</div>
```

*Note:* The toggle behavior is enabled by setting the `Toggle` property to true.

### Vertical Orientation

By default, the ButtonGroup renders horizontally. To display items vertically, set the `Vertical` property to true.

```html
<!-- Vertical ButtonGroup -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md bit-btg-vrt">
  <button class="bit-btg-itm"><span class="bit-btg-btx">Add</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Edit</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Delete</span></button>
</div>
```

### Events

The ButtonGroup supports events at two levels:

- **Group-level ItemClick:** Triggered when any button in the group is clicked.
- **Individual Item's Click:** Each item can have its own click event handler.

```html
<!-- Example: ButtonGroup with item click event -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md" onclick="onGroupItemClick(event)">
  <button class="bit-btg-itm"><span class="bit-btg-btx">Add</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Edit</span></button>
  <button class="bit-btg-itm"><span class="bit-btg-btx">Delete</span></button>
</div>
<script>
  function onGroupItemClick(e) {
    // Handle the click event here (e.g., determine which item was clicked)
    console.log('Item clicked:', e.target.innerText);
  }
</script>
```

### Size

The ButtonGroup supports different sizes. You can choose from Small, Medium, and Large to suit your design needs.

```html
<!-- Small ButtonGroup -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-sm">
  <!-- Items -->
</div>

<!-- Medium ButtonGroup (default) -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md">
  <!-- Items -->
</div>

<!-- Large ButtonGroup -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-lg">
  <!-- Items -->
</div>
```

### FullWidth

Setting the `FullWidth` property expands the ButtonGroup so that it occupies 100% of its container’s width.

```html
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md bit-btg-flw">
  <!-- Items -->
</div>
```

### Color

The ButtonGroup supports themed color variations. You can specify a general color (Primary, Secondary, Tertiary, Info, etc.) to provide consistent visual cues.

```html
<!-- Primary color ButtonGroup -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-pri bit-btg-md">
  <!-- Items -->
</div>

<!-- Secondary color ButtonGroup -->
<div role="group" class="bit-btg bit-btg-fil bit-btg-sec bit-btg-md">
  <!-- Items -->
</div>
```

### RTL (Right-to-Left)

For languages that are read from right-to-left, set the container’s `dir="rtl"` attribute and add the `bit-rtl` class to the ButtonGroup.

```html
<div dir="rtl">
  <div role="group" class="bit-btg bit-rtl bit-btg-fil bit-btg-pri bit-btg-md" dir="rtl">
    <button class="bit-btg-itm">
      <i class="bit-icon bit-icon--Add"></i>
      <span class="bit-btg-btx">اضافه کردن</span>
    </button>
    <button class="bit-btg-itm">
      <i class="bit-icon bit-icon--Edit"></i>
      <span class="bit-btg-btx">ویرایش</span>
    </button>
    <button class="bit-btg-itm">
      <i class="bit-icon bit-icon--Delete"></i>
      <span class="bit-btg-btx">حذف</span>
    </button>
  </div>
</div>
```

---

## API Reference

### BitButtonGroup Parameters

| **Name**          | **Type**                                       | **Default Value**             | **Description**                                                                                                   |
|-------------------|------------------------------------------------|-------------------------------|-------------------------------------------------------------------------------------------------------------------|
| ChildContent      | `RenderFragment?`                              | `null`                        | The content for the ButtonGroup. Typically, a collection of **BitButtonGroupOption** components.                  |
| IconOnly          | `bool`                                         | `false`                       | If true, renders the ButtonGroup items as icons only (without text).                                               |
| Classes           | `BitButtonGroupClassStyles?`                   | `null`                        | Custom CSS classes for different parts of the ButtonGroup.                                                        |
| Color             | `BitColor?`                                    | `null`                        | The overall color theme for the ButtonGroup.                                                                      |
| FullWidth         | `bool`                                         | `false`                       | Expands the ButtonGroup to occupy 100% of its container's width.                                                    |
| Items             | `IEnumerable<TItem>`                           | `new List<TItem>()`           | A list of items for the ButtonGroup. Items can be rendered using a custom template or one of the supported item types.|
| ItemTemplate      | `RenderFragment<TItem>?`                       | `null`                        | Template for rendering each item.                                                                                 |
| NameSelectors     | `BitButtonGroupNameSelectors<TItem>?`          | `null`                        | Selectors to extract specific fields from the item (e.g., class names).                                             |
| OnItemClick       | `EventCallback<TItem>`                         |                               | Callback triggered when an item in the ButtonGroup is clicked.                                                    |
| Options           | `RenderFragment?`                              | `null`                        | Alias for ChildContent, used when rendering **BitButtonGroupOption** components.                                  |
| Toggle            | `bool`                                         | `false`                       | Enables toggle mode for each button in the group.                                                                 |
| Size              | `BitSize?`                                     | `null`                        | The size of the ButtonGroup (Small, Medium, Large).                                                                 |
| Styles            | `BitButtonGroupClassStyles?`                   | `null`                        | Inline CSS styles for different parts of the ButtonGroup.                                                         |
| Variant           | `BitVariant?`                                  | `null`                        | Visual variant for the ButtonGroup (Fill, Outline, Text).                                                         |
| Vertical          | `bool`                                         | `false`                       | Renders the ButtonGroup items vertically if set to true.                                                          |

---

### BitComponentBase Parameters

| **Name**        | **Type**                         | **Default Value**                         | **Description**                                                                       |
|-----------------|----------------------------------|-------------------------------------------|---------------------------------------------------------------------------------------|
| AriaLabel       | `string?`                        | `null`                                    | Accessible label for screen readers.                                                  |
| Class           | `string?`                        | `null`                                    | Custom CSS class for the root element.                                                |
| Dir             | `BitDir?`                        | `null`                                    | Text direction (LTR, RTL, or Auto).                                                   |
| HtmlAttributes  | `Dictionary<string, object>`     | `new Dictionary<string, object>()`        | Additional HTML attributes for the component.                                         |
| Id              | `string?`                        | `null`                                    | Custom identifier for the component; if omitted, a unique ID is generated.              |
| IsEnabled       | `bool`                           | `true`                                    | Whether the component is enabled.                                                     |
| Style           | `string?`                        | `null`                                    | Inline CSS styles for the root element.                                               |
| Visibility      | `BitVisibility`                  | `BitVisibility.Visible`                   | Controls whether the component is visible, hidden, or collapsed.                        |

---

### BitButtonGroupItem Properties

These properties define the individual items in a ButtonGroup when using the BitButtonGroupItem API.

| **Name**       | **Type**         | **Default Value** | **Description**                                                                  |
|----------------|------------------|-------------------|----------------------------------------------------------------------------------|
| Class          | `string?`        | `null`            | Custom CSS classes for the item.                                                 |
| IconName       | `string?`        | `null`            | Name of the icon to render next to the item text.                                |
| IsEnabled      | `bool`           | `true`            | Determines if the item is enabled.                                               |
| Key            | `string?`        | `null`            | A unique key to identify the item.                                               |
| OffIconName    | `string?`        | `null`            | Icon to display when the item is not toggled on.                                 |
| OffText        | `string?`        | `null`            | Text to display when the item is not toggled on.                                 |
| OffTitle       | `string?`        | `null`            | Tooltip when the item is off.                                                    |
| OnIconName     | `string?`        | `null`            | Icon to display when the item is toggled on.                                     |
| OnText         | `string?`        | `null`            | Text to display when the item is toggled on.                                     |
| OnTitle        | `string?`        | `null`            | Tooltip when the item is on.                                                     |
| OnClick        | `EventCallback`  |                   | Click event handler for the item.                                                |
| ReversedIcon   | `bool`           | `false`           | Reverses the position of the icon and text.                                      |
| Style          | `string?`        | `null`            | Inline CSS styles for the item.                                                  |
| Template       | `RenderFragment<BitButtonGroupItem>?` | `null` | Custom template for the item.                                                    |
| Text           | `string?`        | `null`            | The display text for the item.                                                   |
| Title          | `string?`        | `null`            | The tooltip or title text for the item.                                          |

---

### BitButtonGroupOption Properties

When using the BitButtonGroupOption API, the following properties are available:

| **Name**       | **Type**         | **Default Value** | **Description**                                                                  |
|----------------|------------------|-------------------|----------------------------------------------------------------------------------|
| Class          | `string?`        | `null`            | Custom CSS classes for the option.                                               |
| IconName       | `string?`        | `null`            | Name of the icon to display next to the option text.                             |
| IsEnabled      | `bool`           | `true`            | Whether the option is enabled.                                                   |
| Key            | `string?`        | `null`            | Unique key for the option.                                                       |
| OffIconName    | `string?`        | `null`            | Icon displayed when the option is not active (toggle mode off).                    |
| OffText        | `string?`        | `null`            | Text displayed when the option is not active.                                    |
| OffTitle       | `string?`        | `null`            | Tooltip when the option is off.                                                  |
| OnIconName     | `string?`        | `null`            | Icon displayed when the option is active (toggle mode on).                        |
| OnText         | `string?`        | `null`            | Text displayed when the option is active.                                        |
| OnTitle        | `string?`        | `null`            | Tooltip when the option is active.                                               |
| OnClick        | `EventCallback`  |                   | Click event handler for the option.                                              |
| ReversedIcon   | `bool`           | `false`           | Reverses the icon and text order.                                                |
| Style          | `string?`        | `null`            | Inline CSS styles for the option.                                                |
| Template       | `RenderFragment<BitButtonGroupOption>?` | `null` | Custom template for the option.                                                  |
| Text           | `string?`        | `null`            | Display text for the option.                                                     |
| Title          | `string?`        | `null`            | Tooltip for the option.                                                          |

---

### BitButtonGroupClassStyles Properties

Customize the ButtonGroup styling with these properties:

| **Name**   | **Type**  | **Default Value** | **Description**                                                                  |
|------------|-----------|-------------------|----------------------------------------------------------------------------------|
| Root       | `string?` | `null`            | Custom CSS classes/styles for the root element of the ButtonGroup.               |
| Button     | `string?` | `null`            | Custom CSS classes/styles for the internal button element.                       |
| Icon       | `string?` | `null`            | Custom CSS classes/styles for the icon within the ButtonGroup.                   |
| Text       | `string?` | `null`            | Custom CSS classes/styles for the text content within the ButtonGroup.           |
| ToggledButton | `string?` | `null`         | Custom CSS classes/styles for the button when in toggle mode.                    |

---

### BitButtonGroupNameSelectors Properties

Use these to map your custom item data to the properties required by the ButtonGroup.

| **Name**    | **Type**                                    | **Default Value**                           | **Description**                                                |
|-------------|---------------------------------------------|---------------------------------------------|----------------------------------------------------------------|
| Name        | `string`                                    | —                                           | The property name for the custom class.                        |
| Selector    | `Func<TItem, TProp?>?`                       | —                                           | A function to extract the property value from the item.         |

---

## Enumerations

### BitVariant

| **Name**  | **Value** | **Description**                  |
|-----------|-----------|----------------------------------|
| Fill      | 0         | Default filled style.            |
| Outline   | 1         | Outline style variant.           |
| Text      | 2         | Text-only style variant.         |

### BitColor

| **Name**              | **Value** | **Description**                         |
|-----------------------|-----------|-----------------------------------------|
| Primary               | 0         | Primary theme color.                    |
| Secondary             | 1         | Secondary theme color.                  |
| Tertiary              | 2         | Tertiary theme color.                   |
| Info                  | 3         | Informational color.                    |
| Success               | 4         | Success color.                          |
| Warning               | 5         | Warning color.                          |
| SevereWarning         | 6         | Severe warning color.                   |
| Error                 | 7         | Error color.                            |
| PrimaryBackground     | 8         | Primary background color.               |
| SecondaryBackground   | 9         | Secondary background color.             |
| TertiaryBackground    | 10        | Tertiary background color.              |
| PrimaryForeground     | 11        | Primary foreground color.               |
| SecondaryForeground   | 12        | Secondary foreground color.             |
| TertiaryForeground    | 13        | Tertiary foreground color.              |
| PrimaryBorder         | 14        | Primary border color.                   |
| SecondaryBorder       | 15        | Secondary border color.                 |
| TertiaryBorder        | 16        | Tertiary border color.                  |

### BitSize

| **Name** | **Value** | **Description**           |
|----------|-----------|---------------------------|
| Small    | 0         | Small sized ButtonGroup.  |
| Medium   | 1         | Medium sized ButtonGroup. |
| Large    | 2         | Large sized ButtonGroup.  |

### BitButtonType

Although ButtonGroup itself does not directly set a button type, individual items in the group (if rendered as buttons) may use:

| **Name** | **Value** | **Description**                                |
|----------|-----------|------------------------------------------------|
| Button   | 0         | Standard clickable button.                     |
| Submit   | 1         | Button that submits form data.                 |
| Reset    | 2         | Button that resets form inputs.                |

### BitDir

Controls the text direction for the component.

| **Name** | **Value** | **Description**                                                                  |
|----------|-----------|----------------------------------------------------------------------------------|
| Ltr      | 0         | Left-to-right text direction.                                                    |
| Rtl      | 1         | Right-to-left text direction.                                                    |
| Auto     | 2         | Automatically determine the text direction based on content.                     |

### BitVisibility

Controls the rendering of the component.

| **Name**  | **Value** | **Description**                                        |
|-----------|-----------|--------------------------------------------------------|
| Visible   | 0         | Component is visible.                                  |
| Hidden    | 1         | Component is hidden (using `visibility: hidden`).      |
| Collapsed | 2         | Component is not rendered (`display: none`).          |

---