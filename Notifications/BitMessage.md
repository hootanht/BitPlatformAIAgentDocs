# BitMessage Component

**Purpose:** This document provides a structured reference for the `BitMessage` Blazor component (also known as Alert or MessageBar). Use this information to understand its functionality, properties (like color, variant, dismissibility), content templating, styling options, and how to implement it effectively in CSHTML (`.razor`) files.

**How to Use:**
1.  **Understand the Goal:** Read the "Overview" to grasp the component's purpose – displaying status messages (info, success, warning, error).
2.  **See Examples:** Refer to the "Usage Examples" section for practical code snippets demonstrating various features (basic usage, colors, variants, dismissibility, actions, styling, RTL). Copy and adapt these examples.
3.  **Check Properties:** Consult the "API" section for a detailed list of available parameters (`@attributes` in Blazor), their types, default values, and descriptions. This is crucial for configuration and customization.
4.  **Render Fragments:** Note the use of `<Content>` and `<Actions>` render fragments for placing custom content and action buttons within the message bar.
5.  **Styling:** Look at the "Style & Class" example and the `BitMessageClassStyles` in the API section to understand how to apply custom CSS.
6.  **Enums:** Check the "Enums" subsection in the API for valid values for parameters like `Color`, `Variant`, `Alignment`, `Size`, and `Dir`.

---

## Overview

The `BitMessage` component displays errors, warnings, informational messages, or success confirmations. It's typically used to provide feedback to the user about the status of an operation or important contextual information. It can include an icon, text content, action buttons, and a dismiss button.

*(Related terms: Alert, MessageBar)*

---

## Usage Examples

This section demonstrates common ways to use the `BitMessage` component.

### 1. Basic Usage

Displays a simple informational message.

```cshtml
<BitMessage>This is a Message.</BitMessage>
```

### 2. Color

Messages can adopt various predefined colors to indicate severity or type.

*Description:* Use the `Color` parameter with a `BitColor` enum value. `BitColor.Info` is the default if unspecified.

```cshtml
<BitMessage Color="BitColor.Primary">Primary.</BitMessage>
<BitMessage Color="BitColor.Secondary">Secondary.</BitMessage>
<BitMessage Color="BitColor.Tertiary">Tertiary.</BitMessage>
<BitMessage Color="BitColor.Info">Info (default).</BitMessage>
<BitMessage Color="BitColor.Success">Success.</BitMessage>
<BitMessage Color="BitColor.Warning">Warning.</BitMessage>
<BitMessage Color="BitColor.SevereWarning">SevereWarning.</BitMessage>
<BitMessage Color="BitColor.Error">Error.</BitMessage>

@* Theme-aware background/foreground/border colors (less common for direct message types) *@
<BitMessage Color="BitColor.PrimaryBackground">PrimaryBackground.</BitMessage>
<BitMessage Color="BitColor.SecondaryBackground">SecondaryBackground.</BitMessage>
<BitMessage Color="BitColor.TertiaryBackground">TertiaryBackground.</BitMessage>
<BitMessage Color="BitColor.PrimaryForeground">PrimaryForeground.</BitMessage>
<BitMessage Color="BitColor.SecondaryForeground">SecondaryForeground.</BitMessage>
<BitMessage Color="BitColor.TertiaryForeground">TertiaryForeground.</BitMessage>
<BitMessage Color="BitColor.PrimaryBorder">PrimaryBorder.</BitMessage>
<BitMessage Color="BitColor.SecondaryBorder">SecondaryBorder.</BitMessage>
<BitMessage Color="BitColor.TertiaryBorder">TertiaryBorder.</BitMessage>
```

### 3. Variant

Messages support different visual styles: `Fill` (default), `Outline`, and `Text`.

*Description:* Use the `Variant` parameter with a `BitVariant` enum value.

