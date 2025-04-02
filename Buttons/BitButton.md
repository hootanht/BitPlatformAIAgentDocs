# BitButton Component Documentation

This document provides a comprehensive reference for the `BitButton` component used in Bit.BlazorUI. It covers usage examples, the API (including parameters and public members), available enums, styling/customization, and contribution guidelines.

---

## Table of Contents

1. [Overview](#overview)
2. [Usage Examples](#usage-examples)
3. [API Reference](#api-reference)
   - [BitButton Parameters](#bitbutton-parameters)
   - [BitComponentBase Parameters](#bitcomponentbase-parameters)
   - [Public Members](#public-members)
4. [Enums](#enums)
   - [BitVariant](#bitvariant-enum)
   - [BitColor](#bitcolor-enum)
   - [BitSize](#bitsize-enum)
   - [BitButtonType](#bitbuttontype-enum)
   - [BitLabelPosition](#bitlabelposition-enum)
   - [BitLinkRel](#bitlinkrel-enum)
   - [BitPosition](#bitposition-enum)
   - [BitVisibility](#bitvisibility-enum)
   - [BitDir](#bitdir-enum)
5. [Styling and Customization](#styling-and-customization)
6. [Feedback and Contribution](#feedback-and-contribution)
7. [Conclusion](#conclusion)

---

## Overview

The `BitButton` component is a highly customizable button element for Blazor applications. It supports various styles (Fill, Outline, Text), sizes (Small, Medium, Large), color schemes, and additional features such as:
- **Loading state:** With customizable labels and templates.
- **Icon support:** Display icons alongside (or instead of) text.
- **Floating positioning:** To position the button relative to the viewport or its container.
- **Right-to-Left (RTL) support:** For languages written right-to-left.

This documentation serves as a reference for developers integrating and customizing the BitButton in their applications.

---

## Usage Examples

Below are some common usage examples:

### Basic Button

```razor
<BitButton>Click me</BitButton>
```

### Button with an Icon

```razor
<BitButton IconName="@BitIconName.Emoji">
    Click me
</BitButton>
```

### Button with Secondary Text

```razor
<BitButton SecondaryText="this is the secondary text" IconName="@BitIconName.Emoji2">
    Click me
</BitButton>
```

### Loading Button

```razor
<BitButton IsLoading="true" LoadingLabel="Loading...">
    Submit
</BitButton>
```

### Full Width Button

```razor
<BitButton FullWidth IconName="@BitIconName.Emoji2" Variant="BitVariant.Fill">
    Full Width Button
</BitButton>
```

### RTL (Right-to-Left) Button

```razor
<BitButton Dir="BitDir.Rtl" IconName="@BitIconName.Emoji" Variant="BitVariant.Fill">
    دکمه با آیکن
</BitButton>
```

For more detailed examples, refer to the interactive demo pages available in the Bit.BlazorUI repository.

---

## API Reference

### BitButton Parameters

| Name                   | Type                      | Default Value             | Description                                                                                              |
|------------------------|---------------------------|---------------------------|----------------------------------------------------------------------------------------------------------|
| `AllowDisabledFocus`   | `bool`                    | `true`                    | Whether the button can receive focus when disabled.                                                    |
| `AriaDescription`      | `string?`                 | `null`                    | Detailed description for screen readers.                                                               |
| `AriaHidden`           | `bool`                    | `false`                   | If true, adds an `aria-hidden` attribute so that screen readers ignore the element.                      |
| `AutoLoading`          | `bool`                    | `false`                   | If true, the button automatically enters a loading state while awaiting the `OnClick` event.             |
| `ButtonType`           | `BitButtonType?`          | `null`                    | Determines the type attribute of the button (e.g., Submit, Reset, or Button).                            |
| `ChildContent`         | `RenderFragment?`         | `null`                    | The primary content of the button (alias: `PrimaryTemplate`).                                            |
| `Classes`              | `BitButtonClassStyles?`   | `null`                    | Custom CSS classes for different parts of the button.                                                  |
| `Color`                | `BitColor?`               | `null`                    | The general color of the button.                                                                         |
| `FixedColor`           | `bool`                    | `false`                   | Preserves the foreground color regardless of hover or focus states.                                      |
| `Float`                | `bool`                    | `false`                   | Enables floating behavior (button positioned relative to the viewport).                                |
| `FloatAbsolute`        | `bool`                    | `false`                   | Positions the floating button relative to its container.                                               |
| `FloatOffset`          | `string?`                 | `null`                    | Specifies the offset for the floating button.                                                          |
| `FloatPosition`        | `BitPosition?`            | `null`                    | Specifies the position of the floating button (e.g., BottomRight).                                       |
| `FullWidth`            | `bool`                    | `false`                   | Makes the button span 100% of the container's width.                                                     |
| `Href`                 | `string?`                 | `null`                    | If provided, the button renders as an anchor tag with this URL.                                          |
| `IconName`             | `string?`                 | `null`                    | The name of the icon to render within the button.                                                      |
| `IconOnly`             | `bool`                    | `false`                   | If true, only the icon is displayed without any text.                                                  |
| `IconUrl`              | `string?`                 | `null`                    | URL for a custom icon image.                                                                             |
| `IsLoading`            | `bool`                    | `false`                   | Controls whether the button is in a loading state.                                                       |
| `LoadingLabel`         | `string?`                 | `null`                    | Text displayed next to the spinner icon during loading.                                                |
| `LoadingLabelPosition` | `BitLabelPosition`        | `BitLabelPosition.End`    | Position of the loading label relative to the spinner icon.                                            |
| `LoadingTemplate`      | `RenderFragment?`         | `null`                    | Custom template to replace the default loading content.                                                |
| `OnClick`              | `EventCallback<bool>`     |                           | Callback for click events; passes the current loading state as a parameter.                              |
| `Reclickable`          | `bool`                    | `false`                   | Allows re-clicking while in a loading state when `AutoLoading` is enabled.                             |
| `ReversedIcon`         | `bool`                    | `false`                   | Reverses the position of the icon and the text.                                                         |
| `Rel`                  | `BitLinkRel?`             | `null`                    | Specifies the relationship attribute for anchor links (when `Href` is provided).                         |
| `SecondaryText`        | `string?`                 | `null`                    | Text for the secondary section of the button.                                                          |
| `SecondaryTemplate`    | `RenderFragment?`         | `null`                    | Custom template for the secondary content.                                                             |
| `Size`                 | `BitSize?`                | `null`                    | Specifies the size of the button (Small, Medium, or Large).                                              |
| `Styles`               | `BitButtonClassStyles?`   | `null`                    | Custom inline styles for different parts of the button.                                                |
| `Target`               | `string?`                 | `null`                    | Specifies the target attribute for anchor links (e.g., `_blank`).                                        |
| `Title`                | `string?`                 | `null`                    | Tooltip text for the button.                                                                             |
| `Variant`              | `BitVariant?`             | `null`                    | Determines the visual style of the button (Fill, Outline, or Text).                                      |

### BitComponentBase Parameters

| Name              | Type                         | Default Value                          | Description                                                                       |
|-------------------|------------------------------|----------------------------------------|-----------------------------------------------------------------------------------|
| `AriaLabel`       | `string?`                    | `null`                                 | Provides an accessible name for the component.                                  |
| `Class`           | `string?`                    | `null`                                 | Custom CSS class for the root element.                                           |
| `Dir`             | `BitDir?`                    | `null`                                 | Specifies the text direction (LTR, RTL, or Auto).                                |
| `HtmlAttributes`  | `Dictionary<string, object>` | `new Dictionary<string, object>()`     | Additional HTML attributes to apply to the component.                          |
| `Id`              | `string?`                    | `null`                                 | Custom id for the root element. A unique id will be generated if not provided.   |
| `IsEnabled`       | `bool`                       | `true`                                 | Determines whether the component is interactive.                               |
| `Style`           | `string?`                    | `null`                                 | Custom inline styles for the root element.                                       |
| `Visibility`      | `BitVisibility`              | `BitVisibility.Visible`                | Controls the visibility (visible, hidden, or collapsed) of the component.         |

### Public Members

| Name         | Type               | Default Value       | Description                                                     |
|--------------|--------------------|---------------------|-----------------------------------------------------------------|
| `UniqueId`   | `Guid`             | `Guid.NewGuid()`    | Read-only unique identifier for the component instance.        |
| `RootElement`| `ElementReference` | N/A                 | Reference to the root DOM element of the component.             |

---

## Enums

### BitVariant Enum

| Name      | Value | Description               |
|-----------|-------|---------------------------|
| `Fill`    | 0     | Fill styled variant.      |
| `Outline` | 1     | Outline styled variant.   |
| `Text`    | 2     | Text styled variant.      |

### BitColor Enum

| Name                 | Value | Description                         |
|----------------------|-------|-------------------------------------|
| `Primary`            | 0     | Primary general color.              |
| `Secondary`          | 1     | Secondary general color.            |
| `Tertiary`           | 2     | Tertiary general color.             |
| `Info`               | 3     | Informational color.                |
| `Success`            | 4     | Success indicator color.            |
| `Warning`            | 5     | Warning indicator color.            |
| `SevereWarning`      | 6     | Severe warning color.               |
| `Error`              | 7     | Error indicator color.              |
| `PrimaryBackground`  | 8     | Primary background color.           |
| `SecondaryBackground`| 9     | Secondary background color.         |
| `TertiaryBackground` | 10    | Tertiary background color.          |
| `PrimaryForeground`  | 11    | Primary foreground color.           |
| `SecondaryForeground`| 12    | Secondary foreground color.         |
| `TertiaryForeground` | 13    | Tertiary foreground color.          |
| `PrimaryBorder`      | 14    | Primary border color.               |
| `SecondaryBorder`    | 15    | Secondary border color.             |
| `TertiaryBorder`     | 16    | Tertiary border color.              |

### BitSize Enum

| Name    | Value | Description             |
|---------|-------|-------------------------|
| `Small` | 0     | Small size button.      |
| `Medium`| 1     | Medium size button.     |
| `Large` | 2     | Large size button.      |

### BitButtonType Enum

| Name    | Value | Description                                           |
|---------|-------|-------------------------------------------------------|
| `Button`| 0     | A standard clickable button.                          |
| `Submit`| 1     | A button that submits form data.                      |
| `Reset` | 2     | A button that resets form data to its initial values. |

### BitLabelPosition Enum

| Name     | Value | Description                                        |
|----------|-------|----------------------------------------------------|
| `Top`    | 0     | Loading label appears at the top of the button.    |
| `End`    | 1     | Loading label appears at the end of the button.    |
| `Bottom` | 2     | Loading label appears at the bottom of the button. |
| `Start`  | 3     | Loading label appears at the start of the button.  |

### BitLinkRel Enum

| Name         | Value | Description                                                                                 |
|--------------|-------|---------------------------------------------------------------------------------------------|
| `Alternate`  | 1     | Link to an alternate representation (e.g., print version).                                  |
| `Author`     | 2     | Link to the author of the document.                                                         |
| `Bookmark`   | 4     | Permanent URL for bookmarking.                                                              |
| `External`   | 8     | Indicates that the link points to an external site.                                         |
| `Help`       | 16    | Link to a help document.                                                                      |
| `License`    | 32    | Link to licensing information.                                                              |
| `Next`       | 64    | Link to the next document.                                                                    |
| `NoFollow`   | 128   | Instructs search engines not to follow the link.                                              |
| `NoOpener`   | 256   | The linked page must not have access to the originating window (for security).                |
| `NoReferrer` | 512   | The referrer information will not be sent with the request.                                   |
| `Prev`       | 1024  | Link to the previous document.                                                                |
| `Search`     | 2048  | Link to a search tool related to the document.                                                |
| `Tag`        | 4096  | Tag or keyword associated with the document.                                                |

### BitPosition Enum

| Name          | Value | Description                               |
|---------------|-------|-------------------------------------------|
| `TopLeft`     | 0     | Positioned at the top left.               |
| `TopCenter`   | 1     | Positioned at the top center.             |
| `TopRight`    | 2     | Positioned at the top right.              |
| `CenterLeft`  | 3     | Positioned at the center left.            |
| `Center`      | 4     | Positioned at the center.                 |
| `CenterRight` | 5     | Positioned at the center right.           |
| `BottomLeft`  | 6     | Positioned at the bottom left.            |
| `BottomCenter`| 7     | Positioned at the bottom center.          |
| `BottomRight` | 8     | Positioned at the bottom right.           |

### BitVisibility Enum

| Name      | Value | Description                                            |
|-----------|-------|--------------------------------------------------------|
| `Visible` | 0     | The component is visible.                              |
| `Hidden`  | 1     | The component is hidden but retains its layout space.  |
| `Collapsed`| 2    | The component is hidden and does not occupy space.     |

### BitDir Enum

| Name  | Value | Description                                                                  |
|-------|-------|------------------------------------------------------------------------------|
| `Ltr` | 0     | Left-to-right text direction (e.g., English).                                |
| `Rtl` | 1     | Right-to-left text direction (e.g., Arabic).                                 |
| `Auto`| 2     | Automatically determines direction based on the content.                   |

---

## Styling and Customization

The `BitButton` supports extensive styling via the `Style` and `Classes` parameters:

- **Inline Styles**: Directly apply custom CSS using the `Style` parameter.
  
  ```razor
  <BitButton Style="background-color: transparent; border-color: blueviolet; color: blueviolet;" Variant="BitVariant.Outline">
      Styled Button
  </BitButton>
  ```

- **Custom Classes**: Use the `Class` parameter or `Classes` property (of type `BitButtonClassStyles`) to override default styles for specific parts of the button.
  
  ```razor
  <BitButton Class="custom-class">
      Classed Button
  </BitButton>
  ```

Define your custom CSS (e.g., in your CSS file):

```css
.custom-class {
    border-radius: 1rem;
    border-color: blueviolet;
    transition: background-color 1s;
    background: linear-gradient(90deg, magenta, transparent) blue;
}
.custom-class:hover {
    border-color: magenta;
    background-color: magenta;
}
```

---

## Feedback and Contribution

Your feedback is very important! You can help improve this component by:

- Filing a new [Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) on our GitHub repository.
- Starting a new [Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
- Reviewing or editing this documentation and the component code on GitHub:
  - [Review this page](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/Button/BitButtonDemo.razor)
  - [Edit this page](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/Button/BitButtonDemo.razor)

---

## Conclusion

The `BitButton` component is designed to be flexible and powerful—supporting various visual styles, sizes, and interactive states. This reference should serve as a useful guide for integrating, customizing, and extending the BitButton in your Blazor applications.