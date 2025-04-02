# BitHeader Component Reference (Blazor UI)

## Overview

The `BitHeader` component provides a standard way to display a prominent bar, typically containing a title, branding elements, navigation controls, or user actions, at the top of a site or application page. It acts as a container for other components and automatically uses the application's current primary background color theme variable for its background, ensuring visual consistency.

**Use Cases:**

*   Displaying the application title or logo.
*   Providing primary navigation controls (e.g., a hamburger menu button).
*   Showing user authentication status and actions (e.g., Sign In/Sign Out button, user profile menu).
*   Housing global action buttons or search bars.
*   Creating a consistent top bar across different pages of an application.

## Key Concepts

*   **Container:** `BitHeader` serves as a container (`<header>` element) for its `ChildContent`. It typically uses an internal layout mechanism (like CSS Flexbox, implied by the use of `BitSpacer` and `gap` styling in examples) to arrange the items placed within it.
*   **Styling:** By default, it adopts the primary background color from the theme. You can customize its appearance further using the standard `Class` and `Style` parameters. Specific dimensions like `Height` can also be set.
*   **Fixed Positioning:** The `Fixed="true"` parameter allows the header to remain fixed at the top of the viewport, staying visible even when the user scrolls the page content. Be mindful of potential layout overlap with page content below when using `Fixed`.
*   **Content Projection:** Define the header's content by placing text, HTML elements, or other Blazor components (like `BitButton`, `BitText`, `BitSpacer`, `BitMenuButton`) directly between the `<BitHeader>` tags.

## Usage

### Basic Usage

The simplest way to use `BitHeader` is to place text content directly inside its tags.

**CSHTML:**

```csharp
<BitHeader>
    My Application Title
</BitHeader>
```

**Explanation:**

* The text "My Application Title" will appear inside the rendered header bar.
* The header will span the width of its container and use the default primary background color and text color defined by the theme.

### Complex Header with Controls

`BitHeader` is often used to contain multiple interactive elements, like buttons and menus, along with branding or titles. The `BitSpacer` component is useful for pushing elements to opposite ends of the header.

**CSHTML:**

```csharp
<BitHeader Style="gap: 1rem; align-items: center;">  @* Add gap and vertical alignment *@
    @* Left Side - Navigation Toggle *@
    <BitButton Variant="BitVariant.Text" IconName="@BitIconName.GlobalNavButton" Title="Open Navigation" AriaLabel="Toggle Navigation Menu" />

    @* Center/Left - Application Title *@
    <BitText Typography="BitTypography.H6">My Awesome App</BitText> @* Use Typography for semantic title *@

    @* Spacer - Pushes subsequent items to the right *@
    <BitSpacer />

    @* Right Side - User Actions *@
    <BitButton Variant="BitVariant.Text" IconName="@BitIconName.Contact" Title="Sign in" AriaLabel="Sign in" />
    <BitMenuButton TItem="BitMenuButtonOption"
                   IconName="@BitIconName.MoreVertical" @* Changed icon for clarity *@
                   Variant="BitVariant.Text"
                   Tooltip="More options" @* Use Tooltip instead of title for MenuButton *@
                   AriaLabel="More application options"
                   Styles="@(new() { OperatorButton = "padding: 0.5rem;" })">
        <BitMenuButtonOption Text="Settings" IconName="@BitIconName.Settings" />
        <BitMenuButtonOption Text="About" IconName="@BitIconName.Info" />
        <BitMenuButtonOption Text="Feedback" IconName="@BitIconName.Feedback" />
    </BitMenuButton>
</BitHeader>
```

**Explanation:**

1. **`BitHeader Style="gap: 1rem; align-items: center;"`**:
    * `gap: 1rem;`: Adds space between the direct child elements within the header (the buttons, text, spacer, etc.).
    * `align-items: center;`: Vertically aligns the items in the center of the header bar, which is good practice for mixed content heights.
