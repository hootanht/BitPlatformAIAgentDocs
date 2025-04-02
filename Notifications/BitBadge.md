# BitBadge Component

**Purpose:** This document provides a structured reference for the `BitBadge` Blazor component. Use this information to understand its functionality, properties, styling options, and how to implement it effectively in CSHTML (`.razor`) files.

**How to Use:**
1.  **Understand the Goal:** Read the "Overview" to grasp the component's purpose.
2.  **See Examples:** Refer to the "Usage Examples" section for practical code snippets demonstrating various features. Copy and adapt these examples.
3.  **Check Properties:** Consult the "API" section for a detailed list of available parameters (`@attributes` in Blazor), their types, default values, and descriptions. This is crucial for customization.
4.  **Styling:** Look at the "Style & Class" example and the `BitBadgeClassStyles` in the API section to understand how to apply custom CSS.
5.  **Enums:** Check the "Enums" subsection in the API for valid values for parameters like `Color`, `Size`, `Position`, and `Variant`.

---

## Overview

The `BitBadge` component is a small visual element used to highlight or indicate specific information within a user interface, often appearing near another element (like an icon or button) to provide context like counts, status, or notifications.

---

## Usage Examples

This section demonstrates common ways to use the `BitBadge` component.

### 1. Basic Usage

Displays a simple badge with content attached to a child element (e.g., an icon).

```cshtml
<BitBadge Content="63">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

### 2. Variant

The badge offers three visual styles: `Fill` (default), `Outline`, and `Text`. It also supports an `IsEnabled` state.

*Description:* Use the `Variant` parameter to change the appearance.

```cshtml
@* Fill (Default) *@
<BitBadge Content="84" Variant="BitVariant.Fill">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Outline *@
<BitBadge Content="84" Variant="BitVariant.Outline">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Text *@
<BitBadge Content="84" Variant="BitVariant.Text">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>


@* Disabled Fill *@
<BitBadge Content="84" Variant="BitVariant.Fill" IsEnabled="false">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Disabled Outline *@
<BitBadge Content="84" Variant="BitVariant.Outline" IsEnabled="false">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Disabled Text *@
<BitBadge Content="84" Variant="BitVariant.Text" IsEnabled="false">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

### 3. Overlap

Controls whether the badge overlaps its child content.

*Description:* Use the `Overlap` boolean parameter to make the badge slightly overlap the element it's attached to.

```cshtml
<BitBadge Content="63" Overlap>
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

### 4. Dot

Displays the badge as a small dot, hiding any content. Useful for simple notification indicators.

*Description:* Use the `Dot` boolean parameter to show a small indicator dot instead of content.

```cshtml
<BitBadge Dot>
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

### 5. Max

Limits the numerical value displayed in the badge.

*Description:* When `Content` is an integer, use the `Max` parameter to cap the displayed number. Values exceeding `Max` will show as `Max+`.

```cshtml
<BitBadge Max="63" Content="100">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

*(Displays "63+")*

### 6. Customization (Content Types)

Badges can display strings or icons as content.

*Description:* Use the `Content` parameter for text/numbers or the `IconName` parameter for icons within the badge itself.

```cshtml
@* String Content *@
<BitBadge Content="@("Text")">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Icon Content *@
<BitBadge IconName="@BitIconName.Ringer">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

### 7. Hidden

Conditionally hide the badge.

*Description:* Use the `Hidden` boolean parameter to control the badge's visibility dynamically.

```cshtml
<BitToggle @bind-Value="hidden" Label="Hide the badge" />

<BitBadge Hidden="hidden" Content="63">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

```csharp
@code {
    private bool hidden;
}
```

### 8. Position

Control the placement of the badge relative to its child content.

*Description:* Use the `Position` parameter with a `BitPosition` enum value (e.g., `TopRight`, `BottomLeft`) to set the badge's location. Default is `TopRight`.

```cshtml
<BitBadge Content="63" Position="badgePosition">
    <BitButton Variant="BitVariant.Outline">Position</BitButton>