```cshtml
@* Fill Variant (Default) *@
<BitMessage Color="BitColor.Success" Variant="BitVariant.Fill">Success.</BitMessage>

@* Outline Variant *@
<BitMessage Color="BitColor.Warning" Variant="BitVariant.Outline">Warning.</BitMessage>

@* Text Variant *@
<BitMessage Color="BitColor.Error" Variant="BitVariant.Text">Error.</BitMessage>

@* Combine with different colors *@
<BitMessage Color="BitColor.Primary" Variant="BitVariant.Outline">Primary Outline.</BitMessage>
<BitMessage Color="BitColor.Info" Variant="BitVariant.Text">Info Text.</BitMessage>
```

### 4. Alignment

Control the horizontal alignment of the message content (icon and text).

*Description:* Use the `Alignment` parameter with a `BitAlignment` enum value (`Start`, `Center`, `End`). Default is `Start`.

```cshtml
<BitMessage Alignment="BitAlignment.Start" Color="BitColor.Primary">Start</BitMessage>
<BitMessage Alignment="BitAlignment.Center" Color="BitColor.Secondary">Center</BitMessage>
<BitMessage Alignment="BitAlignment.End" Color="BitColor.Tertiary">End</BitMessage>
```

### 5. Elevation

Apply a shadow effect to the message bar.

*Description:* Use the `Elevation` parameter with an integer value from 0 to 24 to control the shadow depth.

```cshtml
<BitMessage Elevation="(int)elevation">Elevated Message</BitMessage>

<BitSlider Label="Elevation" Min="0" Max="24" Step="1" @bind-Value="elevation" />
```

```csharp
@code {
    private double elevation = 7;
}
```

### 6. Multiline

Allow the message content to wrap onto multiple lines.

*Description:* Set the `Multiline` boolean parameter to `true`.

```cshtml
<BitMessage Multiline Color="BitColor.Success">
    <b>Multiline</b> parameter makes the content to be rendered in multiple lines.
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi luctus, purus a lobortis tristique, odio augue pharetra metus, ac placerat nunc mi nec dui. Vestibulum aliquam et nunc semper scelerisque. Curabitur vitae orci nec quam condimentum porttitor et sed lacus. Vivamus ac efficitur leo. Cras faucibus mauris libero, ac placerat erat euismod et. Donec pulvinar commodo odio sit amet faucibus. In hac habitasse platea dictumst. Duis eu ante commodo, condimentum nibh pellentesque, laoreet enim. Fusce massa lorem, ultrices eu mi a, fermentum suscipit magna. Integer porta purus pulvinar, hendrerit felis eget, condimentum mauris.
</BitMessage>
```

### 7. Truncate

Truncate overflowing text in a single-line message and provide an expand/collapse button.

*Description:* Set the `Truncate` boolean parameter to `true`. This is intended for single-line messages in limited space and is incompatible with `Multiline`.

```cshtml
<BitMessage Truncate Color="BitColor.Warning">
    <b>Truncate</b> parameter cut the overflowed content at the end of the single line Message.
    Truncation is not available if you use multiline and should be used sparingly.
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi luctus, purus a lobortis tristique, odio augue pharetra metus, ac placerat nunc mi nec dui. Vestibulum aliquam et nunc semper scelerisque. Curabitur vitae orci nec quam condimentum porttitor et sed lacus. Vivamus ac efficitur leo. Cras faucibus mauris libero, ac placerat erat euismod et. Donec pulvinar commodo odio sit amet faucibus. In hac habitasse platea dictumst. Duis eu ante commodo, condimentum nibh pellentesque, laoreet enim. Fusce massa lorem, ultrices eu mi a, fermentum suscipit magna. Integer porta purus pulvinar, hendrerit felis eget, condimentum mauris.
</BitMessage>
```

### 8. Dismiss

Allow the user to close the message.

*Description:* Provide an `EventCallback` to the `OnDismiss` parameter. This will render a dismiss button (usually an 'X' icon).

```cshtml
@if (isDismissed is false)
{
    <BitMessage OnDismiss="() => isDismissed = true" Color="BitColor.SevereWarning">
        Dismiss option enabled by adding <strong>OnDismiss</strong> parameter.
    </BitMessage>
}
else
{
    <BitButton OnClick="() => isDismissed = false">Dismissed, click to reset</BitButton>
}
```

