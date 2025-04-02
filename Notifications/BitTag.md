# BitTag Component

**Purpose:** This document provides a structured reference for the `BitTag` Blazor component (also known as Chip). Use this information to understand its functionality, properties (text, icon, color, variant, size), dismissibility, templating, styling, and how to implement it effectively in CSHTML (`.razor`) files.

**How to Use:**
1.  **Understand the Goal:** Read the "Overview" to grasp the component's purpose – displaying concise information like tags, attributes, or labels, optionally with an icon and dismiss action.
2.  **See Examples:** Refer to the "Usage Examples" section for practical code snippets demonstrating various features (basic usage, variants, icons, dismissibility, colors, sizes, templates, styling). Copy and adapt these examples.
3.  **Check Properties:** Consult the "API" section for a detailed list of available parameters (`@attributes` in Blazor), their types, default values, and descriptions. This is crucial for configuration and customization.
4.  **Render Fragments/Templates:** Note the use of `<ChildContent>` for templating the tag's content (Example 7).
5.  **Styling:** Look at the "Style & Class" example and the `BitTagClassStyles` in the API section to understand how to apply custom CSS.
6.  **Enums:** Check the "Enums" subsection in the API for valid values for parameters like `Color`, `Size`, `Variant`, and `Dir`.

---

## Overview

The `BitTag` component (also referred to as `Chip`) provides a visual representation of an attribute, keyword, category, person, or asset in a compact format. It typically includes text and can optionally display an icon and a dismiss button.

*(Related terms: Chip)*

---

## Usage Examples

This section demonstrates common ways to use the `BitTag` component.

### 1. Basic Usage

Displays a simple tag with text content.

```cshtml
<BitTag Text="Basic tag" />
```

### 2. Variant

The tag offers different visual styles: `Fill` (default), `Outline`, and `Text`.

*Description:* Use the `Variant` parameter with a `BitVariant` enum value to change the appearance.

```cshtml
<BitTag Text="Fill" Variant="BitVariant.Fill" />
<BitTag Text="Outline" Variant="BitVariant.Outline" />
<BitTag Text="Text" Variant="BitVariant.Text" />
```

### 3. Icon

Include an icon within the tag, typically placed before the text.

*Description:* Use the `IconName` parameter, providing a value from the `BitIconName` enum or a custom icon name string.

```cshtml
<BitTag Text="Calendar icon" IconName="@BitIconName.Calendar" />
```

### 4. Dismiss

Add a dismiss button (usually an 'X' icon) to allow users to remove the tag.

*Description:* Provide an `EventCallback` to the `OnDismiss` parameter. This renders the dismiss button and triggers the callback when clicked.

```cshtml
@if (isDismissed is false)
{
    <BitTag IconName="@BitIconName.AlarmClock" Text="Dismiss me" OnDismiss="() => isDismissed = true" />
}

<BitButton IsEnabled="isDismissed" Variant="BitVariant.Outline" OnClick="() => isDismissed = false">
    Dismissed, click to reset
</BitButton>
```

```csharp
@code {
    private bool isDismissed;
}
```

### 5. Color

Apply different predefined colors to the tag, affecting background, border, and text based on the chosen `Variant`.

*Description:* Use the `Color` parameter with a `BitColor` enum value. Works in combination with `Variant`.

```cshtml
@* Primary Color Examples *@
<BitTag Text="Primary" IconName="@BitIconName.Calendar" Color="BitColor.Primary" Variant="BitVariant.Fill" />
<BitTag Text="Primary" IconName="@BitIconName.Calendar" Color="BitColor.Primary" Variant="BitVariant.Outline" />
<BitTag Text="Primary" IconName="@BitIconName.Calendar" Color="BitColor.Primary" Variant="BitVariant.Text" />

@* Secondary Color Example *@
<BitTag Text="Secondary" IconName="@BitIconName.Calendar" Color="BitColor.Secondary" Variant="BitVariant.Fill" />

@* Success Color Example *@
<BitTag Text="Success" IconName="@BitIconName.Calendar" Color="BitColor.Success" Variant="BitVariant.Outline" />

@* Error Color Example *@
<BitTag Text="Error" IconName="@BitIconName.Calendar" Color="BitColor.Error" Variant="BitVariant.Text" />

@* Theme-aware Color Example *@
<BitTag Text="PrimaryBackground" IconName="@BitIconName.Calendar" Color="BitColor.PrimaryBackground" Variant="BitVariant.Fill" />

@* ... other BitColor values (Tertiary, Info, Warning, SevereWarning, Backgrounds, Foregrounds, Borders) follow the same pattern ... *@
```

### 6. Size

Adjust the overall size (padding, font size) of the tag.

*Description:* Use the `Size` parameter with a `BitSize` enum value (`Small`, `Medium` (default), `Large`).