</BitBadge>

<BitDropdown Items="badgePositionList" @bind-Value="badgePosition" Style="width: 8rem;" />
```

```csharp
@code {
    private BitPosition badgePosition = BitPosition.TopRight; // Default shown for clarity

    private List<BitDropdownItem<BitPosition>> badgePositionList = Enum.GetValues(typeof(BitPosition))
        .Cast<BitPosition>()
        .Select(enumValue => new BitDropdownItem<BitPosition>
        {
            Value = enumValue,
            Text = enumValue.ToString()
        })
        .ToList();
}
```

### 9. Color

Apply different predefined colors to the badge.

*Description:* Use the `Color` parameter with a `BitColor` enum value (e.g., `Primary`, `Success`, `Error`) to change the badge's color scheme. Works with different `Variant`s.

```cshtml
@* Primary Color Examples *@
<BitBadge Content="84" Color="BitColor.Primary">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
<BitBadge Content="84" Color="BitColor.Primary" Variant="BitVariant.Outline">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
<BitBadge Content="84" Color="BitColor.Primary" Variant="BitVariant.Text">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Success Color Example *@
<BitBadge Content="84" Color="BitColor.Success">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Error Color Example *@
<BitBadge Content="84" Color="BitColor.Error">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* ... other BitColor values (Secondary, Tertiary, Info, Warning, SevereWarning) follow the same pattern ... *@
```

### 10. Size

Adjust the size of the badge.

*Description:* Use the `Size` parameter with a `BitSize` enum value (`Small`, `Medium` (default), `Large`) to change the badge's dimensions.

```cshtml
@* Small Size Examples *@
<BitBadge Content="84" Size="BitSize.Small" Variant="BitVariant.Fill">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
<BitBadge Content="84" Size="BitSize.Small" Variant="BitVariant.Outline">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
<BitBadge Content="84" Size="BitSize.Small" Variant="BitVariant.Text">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Medium (Default) Size Example *@
<BitBadge Content="84" Size="BitSize.Medium" Variant="BitVariant.Fill">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Large Size Example *@
<BitBadge Content="84" Size="BitSize.Large" Variant="BitVariant.Fill">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* ... other variants (Outline, Text) combined with sizes follow the same pattern ... *@
```

### 11. Style & Class Customization

Apply custom CSS styles and classes to the badge and its internal elements.

*Description:* Use standard `Style` and `Class` attributes for the root element. Use the `Styles` and `Classes` parameters (which accept a `BitBadgeClassStyles` object) to target specific internal parts like the badge itself (`Badge`), its wrapper (`BadgeWrapper`), or the icon (`Icon`).

```html
<style>
    .custom-class { /* Applied via Class attribute */
        border-radius: 1rem;
        box-shadow: aqua 0 0 0.5rem;
    }
    .custom-class div { /* Affects child content */
        padding: 0.5rem;
        color: blueviolet;
    }

    /* Applied via Classes parameter */
    .custom-root {
        margin-left: 2rem;
        text-shadow: aqua 0 0 0.5rem;
    }
    .custom-wrapper {
        padding: 1rem;
    }
    .custom-badge {
        border-end-end-radius: 0.5rem;
        border-start-end-radius: unset;
        border-end-start-radius: unset;
        border-start-start-radius: 0.5rem;
    }
    .custom-icon {
        color: dodgerblue;
    }
</style>
```

```cshtml
@* Using Style and Class attributes *@
<BitBadge Content="84" Style="color: dodgerblue;"> @* Affects root/text indirectly *@
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
<BitBadge Content="84" Class="custom-class" Variant="BitVariant.Outline">
    <div>Anchor</div> @* Child content styled by .custom-class div *@
</BitBadge>


@* Using Styles parameter *@
<BitBadge Content="84" IconName="@BitIconName.Info"
           Styles="@(new() { Root = "color: tomato;",
                             Badge = "border-radius: unset;",
                             Icon = "color: tomato;" })">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>