```csharp
@code {
    private bool isDismissed;
}
```

### 9. Actions

Include custom action buttons or other content in a dedicated section of the message bar.

*Description:* Use the `<Actions>` render fragment to add elements like `BitButton`s.

```cshtml
<BitMessage>
    <Actions>
        <BitButton Variant="BitVariant.Text" Color="BitColor.Tertiary" IconName="@BitIconName.Up" />
        &nbsp;
        <BitButton Variant="BitVariant.Text" Color="BitColor.Tertiary" IconName="@BitIconName.Down" />
    </Actions>
    <Content>
        Message with single line and action buttons.
    </Content> @* You can also use ChildContent directly instead of <Content> *@
</BitMessage>
```

### 10. HideIcon

Remove the default icon associated with the message color/type.

*Description:* Set the `HideIcon` boolean parameter to `true`.

```cshtml
<BitMessage Color="BitColor.Info" HideIcon>Info (default) Message.</BitMessage>
<BitMessage Color="BitColor.Success" HideIcon>Success Message.</BitMessage>
<BitMessage Color="BitColor.Warning" HideIcon>Warning Message.</BitMessage>
<BitMessage Color="BitColor.SevereWarning" HideIcon>SevereWarning Message.</BitMessage>
<BitMessage Color="BitColor.Error" HideIcon>Error Message.</BitMessage>
```

### 11. Icons

Customize the icons used for the message type, dismiss button, or truncate expand/collapse buttons.

*Description:* Use `IconName` for the main icon, `DismissIcon` for the close button, and `ExpandIcon`/`CollapseIcon` for the truncate toggle.

```cshtml
@* Custom main icon *@
<BitMessage Color="BitColor.Success" IconName="@BitIconName.CheckMark">
    Message with a custom icon.
</BitMessage>

@* Custom dismiss icon *@
<BitMessage Color="BitColor.Warning" OnDismiss="() => {}" DismissIcon="@BitIconName.Blocked2Solid">
    Message with a custom dismiss icon.
</BitMessage>

@* Custom expand/collapse icons for truncate *@
<BitMessage Truncate Color="BitColor.Warning"
            ExpandIcon="@BitIconName.ChevronDownEnd"
            CollapseIcon="@BitIconName.ChevronUpEnd">
    Message with custom expand and collapse icon.
    (Long truncated content...)
</BitMessage>
```

### 12. Advanced Combination

Combine multiple features like `Truncate`, `OnDismiss`, and `Actions`.

```cshtml
@* Truncated, Dismissible, with Actions *@
<BitMessage Truncate OnDismiss="() => {}" Color="BitColor.Warning">
    <Content>
        <b>Truncate</b> with <b>OnDismiss</b> and <b>Actions</b>.
        (Long truncated content...)
    </Content>
    <Actions>
        <div style="display:flex;align-items:center;gap:4px">
            <button>Yes</button> @* Example using plain HTML button *@
            <button>No</button>
        </div>
    </Actions>
</BitMessage>

@* Multiline, Dismissible, with Actions *@
<BitMessage Multiline OnDismiss="() => {}" Color="BitColor.Error">
    <Content>
        <b>Multiline</b> with <b>OnDismiss</b> and <b>Actions</b>.
        (Long multiline content...)
    </Content>
    <Actions>
        <BitButton Variant="BitVariant.Outline">Yes</BitButton>
        &nbsp;
        <BitButton Variant="BitVariant.Outline">No</BitButton>
    </Actions>
</BitMessage>
```

### 13. Size

Adjust the overall size (padding, font size) of the message bar.

*Description:* Use the `Size` parameter with a `BitSize` enum value (`Small`, `Medium` (default), `Large`).

```cshtml
<BitMessage Size="BitSize.Small" Color="BitColor.Primary">Small</BitMessage>
<BitMessage Size="BitSize.Medium" Color="BitColor.Secondary">Medium</BitMessage>
<BitMessage Size="BitSize.Large" Color="BitColor.Tertiary">Large</BitMessage>
```

### 14. Style & Class Customization

Apply custom CSS styles and classes to the message bar and its internal elements.