2. **`BitButton Variant="BitVariant.Text"`**: Buttons use the `Text` variant to appear as simple icons/text without a background or border, blending into the header bar. `IconName` provides the visual icon. `Title` provides a tooltip on hover, and `AriaLabel` is crucial for accessibility, especially for icon-only buttons.
3. **`BitText Typography="BitTypography.H6"`**: Displays the application title. Using `BitTypography` can help maintain consistent text styling based on the theme. Changed from `Caption1` in the original example to `H6` for a more typical header title size.
4. **`BitSpacer />`**: This is a key component for layout. It expands to take up available space, effectively pushing the elements before it (`BitButton`, `BitText`) to the left and the elements after it (`BitButton`, `BitMenuButton`) to the right.
5. **`BitMenuButton`**: Provides a dropdown menu for less frequent actions.
    * `IconName="@BitIconName.MoreVertical"`: Uses a common "more options" icon.
    * `Variant="BitVariant.Text"`: Matches the style of other buttons.
    * `Tooltip` and `AriaLabel` provide hover text and accessibility information.
    * `Styles`: Customizes the padding of the menu button itself.
    * `BitMenuButtonOption`: Defines the items within the dropdown menu.

## API Reference

### `BitHeader` Parameters

| Parameter      | Type              | Default Value | Description                                                                      |
| -------------- | ----------------- | ------------- | -------------------------------------------------------------------------------- |
| `ChildContent` | `RenderFragment?` | `null`        | The content (text, HTML, other components) to be rendered inside the `BitHeader`. |
| `Height`       | `int?`            | `null`        | Sets a specific height for the `BitHeader` in pixels. If `null`, height is auto.   |
| `Fixed`        | `bool`            | `false`       | If `true`, the header uses `position: fixed` to stay anchored at the top of the viewport during scrolling. |
| *(Inherited)*  |                   |               | Inherits parameters from `BitComponentBase` (see below).                           |

### Inherited Parameters (from `BitComponentBase`)

These parameters are available on `BitHeader` as it inherits from `BitComponentBase`.

| Parameter        | Type                           | Default Value                       | Description                                                                                 |
| ---------------- | ------------------------------ | ----------------------------------- | ------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                      | `null`                              | The `aria-label` attribute for the root `<header>` element, improving accessibility.          |
| `Class`          | `string?`                      | `null`                              | Custom CSS class(es) to apply to the root `<header>` element.                               |
| `Dir`            | `BitDir?`                      | `null`                              | Specifies the text direction (`Ltr`, `Rtl`, `Auto`) for the header content.               |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<string, object>()`  | Allows capturing and rendering additional HTML attributes on the root `<header>` element.      |
| `Id`             | `string?`                      | `null`                              | Sets a custom `id` attribute for the root element.                                          |
| `IsEnabled`      | `bool`                         | `true`                              | Whether the component (and potentially its contents) appears enabled or disabled visually.    |
| `Style`          | `string?`                      | `null`                              | Custom inline CSS styles to apply to the root `<header>` element.                           |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`             | Controls the visibility of the component (`Visible`, `Hidden`, `Collapsed`).                |

### Public Members (from `BitComponentBase`)

These are public members available on the component instance.

| Member        | Type               | Default Value      | Description                                                                                                |
| ------------- | ------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()`   | A read-only unique identifier (`Guid`) generated for each component instance. Useful for internal referencing. |
| `RootElement` | `ElementReference` | *(N/A)*            | An `ElementReference` pointing to the root DOM element (`<header>`) of the component. Useful for JS interop. |

## Related Enums

### `BitVisibility` Enum

Defines how the component is displayed.

| Name        | Value | Description                                                                                    | CSS Equivalent         |
| ----------- | ----- | ---------------------------------------------------------------------------------------------- | ---------------------- |
| `Visible`   | `0`   | The component is rendered and visible.                                                         | `visibility: visible;` |
| `Hidden`    | `1`   | The component is hidden, but it still occupies space in the layout.                            | `visibility: hidden;`  |
| `Collapsed` | `2`   | The component is hidden and does not occupy any space in the layout (removed from flow).       | `display: none;`       |

### `BitDir` Enum

Defines the text directionality.

| Name   | Value | Description                                                                                                                                                   | HTML `dir` Attribute |
| ------ | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| `Ltr`  | `0`   | Left-to-right text direction (e.g., English).                                                                                                                 | `ltr`                |
| `Rtl`  | `1`   | Right-to-left text direction (e.g., Arabic, Hebrew).                                                                                                          | `rtl`                |
| `Auto` | `2`   | The browser determines the direction based on the content. Useful for user-generated content where the language is unknown.                                     | `auto`               |

## Feedback

* Provide feedback via [GitHub Issues](https://github.com/bitfoundation/bitplatform/issues/new/choose).
* Start a discussion on [GitHub Discussions](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
* Review/Edit the [Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Layouts/Header/BitHeaderDemo.razor).
* Review/Edit the [Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Layouts/Header/BitHeader.razor).