```cshtml
@* Small Size Examples *@
<BitTag Text="Small" IconName="@BitIconName.Calendar" Size="BitSize.Small" Variant="BitVariant.Fill" />
<BitTag Text="Small" IconName="@BitIconName.Calendar" Size="BitSize.Small" Variant="BitVariant.Outline" />
<BitTag Text="Small" IconName="@BitIconName.Calendar" Size="BitSize.Small" Variant="BitVariant.Text" />

@* Medium (Default) Size Example *@
<BitTag Text="Medium" IconName="@BitIconName.Calendar" Size="BitSize.Medium" Variant="BitVariant.Fill" />

@* Large Size Example *@
<BitTag Text="Large" IconName="@BitIconName.Calendar" Size="BitSize.Large" Variant="BitVariant.Outline" />
```

### 7. Template (ChildContent)

Customize the content inside the tag using the `ChildContent` render fragment. This overrides the `Text` and `IconName` parameters.

*Description:* Place custom HTML elements or other Blazor components within the `<BitTag>` tags.

```html
<style>
    /* Example styles for custom content */
    .custom-tag-stack { padding-inline: 0.5rem; }
</style>
```

```cshtml
<BitTag>
    <ChildContent>
        <BitStack Horizontal Gap="0.5rem" Class="custom-tag-stack">
            <BitLabel>Custom content</BitLabel>
            <BitRollerLoading CustomSize="32" Color="BitColor.Tertiary" />
        </BitStack>
    </ChildContent>
</BitTag>
```

### 8. Style & Class Customization

Apply custom CSS styles and classes to the tag and its internal elements.

*Description:* Use standard `Style` and `Class` attributes for the root element. Use the `Styles` and `Classes` parameters (which accept a `BitTagClassStyles` object) to target specific internal parts like the text (`Text`), icon (`Icon`), or dismiss button (`DismissButton`).

```html
<style>
    .custom-class { /* Applied via Class attribute */
        border-radius: 0.25rem;
        box-shadow: aqua 0 0 0.5rem;
    }

    /* Applied via Classes parameter */
    .custom-root {
        color: mediumpurple;
        border-radius: 0.5rem;
        border-color: mediumpurple;
        background-color: transparent;
        box-shadow: mediumpurple 0 0 0.5rem;
    }
    .custom-icon {
        font-size: 1.25rem;
        font-weight: bolder;
    }
</style>
```

```cshtml
@* Using Style attribute on root *@
<BitTag Text="Styled Tag" IconName="@BitIconName.People"
        Style="border-radius: 1rem; font-weight:bold" />

@* Using Class attribute on root *@
<BitTag Text="Classed Tag" IconName="@BitIconName.People"
        Class="custom-class" Variant="BitVariant.Outline" />

@* Using Styles parameter for internal elements *@
<BitTag Text="Styles" IconName="@BitIconName.People"
        Styles="@(new() { Root = "border-color: red; background-color: transparent;",
                          Text = "color: tomato; font-weight: bold;",
                          Icon = "color: tomato;" })" />

@* Using Classes parameter for internal elements *@
<BitTag Text="Classes" IconName="@BitIconName.People"
        Classes="@(new() { Root = "custom-root",
                           Icon = "custom-icon" })" />
```

---

## API

This section details the parameters (properties) available for the `BitTag` component.

### Parameters (BitTag)

| Name           | Type                            | Default Value | Description                                                                    |
| -------------- | ------------------------------- | ------------- | ------------------------------------------------------------------------------ |
| `ChildContent` | `RenderFragment?`               | `null`        | Custom content for the tag. Overrides `Text` and `IconName`.                 |
| `Classes`      | `BitTagClassStyles?`            | `null`        | Custom CSS classes for internal parts. See `BitTagClassStyles` below.          |
| `Color`        | `BitColor?`                     | `null`        | General color of the tag. See `BitColor` enum below.                           |
| `IconName`     | `string?`                       | `null`        | Icon name (from `BitIconName`) to display in the tag.                          |
| `OnClick`      | `EventCallback<MouseEventArgs>` | (none)        | Click event handler for the tag.                                               |
| `OnDismiss`    | `EventCallback<MouseEventArgs>` | (none)        | Click event handler for the dismiss button. If provided, the button is shown. |
| `Reversed`     | `bool`                          | `false`       | Reverses the horizontal flow direction of icon and text.                       |
| `Size`         | `BitSize?`                      | `null`        | The size of the tag. See `BitSize` enum below. Default: `Medium`.              |
| `Styles`       | `BitTagClassStyles?`            | `null`        | Custom CSS styles for internal parts. See `BitTagClassStyles` below.           |
| `Text`         | `string?`                       | `null`        | The text content of the tag. Ignored if `ChildContent` is provided.            |
| `Variant`      | `BitVariant?`                   | `null`        | Visual variant (Fill, Outline, Text). See `BitVariant` enum. Default: `Fill`. |

### Parameters (Inherited from BitComponentBase)