*Description:* Use standard `Style` and `Class` attributes for the root element. Use the `Styles` and `Classes` parameters (which accept a `BitMessageClassStyles` object) to target specific internal parts like the icon (`Icon`), content area (`Content`), dismiss button (`DismissButton`), etc.

```html
<style>
    .custom-class { /* Applied via Class attribute */
        padding: 1rem;
        color: deeppink;
        font-size: 1rem;
        font-style: italic;
    }

    /* Applied via Classes parameter */
    .custom-icon {
        font-size: 2rem;
    }
    .custom-content {
        font-size: 1.5rem;
    }
    .custom-expander-icon {
        margin: 0.5rem;
        font-size: 2rem;
    }
    .custom-dismiss-icon {
        margin: 0.5rem;
        font-size: 2rem;
    }
</style>
```

```cshtml
@* Using Style attribute on root *@
<BitMessage Color="BitColor.Info" Multiline OnDismiss="() => {}"
            Style="padding:8px;color:red;">
    <b>Styled Message.</b> (Content...)
</BitMessage>

@* Using Class attribute on root *@
<BitMessage Color="BitColor.Success" Truncate Class="custom-class">
    <b>Classed Message.</b> (Content...)
</BitMessage>

@* Using Styles parameter for internal elements *@
<BitMessage Color="BitColor.Warning" OnDismiss="() => {}" Multiline
            Styles="@(new() { Root="padding:1rem",
                              IconContainer="line-height:1.25",
                              Content="color:blueviolet",
                              ContentContainer="margin:0 10px",
                              DismissIcon="font-size:1rem",
                              Actions="justify-content:center;gap:1rem" })">
    <Content><b>Styles.</b> (Content...)</Content>
    <Actions><BitButton Variant="BitVariant.Text">Ok</BitButton><BitButton Variant="BitVariant.Text">Cancel</BitButton></Actions>
</BitMessage>

@* Using Classes parameter for internal elements *@
<BitMessage Color="BitColor.SevereWarning" OnDismiss="() => {}" Truncate
            Classes="@(new() { Icon="custom-icon",
                               Content="custom-content",
                               ExpanderIcon="custom-expander-icon",
                               DismissIcon="custom-dismiss-icon" })">
    <b>Classes.</b> (Content...)
</BitMessage>
```

### 15. RTL (Right-to-Left)

Render the message bar correctly for right-to-left languages.

*Description:* Set the `Dir` parameter to `BitDir.Rtl`.

```cshtml
<BitMessage Dir="BitDir.Rtl" Color="BitColor.Info">
    پیام خبری (پیش فرض). <BitLink Href="https://bitplatform.dev">به وبسایت ما سر بزنید.</BitLink>
</BitMessage>

<BitMessage Dir="BitDir.Rtl" Color="BitColor.Success" Truncate OnDismiss="() => {}">
    پیام موفق. <BitLink Href="https://bitplatform.dev">به وبسایت ما سر بزنید.</BitLink>
    (Long truncated RTL content...)
</BitMessage>

<BitMessage Dir="BitDir.Rtl" Color="BitColor.Warning" Multiline OnDismiss="() => {}">
    پیام هشدار. <BitLink Href="https://bitplatform.dev">به وبسایت ما سر بزنید.</BitLink>
    (Long multiline RTL content...)
</BitMessage>
```

---

## API

This section details the parameters (properties) available for the `BitMessage` component.

### Parameters (BitMessage)

