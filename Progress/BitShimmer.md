# Bit Blazor UI Shimmer Component (`BitShimmer`)

**Version:** (Based on the provided HTML snapshot)
**Purpose:** This document provides a reference guide for using the `BitShimmer` component (also known as a Skeleton loader) in the Bit Blazor UI library. It covers its role as a placeholder, customization options (shape, size, animation, color), handling loaded content, advanced templating, and provides a detailed API reference.

---

## Overview

`BitShimmer` (or Skeleton) acts as a temporary animated placeholder. It's used to improve the user experience when parts of the UI are waiting for data (e.g., from a service call) to load. Instead of showing a blank space or a disruptive loading spinner, the shimmer mimics the shape of the content that will eventually appear, indicating that content is forthcoming without blocking the rendering of the surrounding UI.

---

## Usage Examples

Below are examples demonstrating how to use and customize the `BitShimmer` component.

### 1. Basic Usage

The simplest way to use the shimmer is with its default rectangular shape and wave animation.

```cshtml
<BitShimmer />
```

*(Note: Renders a basic rectangular shimmer placeholder with a subtle wave animation.)*

### 2. Setting Size (`Width`, `Height`)

You can control the dimensions of the shimmer placeholder using standard CSS units in the `Width` and `Height` parameters.

```cshtml
@* Shimmer with a specific height *@
<BitShimmer Height="5rem" />

@* Shimmer with a specific width *@
<BitShimmer Width="10rem" />
```

*(Note: Renders rectangular shimmers, one taller and one wider than the default.)*

### 3. Circular Shape (`Circle`)

Set the `Circle` parameter to `true` to render a circular shimmer, often used as a placeholder for avatars or icons. `Width` or `Height` can be used to control its size (it will maintain a 1:1 aspect ratio based on the *smaller* of the two if both are set, or use the single dimension provided).

```cshtml
@* Circular shimmer sized by Height *@
<BitShimmer Circle Height="3rem" />

@* Circular shimmer sized by Width *@
<BitShimmer Circle Width="4rem" />
```

*(Note: Renders circular shimmer placeholders of different sizes.)*

### 4. Customizing Animation (`Pulse`, `Duration`, `Delay`)

* `Pulse`: Set to `true` to change the animation from the default `Wave` to a `Pulse` effect.
* `Duration`: Control the speed of one animation cycle (in milliseconds).
* `Delay`: Set a delay before the animation starts (in milliseconds).

```cshtml
@* Default Wave animation with custom timing *@
<BitShimmer Height="4rem" Duration="5000" Delay="1000" />

@* Pulse animation with custom timing *@
<BitStack Horizontal>
    <BitShimmer Pulse Circle Height="4rem" Duration="3000" Delay="1000" />
    <BitShimmer Pulse Height="4rem" Width="100%" Duration="3000" Delay="1000" />
</BitStack>
```

*(Note: Renders shimmers with modified animation speeds and delays. The second example shows the 'Pulse' animation on both circular and rectangular shimmers.)*

### 5. Handling Loaded Content (`Loaded`, `ChildContent`/`Content`)

The primary use case involves replacing the shimmer with actual content once data is available.

* Set the `Loaded` parameter to a boolean value (e.g., `@isDataLoaded`).
* When `Loaded` is `false`, the shimmer is shown (either the default or the custom `Template`).
* When `Loaded` becomes `true`, the content provided within the `BitShimmer` tags (its `ChildContent`, aliased as `Content`) is rendered instead, often with a smooth transition.

```csharp
@page "/shimmer-loaded"
@using Microsoft.AspNetCore.Components.Web

<BitShimmer Loaded="@isDataLoaded" AriaLabel="Loading content" Height="1.5rem">
    Content loaded successfully.
</BitShimmer>
<br />
<BitToggleButton @bind-IsChecked="@isDataLoaded" Text="Toggle shimmer" />

@code {
    private bool isDataLoaded;
}
```

*(Note: Shows a shimmer initially. Clicking the toggle button sets `isDataLoaded` to true, replacing the shimmer with the text "Content loaded successfully.".)*

### 6. Advanced Usage with Custom Template (`Template`)

For complex placeholder layouts that mimic the structure of the final content, use the `<Template>` render fragment inside `BitShimmer`. This allows nesting other `BitShimmer` components to create sophisticated skeleton screens. The `<Content>` (or `ChildContent`) fragment still defines what appears when `Loaded` is true.