@* Using Classes parameter *@
<BitBadge Content="84" IconName="@BitIconName.Info"
          Variant="BitVariant.Outline"
          Classes="@(new() { Root = "custom-root",
                             BadgeWrapper = "custom-wrapper",
                             Badge = "custom-badge",
                             Icon = "custom-icon" })">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

### 12. Events

Handle click events on the badge itself.

*Description:* Use the `OnClick` parameter to trigger an action when the badge area (not the child content) is clicked.

```cshtml
<BitBadge Content="counter" OnClick="() => counter++">
    <BitIcon IconName="@BitIconName.Mail" Color="BitColor.Tertiary" />
</BitBadge>
```

```csharp
@code {
    private int counter;
}
```

---

## API

This section details the parameters (properties) available for the `BitBadge` component.

### Parameters (BitBadge)

| Name           | Type                          | Default Value | Description                                                                 |
| -------------- | ----------------------------- | ------------- | --------------------------------------------------------------------------- |
| `ChildContent` | `RenderFragment?`             | `null`        | Child content of component, the content that the badge will apply to.       |
| `Classes`      | `BitBadgeClassStyles?`        | `null`        | Custom CSS classes for different parts of the BitBadge.                     |
| `Color`        | `BitColor?`                   | `null`        | The general color of the badge. See `BitColor` enum below.                  |
| `Content`      | `object?`                     | `null`        | Content you want inside the badge. Supported types are string and integer.  |
| `Dot`          | `bool`                        | `false`       | Reduces the size of the badge and hide any of its content.                  |
| `Hidden`       | `bool`                        | `false`       | The visibility of the badge.                                                |
| `IconName`     | `string?`                     | `null`        | Sets the Icon to use in the badge (alternative to `Content`).               |
| `Max`          | `int?`                        | `null`        | Max value to display when content is integer type. Shows `Max+` if exceeded.|
| `OnClick`      | `EventCallback<MouseEventArgs>` | (none)        | Button click event if set. Triggered when the badge itself is clicked.      |
| `Overlap`      | `bool`                        | `false`       | Overlaps the badge on top of the child content.                             |
| `Position`     | `BitPosition?`                | `null`        | The position of the badge. See `BitPosition` enum below. Default: TopRight. |
| `Size`         | `BitSize?`                    | `null`        | The size of badge. See `BitSize` enum below. Default: Medium.             |
| `Styles`       | `BitBadgeClassStyles?`        | `null`        | Custom CSS styles for different parts of the BitBadge.                      |
| `Variant`      | `BitVariant?`                 | `null`        | The visual variant of the badge. See `BitVariant` enum below. Default: Fill.|

### Parameters (Inherited from BitComponentBase)

| Name             | Type                            | Default Value                      | Description                                                                                     |
| ---------------- | ------------------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                             | The aria-label of the control for screen readers.                                               |
| `Class`          | `string?`                       | `null`                             | Custom CSS class for the root element of the component.                                         |
| `Dir`            | `BitDir?`                       | `null`                             | Determines the component direction (Ltr, Rtl, Auto).                                            |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()` | Capture and render additional HTML attributes on the root element.                              |
| `Id`             | `string?`                       | `null`                             | Custom id attribute for the root element. If null, a unique ID (`UniqueId`) will be used.       |
| `IsEnabled`      | `bool`                          | `true`                             | Whether or not the component is enabled.                                                        |
| `Style`          | `string?`                       | `null`                             | Custom CSS style for the root element of the component.                                         |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`            | Whether the component is `Visible`, `Hidden` (takes space), or `Collapsed` (takes no space). |

### Class Styles (BitBadgeClassStyles)

Used with the `Classes` and `Styles` parameters to target specific elements within the component.