| Name           | Type                          | Default Value | Description                                                                                                                            |
| -------------- | ----------------------------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `Actions`      | `RenderFragment?`             | `null`        | The content of the action section to show on the message.                                                                              |
| `Alignment`    | `BitAlignment?`               | `null`        | Determines the horizontal alignment of the content section (icon + text). See `BitAlignment` enum below. Default: `Start`.               |
| `ChildContent` | `RenderFragment?`             | `null`        | The main content of the message.                                                                                                       |
| `Classes`      | `BitMessageClassStyles?`      | `null`        | Custom CSS classes for different internal parts of the BitMessage. See `BitMessageClassStyles` below.                                  |
| `CollapseIcon` | `string?`                     | `null`        | Custom icon name (from `BitIconName`) for the collapse icon in Truncate mode. Default: `DoubleChevronUp`.                              |
| `Color`        | `BitColor?`                   | `null`        | The general color/type of the message. See `BitColor` enum below. Default: `Info`.                                                     |
| `Content`      | `RenderFragment?`             | `null`        | Alias for `ChildContent`.                                                                                                              |
| `DismissIcon`  | `string?`                     | `null`        | Custom icon name (from `BitIconName`) for the dismiss button. Default: `Cancel`.                                                       |
| `Elevation`    | `int?`                        | `null`        | Determines the elevation (shadow depth) of the message, a scale from 0 to 24.                                                          |
| `ExpandIcon`   | `string?`                     | `null`        | Custom icon name (from `BitIconName`) for the expand icon in Truncate mode. Default: `DoubleChevronDown`. (Note: HTML shows UpChevron) |
| `HideIcon`     | `bool`                        | `false`       | Prevents rendering the default icon associated with the message `Color`.                                                               |
| `IconName`     | `string?`                     | `null`        | Custom icon name (from `BitIconName`) to replace the default message icon.                                                             |
| `Multiline`    | `bool`                        | `false`       | Allows the message content to wrap onto multiple lines.                                                                                |
| `OnDismiss`    | `EventCallback`               | (none)        | Callback invoked when the dismiss button is clicked. If provided, the dismiss button is shown.                                         |
| `Role`         | `string?`                     | `null`        | Custom ARIA role for the message text container. Defaults based on `Color` (`status` for Info/Success, `alert` for others).           |
| `Size`         | `BitSize?`                    | `null`        | The size of the Message. See `BitSize` enum below. Default: `Medium`.                                                                  |
| `Styles`       | `BitMessageClassStyles?`      | `null`        | Custom CSS styles for different internal parts of the BitMessage. See `BitMessageClassStyles` below.                                   |
| `Truncate`     | `bool`                        | `false`       | Truncates the message text and adds an expand/collapse button. Only for single-line messages without actions.                            |
| `Variant`      | `BitVariant?`                 | `null`        | The visual variant of the message (Fill, Outline, Text). See `BitVariant` enum below. Default: `Fill`.                                 |

### Parameters (Inherited from BitComponentBase)

| Name             | Type                            | Default Value                      | Description                                                                                     |
| ---------------- | ------------------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                             | The aria-label of the control for screen readers.                                               |
| `Class`          | `string?`                       | `null`                             | Custom CSS class for the root element of the component.                                         |
| `Dir`            | `BitDir?`                       | `null`                             | Determines the component direction (Ltr, Rtl, Auto).                                            |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()` | Capture and render additional HTML attributes on the root element.                              |
| `Id`             | `string?`                       | `null`                             | Custom id attribute for the root element. If null, a unique ID (`UniqueId`) will be used.       |
| `IsEnabled`      | `bool`                          | `true`                             | Whether or not the component is enabled. (Mostly relevant for actions/buttons inside).        |
| `Style`          | `string?`                       | `null`                             | Custom CSS style for the root element of the component.                                         |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`            | Whether the component is `Visible`, `Hidden` (takes space), or `Collapsed` (takes no space). |

### Class Styles (BitMessageClassStyles)

Used with the `Classes` and `Styles` parameters to target specific elements within the component.