| Name             | Type                            | Default Value                      | Description                                                                                     |
| ---------------- | ------------------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                             | The aria-label of the control for screen readers.                                               |
| `Class`          | `string?`                       | `null`                             | Custom CSS class for the root element of the component.                                         |
| `Dir`            | `BitDir?`                       | `null`                             | Determines the component direction (Ltr, Rtl, Auto).                                            |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()` | Capture and render additional HTML attributes on the root element.                              |
| `Id`             | `string?`                       | `null`                             | Custom id attribute for the root element. If null, a unique ID (`UniqueId`) will be used.       |
| `IsEnabled`      | `bool`                          | `true`                             | Whether or not the component is enabled (affects click handlers).                             |
| `Style`          | `string?`                       | `null`                             | Custom CSS style for the root element of the component.                                         |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`            | Whether the component is `Visible`, `Hidden` (takes space), or `Collapsed` (takes no space). |

### Public Members (Inherited from BitComponentBase)

| Name          | Type               | Default Value    | Description                                                                                           |
| ------------- | ------------------ | ---------------- | ----------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()` | Readonly unique ID of the root element, generated at component instantiation.                         |
| `RootElement` | `ElementReference` |                  | Reference to the root DOM element of the component.                                                   |

### Class Styles (BitTagClassStyles)

Used with the `Classes` and `Styles` parameters on `<BitTag>` to target internal elements.

| Name            | Type      | Description                                                              |
| --------------- | --------- | ------------------------------------------------------------------------ |
| `Root`          | `string?` | Custom CSS classes/styles for the root `<div>` element.                  |
| `Text`          | `string?` | Custom CSS classes/styles for the text `<span>`.                         |
| `Icon`          | `string?` | Custom CSS classes/styles for the icon `<i>` element.                   |
| `DismissButton` | `string?` | Custom CSS classes/styles for the dismiss `<button>`.                    |
| `DismissIcon`   | `string?` | Custom CSS classes/styles for the dismiss icon `<i>`.                   |

### Enums

#### `BitColor`

Defines standard color options for the tag.

| Name                | Value | Description                  |
| ------------------- | ----- | ---------------------------- |
| `Primary`           | 0     | Primary theme color.         |
| `Secondary`         | 1     | Secondary theme color.       |
| `Tertiary`          | 2     | Tertiary theme color.        |
| `Info`              | 3     | Informational theme color.   |
| `Success`           | 4     | Success theme color.         |
| `Warning`           | 5     | Warning theme color.         |
| `SevereWarning`     | 6     | Severe Warning theme color.  |
| `Error`             | 7     | Error/Danger theme color.    |
| `PrimaryBackground` | 8     | Primary background color.    |
| `SecondaryBackground`| 9     | Secondary background color.  |
| `TertiaryBackground`| 10    | Tertiary background color.   |
| `PrimaryForeground` | 11    | Primary foreground color.    |
| `SecondaryForeground`| 12    | Secondary foreground color.  |
| `TertiaryForeground`| 13    | Tertiary foreground color.   |
| `PrimaryBorder`     | 14    | Primary border color.        |
| `SecondaryBorder`   | 15    | Secondary border color.      |
| `TertiaryBorder`    | 16    | Tertiary border color.       |

#### `BitSize`

Defines the size variants for the tag.

| Name     | Value | Description              |
| -------- | ----- | ------------------------ |
| `Small`  | 0     | The small size tag.      |
| `Medium` | 1     | The medium size tag.     |
| `Large`  | 2     | The large size tag.      |

#### `BitVariant`

Defines the visual style of the tag.

| Name      | Value | Description               |
| --------- | ----- | ------------------------- |
| `Fill`    | 0     | Fill styled variant.      |
| `Outline` | 1     | Outline styled variant.   |
| `Text`    | 2     | Text styled variant.      |

#### `BitVisibility` (from BitComponentBase)

Controls the rendering and visibility of the component.

| Name        | Value | Description                                                                                       |
| ----------- | ----- | ------------------------------------------------------------------------------------------------- |
| `Visible`   | 0     | The component is visible.                                                                         |
| `Hidden`    | 1     | The component is hidden (`visibility: hidden`), but still occupies space in the layout.           |
| `Collapsed` | 2     | The component is hidden (`display: none`) and does not occupy any space in the layout.            |

#### `BitDir` (from BitComponentBase)

Specifies the text directionality.

| Name   | Value | Description                                                                                                |
| ------ | ----- | ---------------------------------------------------------------------------------------------------------- |
| `Ltr`  | 0     | Left-to-right direction.                                                                                   |
| `Rtl`  | 1     | Right-to-left direction.                                                                                   |
| `Auto` | 2     | Lets the browser decide the direction based on the content.                                                |

---

## Feedback

* **GitHub Repo:** [bitfoundation/bitplatform](https://github.com/bitfoundation/bitplatform)
* **File an Issue:** [New Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Start a Discussion:** [New Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose)
* **Component Source Code:** [BitTag.razor](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Notifications/Tag/BitTag.razor)