| Name           | Type      | Default Value | Description                                                              |
| -------------- | --------- | ------------- | ------------------------------------------------------------------------ |
| `Root`         | `string?` | `null`        | Custom CSS classes/styles for the root element (`<span>`) of the BitBadge. |
| `BadgeWrapper` | `string?` | `null`        | Custom CSS classes/styles for the wrapper `<span>` containing the badge.  |
| `Badge`        | `string?` | `null`        | Custom CSS classes/styles for the badge content `<span>` itself.          |
| `Icon`         | `string?` | `null`        | Custom CSS classes/styles for the icon `<i>` when `IconName` is used.    |

### Enums

#### `BitColor`

Defines the color themes for the badge.

| Name            | Value | Description                  |
| --------------- | ----- | ---------------------------- |
| `Primary`       | 0     | Primary theme color.         |
| `Secondary`     | 1     | Secondary theme color.       |
| `Tertiary`      | 2     | Tertiary theme color.        |
| `Info`          | 3     | Informational theme color.   |
| `Success`       | 4     | Success theme color.         |
| `Warning`       | 5     | Warning theme color.         |
| `SevereWarning` | 6     | Severe Warning theme color.  |
| `Error`         | 7     | Error/Danger theme color.    |

#### `BitSize`

Defines the size variants for the badge.

| Name     | Value | Description              |
| -------- | ----- | ------------------------ |
| `Small`  | 0     | The small size badge.    |
| `Medium` | 1     | The medium size badge.   |
| `Large`  | 2     | The large size badge.    |

#### `BitPosition`

Defines the placement of the badge relative to its child content.

| Name           | Value | Description          |
| -------------- | ----- | -------------------- |
| `TopLeft`      | 0     | Position at Top-Left     |
| `TopCenter`    | 1     | Position at Top-Center   |
| `TopRight`     | 2     | Position at Top-Right (Default) |
| `CenterLeft`   | 3     | Position at Center-Left  |
| `Center`       | 4     | Position at Center       |
| `CenterRight`  | 5     | Position at Center-Right |
| `BottomLeft`   | 6     | Position at Bottom-Left  |
| `BottomCenter` | 7     | Position at Bottom-Center|
| `BottomRight`  | 8     | Position at Bottom-Right |

#### `BitVariant`

Defines the visual style of the badge.

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
* **Component Source Code:** [BitBadge.razor](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Notifications/Badge/BitBadge.razor)

**Explanation of the Markdown File for the AI:**

1.  **Structure:** The file uses standard Markdown syntax. Headings (`#`, `##`, `###`, `####`) organize information hierarchically. Code blocks (```) contain C# (`.razor`/CSHTML) and C# code snippets. Tables (`| Name | ... |`) provide structured API details.
2.  **Overview:** A high-level summary of what the component does.
3.  **Usage Examples:** Each `###` subheading under "Usage Examples" shows a specific feature or configuration. The text description explains the goal, and the code block provides a ready-to-use example. These are your primary source for generating basic component usage code.
4.  **API Section:** This is critical for understanding customization options.
    *   **Parameters Tables:** List all `@attributes` you can set on the `<BitBadge>` tag. Pay attention to the `Type` (e.g., `string`, `bool`, `int?`, `BitColor?`) and `Default Value`. Use the `Description` to understand what each parameter does. Inherited parameters come from a base class and are common to many components.
    *   **Class Styles Table:** Explains the `BitBadgeClassStyles` object used with the `Styles` and `Classes` parameters for fine-grained CSS control. The `Name` column indicates the part of the component being targeted (e.g., `Root`, `Badge`).
    *   **Enums Tables:** List the valid options for parameters that take specific enumerated types (like `Color`, `Size`, `Position`, `Variant`). When a user asks for a specific color, size, etc., refer to these tables for the correct `BitColor.Value`, `BitSize.Value`, etc.
5.  **Feedback:** Contains links relevant to the source project, less critical for code generation but useful for context.

By following this structure, the AI agent can effectively understand the `BitBadge` component and assist users in implementing it correctly.