| Name               | Type      | Default Value | Description                                                              |
| ------------------ | --------- | ------------- | ------------------------------------------------------------------------ |
| `Root`             | `string?` | `null`        | Custom CSS classes/styles for the root `<div>` element.                  |
| `RootContainer`    | `string?` | `null`        | Custom CSS classes/styles for the main container `<div>` inside the root.|
| `Container`        | `string?` | `null`        | Custom CSS classes/styles for the `<div>` holding icon and content.       |
| `IconContainer`    | `string?` | `null`        | Custom CSS classes/styles for the `<div>` wrapping the main icon.         |
| `Icon`             | `string?` | `null`        | Custom CSS classes/styles for the main icon `<i>` element.               |
| `ContentContainer` | `string?` | `null`        | Custom CSS classes/styles for the `<div>` holding content wrapper.       |
| `ContentWrapper`   | `string?` | `null`        | Custom CSS classes/styles for the `<div>` wrapping the content text.      |
| `Content`          | `string?` | `null`        | Custom CSS classes/styles for the content text `<div>`.                  |
| `Actions`          | `string?` | `null`        | Custom CSS classes/styles for the actions container `<div>`.             |
| `ExpanderButton`   | `string?` | `null`        | Custom CSS classes/styles for the truncate expander `<button>`.          |
| `ExpanderIcon`     | `string?` | `null`        | Custom CSS classes/styles for the truncate expander icon `<i>`.          |
| `DismissButton`    | `string?` | `null`        | Custom CSS classes/styles for the dismiss `<button>`.                    |
| `DismissIcon`      | `string?` | `null`        | Custom CSS classes/styles for the dismiss icon `<i>`.                   |

### Enums

#### `BitColor`

Defines the color themes and types for the message.

| Name                | Value | Description                  | Default Icon      | Role    |
| ------------------- | ----- | ---------------------------- | ----------------- | ------- |
| `Primary`           | 0     | Primary theme color.         | `Info`            | `alert` |
| `Secondary`         | 1     | Secondary theme color.       | `Info`            | `alert` |
| `Tertiary`          | 2     | Tertiary theme color.        | `Info`            | `alert` |
| `Info`              | 3     | **Informational theme color.** | `Info`            | `status`|
| `Success`           | 4     | **Success theme color.**       | `Completed`       | `status`|
| `Warning`           | 5     | **Warning theme color.**       | `Info`            | `alert` |
| `SevereWarning`     | 6     | **Severe Warning theme color.**| `Warning`         | `alert` |
| `Error`             | 7     | **Error theme color.**         | `ErrorBadge`      | `alert` |
| `PrimaryBackground` | 8     | Primary background color.    | `Info`            | `alert` |
| `SecondaryBackground`| 9     | Secondary background color.  | `Info`            | `alert` |
| `TertiaryBackground`| 10    | Tertiary background color.   | `Info`            | `alert` |
| `PrimaryForeground` | 11    | Primary foreground color.    | `Info`            | `alert` |
| `SecondaryForeground`| 12    | Secondary foreground color.  | `Info`            | `alert` |
| `TertiaryForeground`| 13    | Tertiary foreground color.   | `Info`            | `alert` |
| `PrimaryBorder`     | 14    | Primary border color.        | `Info`            | `alert` |
| `SecondaryBorder`   | 15    | Secondary border color.      | `Info`            | `alert` |
| `TertiaryBorder`    | 16    | Tertiary border color.       | `Info`            | `alert` |

#### `BitVariant`

Defines the visual style of the message.

| Name      | Value | Description               |
| --------- | ----- | ------------------------- |
| `Fill`    | 0     | Fill styled variant.      |
| `Outline` | 1     | Outline styled variant.   |
| `Text`    | 2     | Text styled variant.      |

#### `BitAlignment`

Defines the horizontal alignment of content within containers.

| Name           | Value | Description (CSS `justify-content`) |
| -------------- | ----- | ----------------------------------- |
| `Start`        | 0     | `flex-start`                      |
| `End`          | 1     | `flex-end`                        |
| `Center`       | 2     | `center`                          |
| `SpaceBetween` | 3     | `space-between`                   |
| `SpaceAround`  | 4     | `space-around`                    |
| `SpaceEvenly`  | 5     | `space-evenly`                    |
| `Baseline`     | 6     | `baseline`                        |
| `Stretch`      | 7     | `stretch`                         |

#### `BitSize`

Defines the size variants for the message.

| Name     | Value | Description              |
| -------- | ----- | ------------------------ |
| `Small`  | 0     | The small size message.  |
| `Medium` | 1     | The medium size message. |
| `Large`  | 2     | The large size message.  |

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
* **Component Source Code:** [BitMessage.razor](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Notifications/Message/BitMessage.razor)