```csharp
@page "/shimmer-advanced"
@using Microsoft.AspNetCore.Components.Web
@using Bit.BlazorUI

<BitShimmer Loaded="@isContentLoaded" AriaLabel="Loading content" Width="15rem" Height="unset">
    <Content>
        @* This is the actual content shown when isContentLoaded is true *@
        <BitImage Height="8rem" Alt="bit logo" Src="/images/bit-logo-blue.png" />
        <br />
        <BitPersona PrimaryText="Annie Lindqvist"
                    SecondaryText="Software Engineer"
                    Size="@BitPersonaSize.Size56"
                    Presence="@BitPersonaPresence.Online"
                    ImageUrl="https://static2.sharepointonline.com/files/fabric/office-ui-fabric-react-assets/persona-female.png" />
    </Content>
    <Template>
        @* This is the placeholder structure shown when isContentLoaded is false *@
        <BitShimmer Height="8rem" /> @* Placeholder for Image *@
        <br />
        <BitStack Horizontal AlignItems="BitStackAlignment.Center">
            <BitShimmer Circle Height="3.5rem" /> @* Placeholder for Persona image *@
            <BitStack VerticalAlign="BitStackAlignment.SpaceBetween">
                <BitShimmer Height="1.25rem" Width="8.5rem" /> @* Placeholder for PrimaryText *@
                <BitShimmer Height="0.75rem" Width="7rem" /> @* Placeholder for SecondaryText *@
            </BitStack>
        </BitStack>
    </Template>
</BitShimmer>
<br />
<BitToggleButton @bind-IsChecked="@isContentLoaded" Text="Toggle shimmer" />

@code {
    private bool isContentLoaded;
}
```

*(Note: Initially shows a placeholder layout consisting of a large rectangle (for the image) and a circle next to two smaller rectangles (for the persona). When toggled, this is replaced by the actual `BitImage` and `BitPersona` components.)*

### 7. Shimmer Animation Color (`Color`)

Use the `Color` parameter with the `BitColor` enum to change the color of the *animated highlight* (the wave or pulse) within the shimmer.

```cshtml
<BitShimmer Height="1rem" Color="BitColor.Primary" />
<BitShimmer Height="1rem" Color="BitColor.Secondary" />
<BitShimmer Height="1rem" Color="BitColor.Tertiary" />
<BitShimmer Height="1rem" Color="BitColor.Info" />
<BitShimmer Height="1rem" Color="BitColor.Success" />
<BitShimmer Height="1rem" Color="BitColor.Warning" />
<BitShimmer Height="1rem" Color="BitColor.SevereWarning" />
<BitShimmer Height="1rem" Color="BitColor.Error" />
@* Foreground colors often provide good contrast for the animation *
<BitShimmer Height="1rem" Color="BitColor.PrimaryForeground" />
<BitShimmer Height="1rem" Color="BitColor.SecondaryForeground" />
<BitShimmer Height="1rem" Color="BitColor.TertiaryForeground" />
@* Background/Border colors might be less visible depending on the Background color *
<BitShimmer Height="1rem" Color="BitColor.PrimaryBackground" />
<BitShimmer Height="1rem" Color="BitColor.SecondaryBackground" />
<BitShimmer Height="1rem" Color="BitColor.TertiaryBackground" />
<BitShimmer Height="1rem" Color="BitColor.PrimaryBorder" />
<BitShimmer Height="1rem" Color="BitColor.SecondaryBorder" />
<BitShimmer Height="1rem" Color="BitColor.TertiaryBorder" />
```

*(Note: Renders multiple shimmers where the moving highlight part uses different theme colors specified by `BitColor`.)*

### 8. Shimmer Background Color (`Background`)

Use the `Background` parameter with the `BitColor` enum to change the color of the *static container* of the shimmer. The default is typically a subtle grey (`SecondaryBackground`).

```cshtml
<BitShimmer Height="2rem" Background="BitColor.Primary" />
<BitShimmer Height="2rem" Background="BitColor.Secondary" />
<BitShimmer Height="2rem" Background="BitColor.Tertiary" />
<BitShimmer Height="2rem" Background="BitColor.Info" />
<BitShimmer Height="2rem" Background="BitColor.Success" />
<BitShimmer Height="2rem" Background="BitColor.Warning" />
<BitShimmer Height="2rem" Background="BitColor.SevereWarning" />
<BitShimmer Height="2rem" Background="BitColor.Error" />
<BitShimmer Height="2rem" Background="BitColor.PrimaryBackground" />
<BitShimmer Height="2rem" Background="BitColor.SecondaryBackground" /> @* Default Background Color *@
<BitShimmer Height="2rem" Background="BitColor.TertiaryBackground" />
<BitShimmer Height="2rem" Background="BitColor.PrimaryForeground" />
<BitShimmer Height="2rem" Background="BitColor.SecondaryForeground" />
<BitShimmer Height="2rem" Background="BitColor.TertiaryForeground" />
<BitShimmer Height="2rem" Background="BitColor.PrimaryBorder" />
<BitShimmer Height="2rem" Background="BitColor.SecondaryBorder" />
<BitShimmer Height="2rem" Background="BitColor.TertiaryBorder" />
```

*(Note: Renders multiple shimmers where the static background area uses different theme colors specified by `BitColor`.)*

### 9. Custom Styling (`Style`, `Class`, `Styles`, `Classes`)

Apply custom styles and classes:

* `Style` / `Class`: Apply directly to the root element.
* `Styles` / `Classes`: Target specific internal elements (`Root`, `ShimmerWrapper`, `Shimmer`) using the `BitShimmerClassStyles` object.

```css
/* Example CSS */
.custom-class {
    box-shadow: aqua 0 0 1rem 0.5rem; /* Applied to root */
}

.custom-root {
    border-radius: 1rem; /* Style root */
    overflow: hidden; /* Recommended when styling root */
}

.custom-shimmer {
    /* Style the animated element */
    background: linear-gradient(90deg, transparent, darkred, transparent);
}

.custom-wrapper {
    /* Style the container holding the animation */
    border: 2px dashed tomato;
    background-color: lightgoldenrodyellow; /* Change shimmer background via wrapper */
}
```

```cshtml
@* Inline style on root *@
<BitShimmer Height="2.7rem" Style="border: 2px solid purple; border-radius: 5px;" />
<br />

@* CSS class on root *@
<BitShimmer Height="2.7rem" Class="custom-class" />
<br />

@* Targeting internal elements with Styles (inline) *@
<BitShimmer Height="2.7rem"
             Styles="@(new() { Shimmer = "background: darkblue;",
                               ShimmerWrapper = "background-color: lightblue;" })" />
<br />

@* Targeting internal elements with Classes (CSS) *@
<BitShimmer Height="2.7rem"
             Classes="@(new() { Root = "custom-root",
                                Shimmer = "custom-shimmer",
                                ShimmerWrapper = "custom-wrapper" })" />
```

*(Note: Demonstrates applying borders, shadows, custom animation gradients, and wrapper styles using the various styling parameters.)*

---

## API Reference

### `BitShimmer` Parameters

| Name           | Type                       | Default Value | Description                                                                                     |
| :------------- | :------------------------- | :------------ | :---------------------------------------------------------------------------------------------- |
| `Background`   | `BitColor?`                | `null` (defaults to `SecondaryBackground`) | The background color of the static container of the shimmer (uses `BitColor` enum). |
| `ChildContent` | `RenderFragment?`          | `null`        | The actual content to display when `Loaded` becomes true. Rendered instead of the shimmer/template. |
| `Circle`       | `bool`                     | `false`       | Renders the shimmer as a circle instead of a rectangle.                                         |
| `Classes`      | `BitShimmerClassStyles?`   | `null`        | Custom CSS classes for different internal parts of the BitShimmer (uses `BitShimmerClassStyles`).|
| `Color`        | `BitColor?`                | `null` (defaults to `TertiaryBackground`) | The color of the animated part (wave/pulse) of the shimmer (uses `BitColor` enum).       |
| `Content`      | `RenderFragment?`          | `null`        | Alias for `ChildContent`.                                                                       |
| `Delay`        | `int?`                     | `null`        | Animation delay in milliseconds.                                                                |
| `Duration`     | `int?`                     | `null`        | Animation duration for one cycle in milliseconds.                                               |
| `Height`       | `string?`                  | `null`        | CSS height value for the shimmer (e.g., "1rem", "50px").                                        |
| `Loaded`       | `bool`                     | `false`       | When true, displays `ChildContent`/`Content`; when false, displays the shimmer/`Template`.     |
| `Pulse`        | `bool`                     | `false`       | Changes the animation style from the default 'wave' to 'pulse'.                                 |
| `Styles`       | `BitShimmerClassStyles?`   | `null`        | Custom inline CSS styles for different internal parts of the BitShimmer (uses `BitShimmerClassStyles`).|
| `Template`     | `RenderFragment?`          | `null`        | Custom placeholder structure (often containing nested `BitShimmer`s) shown when `Loaded` is false. |
| `Width`        | `string?`                  | `null`        | CSS width value for the shimmer (e.g., "100%", "200px").                                        |

### `BitComponentBase` Parameters (Inherited)

These parameters are common to all Bit Blazor UI components.

| Name           | Type                            | Default Value                        | Description                                                                                     |
| :------------- | :------------------------------ | :----------------------------------- | :---------------------------------------------------------------------------------------------- |
| `AriaLabel`    | `string?`                       | `null`                               | The `aria-label` attribute for accessibility, important for shimmer placeholders.               |
| `Class`        | `string?`                       | `null`                               | Custom CSS class(es) to apply to the root element.                                              |
| `Dir`          | `BitDir?`                       | `null`                               | Sets the component's text direction (LTR/RTL/Auto) using the `BitDir` enum.                   |
| `HtmlAttributes`| `Dictionary<string, object>`  | `new Dictionary<string, object>()` | Captures and renders additional HTML attributes on the root element.                              |
| `Id`           | `string?`                       | `null`                               | Custom `id` attribute for the root element. If `null`, a unique ID (`UniqueId`) is generated. |
| `IsEnabled`    | `bool`                          | `true`                               | Whether the component is visually/functionally enabled.                                         |
| `Style`        | `string?`                       | `null`                               | Custom inline CSS styles to apply to the root element.                                          |
| `Visibility`   | `BitVisibility`                 | `BitVisibility.Visible`              | Controls the component's visibility (`Visible`, `Hidden`, `Collapsed`) using the `BitVisibility` enum. |

### `BitComponentBase` Public Members (Inherited)

| Name          | Type               | Default Value      | Description                                                                               |
| :------------ | :----------------- | :----------------- | :---------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()`   | A read-only unique identifier generated for the component instance upon construction.      |
| `RootElement` | `ElementReference` | *(N/A)*            | Provides a reference to the component's root HTML element (useful for JavaScript interop). |

---

## Supporting Types

### `BitShimmerClassStyles` Class

Used by the `Styles` and `Classes` parameters to target specific elements within the `BitShimmer` component.

| Property       | Type      | Description                                                    |
| :------------- | :-------- | :------------------------------------------------------------- |
| `Root`         | `string?` | Styles/classes for the root container element.                 |
| `Content`      | `string?` | Styles/classes for the actual content wrapper (when loaded).   |
| `ShimmerWrapper`| `string?` | Styles/classes for the wrapper containing the shimmer animation. |
| `Shimmer`      | `string?` | Styles/classes for the animated shimmer element itself (wave/pulse). |

### `BitColor` Enum

Provides predefined theme color options for `Color` and `Background` parameters. (Includes Primary, Secondary, Tertiary, Info, Success, Warning, SevereWarning, Error, and various Background, Foreground, Border variations).

*(Refer to the full BitColor Enum definition in shared documentation or previous examples if needed)*

### `BitVisibility` Enum

Controls the component's rendering and visibility.

| Name      | Value | Description                                                         |
| :-------- | :---- | :------------------------------------------------------------------ |
| `Visible` | `0`   | Component is rendered and visible.                                |
| `Hidden`  | `1`   | Component is hidden (`visibility: hidden`), but preserves space. |
| `Collapsed`| `2`   | Component is not rendered (`display: none`), consumes no space.    |

### `BitDir` Enum

Controls the component's text and layout direction.

| Name | Value | Description                                                   |
| :--- | :---- | :------------------------------------------------------------ |
| `Ltr`| `0`   | Left-to-right direction (e.g., English).                    |
| `Rtl`| `1`   | Right-to-left direction (e.g., Arabic, Hebrew).             |
| `Auto`| `2`   | Browser automatically determines direction based on content. |

---

## Feedback & Source Code

* **Report Issues:** [File an Issue on GitHub](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Start Discussions:** [Start a Discussion on GitHub](https://github.com/bitfoundation/bitplatform/discussions/new/choose)
* **View/Edit Page Source:** [Shimmer Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Progress/Shimmer/BitShimmerDemo.razor)
* **View/Edit Component Source:** [BitShimmer Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Progress/Shimmer/BitShimmer.razor)