# BitSnackBar Component

**Purpose:** This document provides a structured reference for the `BitSnackBar` Blazor component (also known as Toast). Use this information to understand its functionality (displaying brief notifications), how to trigger snackbars programmatically, configure appearance (position, color, dismissal), customize content with templates, apply styling, and implement it effectively in CSHTML (`.razor`) files.

**How to Use:**
1.  **Understand the Goal:** Read the "Overview" to grasp the component's purpose – showing temporary, non-intrusive messages.
2.  **Key Concept:** The `<BitSnackBar>` tag itself is a *container* and *manager* for snackbar items. You don't put content directly inside it. Instead, you get a reference (`@ref`) to it and call methods like `.Show()`, `.Info()`, `.Success()`, etc., from your C# code to display individual snackbars.
3.  **See Examples:** Refer to the "Usage Examples" section for practical code snippets demonstrating various features (basic usage, customization options, templates, styling). Copy and adapt these examples.
4.  **Check Properties:** Consult the "API" section for a detailed list of available parameters (`@attributes`) for the `<BitSnackBar>` container (like `Position`, `AutoDismissTime`) and the parameters for the `.Show()` method (for individual item styling).
5.  **Public Methods:** Pay close attention to the "Public Members" table in the API section, which lists the methods (`.Show()`, `.Info()`, etc.) used to trigger snackbars.
6.  **Styling:** Look at the "Style & Class" example and the `BitSnackBarClassStyles` in the API section to understand how to apply custom CSS to the container and individual items.
7.  **Enums:** Check the "Enums" subsection in the API for valid values for parameters like `Position`, `Color`, and `Dir`.

---

## Overview

The `BitSnackBar` component provides brief notifications, often called "toasts". It's used to display short messages to the user that typically appear temporarily and then disappear automatically or can be dismissed manually. They are suitable for feedback like "Item saved successfully" or "Connection lost".

*(Related terms: Toast)*

---

## Usage Examples

This section demonstrates common ways to use the `BitSnackBar` component. Remember to add `@inject BitSnackBarService BitSnackBarService` to your `_Imports.razor` or page/component if you intend to use the service-based approach (not shown in these examples which use `@ref`).

### 1. Basic Usage

Shows how to declare the `BitSnackBar` container and trigger a simple informational snackbar using `@ref`.

```cshtml
<BitSnackBar @ref="basicRef" />
<BitButton OnClick="OpenBasicSnackBar">Open SnackBar</BitButton>
```

```csharp
@code {
    private BitSnackBar basicRef = default!; // Reference to the component instance

    private async Task OpenBasicSnackBar()
    {
        // Call a method on the referenced component to show a snackbar
        await basicRef.Info("This is title", "This is body");
    }
}
```

### 2. Customization (Position, Dismissal, Color, etc.)

Demonstrates configuring the `BitSnackBar` container's behavior (position, auto-dismiss) and dynamically setting the type (color) and content of the shown snackbar.

*Description:* Set container properties like `Position`, `AutoDismiss`, `AutoDismissTime`, and `Dir` on the `<BitSnackBar>` tag. Control the appearance and content of *individual* snackbars by passing parameters to the trigger method (e.g., `basicSnackBarRef.Show(title, body, color)`).

```cshtml
<BitSnackBar @ref="basicSnackBarRef"
             Dir="direction"
             Position="@basicSnackBarPosition"
             AutoDismiss="@basicSnackBarAutoDismiss"
             AutoDismissTime="TimeSpan.FromSeconds(basicSnackBarDismissSeconds)"
             Multiline="basicSnackBarMultiline" />

<BitButton OnClick="OpenBasicSnackBar">Show</BitButton>

@* Controls to configure the next snackbar to be shown *@
<BitChoiceGroup @bind-Value="basicSnackBarColor" Label="Type" TItem="BitChoiceGroupOption<BitColor>" TValue="BitColor">
    <BitChoiceGroupOption Text="Primary" Value="BitColor.Primary" />
    <BitChoiceGroupOption Text="Secondary" Value="BitColor.Secondary" />
    <BitChoiceGroupOption Text="Tertiary" Value="BitColor.Tertiary" />
    <BitChoiceGroupOption Text="Info" Value="BitColor.Info" />
    <BitChoiceGroupOption Text="Success" Value="BitColor.Success" />
    <BitChoiceGroupOption Text="Warning" Value="BitColor.Warning" />
    <BitChoiceGroupOption Text="SevereWarning" Value="BitColor.SevereWarning" />
    <BitChoiceGroupOption Text="Error" Value="BitColor.Error" />
    @* Other BitColor values omitted for brevity *@
</BitChoiceGroup>

<BitChoiceGroup @bind-Value="basicSnackBarPosition" Label="Position" TItem="BitChoiceGroupOption<BitSnackBarPosition>" TValue="BitSnackBarPosition">
    <BitChoiceGroupOption Text="TopStart" Value="BitSnackBarPosition.TopStart" />
    <BitChoiceGroupOption Text="TopCenter" Value="BitSnackBarPosition.TopCenter" />
    <BitChoiceGroupOption Text="TopEnd" Value="BitSnackBarPosition.TopEnd" />
    <BitChoiceGroupOption Text="BottomStart" Value="BitSnackBarPosition.BottomStart" />
    <BitChoiceGroupOption Text="BottomCenter" Value="BitSnackBarPosition.BottomCenter" />
    <BitChoiceGroupOption Text="BottomEnd" Value="BitSnackBarPosition.BottomEnd" />
</BitChoiceGroup>

<BitChoiceGroup @bind-Value="direction" Label="Direction" TItem="BitChoiceGroupOption<BitDir>" TValue="BitDir">
    <BitChoiceGroupOption Text="LTR" Value="BitDir.Ltr" />
    <BitChoiceGroupOption Text="RTL" Value="BitDir.Rtl" />
    <BitChoiceGroupOption Text="Auto" Value="BitDir.Auto" />
</BitChoiceGroup>

<BitToggle @bind-Value="basicSnackBarAutoDismiss" Label="Auto Dismiss" />
<BitNumberField @bind-Value="basicSnackBarDismissSeconds" Step="1" Min="1" Label="Dismiss Time (seconds)" />

<BitToggle @bind-Value="basicSnackBarMultiline" Label="Multiline" Inline />

<BitTextField @bind-Value="basicSnackBarTitle" Label="Title" DefaultValue="Title" />
<BitTextField @bind-Value="basicSnackBarBody" Label="Body" Multiline Rows="6" DefaultValue="This is a body!" />
```

```csharp
@code {
    private BitDir direction = BitDir.Ltr;
    private bool basicSnackBarMultiline;
    private bool basicSnackBarAutoDismiss;
    private int basicSnackBarDismissSeconds = 3;
    private BitSnackBar basicSnackBarRef = default!;
    private string basicSnackBarBody = "This is body";
    private string basicSnackBarTitle = "This is title";
    private BitColor basicSnackBarColor = BitColor.Info;
    private BitSnackBarPosition basicSnackBarPosition = BitSnackBarPosition.BottomEnd;

    private async Task OpenBasicSnackBar()
    {
        // Pass configured values to the Show method
        await basicSnackBarRef.Show(basicSnackBarTitle, basicSnackBarBody, basicSnackBarColor);
    }
}
```

### 3. Templates

Customize parts of the snackbar using RenderFragments.

*Description:* Use `DismissIconName` to change the close icon. Use `<TitleTemplate>` and `<BodyTemplate>` to provide custom rendering logic, accessing the original title/body via the `Context` attribute.

```cshtml
@* Custom Dismiss Icon *@
<BitSnackBar @ref="dismissIconNameRef" DismissIconName="@BitIconName.Go" />
<BitButton OnClick="OpenDismissIconName">Dismiss Icon Name</BitButton>

@* Custom Title Template *@
<BitSnackBar @ref="titleTemplateRef" AutoDismiss="false">
    <TitleTemplate Context="title">
        <div style="display: flex; flex-direction: row; gap: 10px;">
            <span>@title</span>
            <BitProgress Thickness="20" Style="width: 40px;" Indeterminate />
        </div>
    </TitleTemplate>
</BitSnackBar>
<BitButton OnClick="OpenTitleTemplate">Title Template</BitButton>

@* Custom Body Template with Actions *@
<BitSnackBar @ref="bodyTemplateRef" AutoDismiss="false">
    <BodyTemplate Context="body">
        <div style="display: flex; flex-flow: column nowrap; gap: 5px;">
            <span style="font-size: 12px; margin-bottom: 5px;">@body</span>
            <div style="display: flex; gap: 10px;">
                <BitButton OnClick="@(() => bodyTemplateAnswer = "Yes")">Yes</BitButton>
                <BitButton OnClick="@(() => bodyTemplateAnswer = "No")">No</BitButton>
            </div>
            <span>Answer: @bodyTemplateAnswer</span>
        </div>
    </BodyTemplate>
</BitSnackBar>
<BitButton OnClick="OpenBodyTemplate">Body Template</BitButton>
```

```csharp
@code {
    private string? bodyTemplateAnswer;
    private BitSnackBar bodyTemplateRef = default!;
    private BitSnackBar titleTemplateRef = default!;
    private BitSnackBar dismissIconNameRef = default!;

    private async Task OpenDismissIconName() {
        await dismissIconNameRef.Success("This is title", "This is body");
    }

    private async Task OpenTitleTemplate() {
        await titleTemplateRef.Warning("This is title", "This is body");
    }

    private async Task OpenBodyTemplate() {
        await bodyTemplateRef.Error("This is title", "This is body");
    }
}
```

### 4. Style & Class Customization

Apply custom CSS styles and classes to the SnackBar container and individual snackbar items.

*Description:*

* To style an *individual* snackbar item when shown, pass `cssClass` or `cssStyle` arguments to the `.Show()` method (or its variants like `.Info()`).
* To apply styles/classes to the *internal elements* of *all* snackbars managed by a container, use the `Styles` and `Classes` parameters on the `<BitSnackBar>` tag itself (accepts `BitSnackBarClassStyles`).

```html
<style>
    .custom-class { /* Applied to individual item via Show(cssClass: ...) */
        background-color: tomato;
        box-shadow: gold 0 0 1rem;
    }

    /* Applied via Classes parameter on BitSnackBar */
    .custom-container {
        border: 1px solid gold;
    }
    .custom-progress {
        background-color: red; /* Styles the progress bar */
    }
</style>
```

```cshtml
@* Style/Class per item via Show() method *@
<BitSnackBar @ref="snackBarStyleRef" />
<BitButton OnClick="OpenSnackBarStyle">Custom style item</BitButton>

<BitSnackBar @ref="snackBarClassRef" />
<BitButton OnClick="OpenSnackBarClass">Custom class item</BitButton>

@* Styles/Classes for internal elements via BitSnackBar parameters *@
<BitSnackBar @ref="snackBarStylesRef"
             Styles="@(new() { Container = "width: 16rem; background-color: purple;",
                               Header = "background-color: rebeccapurple; padding: 0.2rem;" })" />
<BitButton OnClick="OpenSnackBarStyles">Custom styles (internal)</BitButton>

<BitSnackBar @ref="snackBarClassesRef" AutoDismiss
             Classes="@(new() { Container = "custom-container",
                                ProgressBar = "custom-progress" })" />
<BitButton OnClick="OpenSnackBarClasses">Custom classes (internal)</BitButton>
```

```csharp
@code {
    private BitSnackBar snackBarStyleRef = default!;
    private BitSnackBar snackBarClassRef = default!;
    private BitSnackBar snackBarStylesRef = default!;
    private BitSnackBar snackBarClassesRef = default!;

    private async Task OpenSnackBarStyle() {
        // Apply style directly to this specific snackbar item
        await snackBarClassRef.Show("This is title", "This is body", cssStyle: "background-color: dodgerblue; border-radius: 0.5rem;");
    }

    private async Task OpenSnackBarClass() {
        // Apply class directly to this specific snackbar item
        await snackBarStyleRef.Show("This is title", "This is body", cssClass: "custom-class");
    }

    private async Task OpenSnackBarStyles() {
        // Styles configured on BitSnackBar tag will apply
        await snackBarStylesRef.Show("This is title", "This is body");
    }

    private async Task OpenSnackBarClasses() {
        // Classes configured on BitSnackBar tag will apply
        await snackBarClassesRef.Show("This is title", "This is body");
    }
}
```

---

## API

This section details the parameters for the `<BitSnackBar>` container component and its public methods for showing items.

### Parameters (BitSnackBar Container)

These parameters configure the overall behavior and default appearance of the SnackBar container.

| Name             | Type                          | Default Value         | Description                                                                                      |
| ---------------- | ----------------------------- | --------------------- | ------------------------------------------------------------------------------------------------ |
| `AutoDismiss`      | `bool`                        | `false`               | Whether snackbars automatically dismiss by default. Can be overridden per item in `.Show()`.     |
| `AutoDismissTime`  | `TimeSpan?`                   | `null` (uses 3 sec) | Default duration before auto-dismissal. Defaults to 3 seconds if `null`. Can be overridden.      |
| `BodyTemplate`     | `RenderFragment<string>?`     | `null`                | Custom template for rendering the body content of *all* snackbars shown by this container.       |
| `Classes`          | `BitSnackBarClassStyles?`     | `null`                | Custom CSS classes for internal elements of *all* snackbars. See `BitSnackBarClassStyles` below. |
| `DismissIconName`  | `string?`                     | `null` (uses `Cancel`)| Default icon name (from `BitIconName`) for the dismiss button. Can be overridden.              |
| `Multiline`        | `bool`                        | `false`               | Default setting for enabling multiline mode for title and body. Can be overridden.             |
| `OnDismiss`        | `EventCallback`               | (none)                | Global callback invoked when *any* snackbar managed by this container is dismissed.                |
| `Position`         | `BitSnackBarPosition?`        | `null` (uses `BottomEnd`)| Position where snackbars appear on screen. See `BitSnackBarPosition` enum. Default: `BottomEnd`.|
| `Styles`           | `BitSnackBarClassStyles?`     | `null`                | Custom CSS styles for internal elements of *all* snackbars. See `BitSnackBarClassStyles` below.  |
| `TitleTemplate`    | `RenderFragment<string>?`     | `null`                | Custom template for rendering the title content of *all* snackbars shown by this container.      |

### Public Members (Methods on BitSnackBar Instance)

Call these methods on your `@ref` variable to display snackbars.

| Name            | Signature                                                                                                 | Description                                   |
| --------------- | --------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| `Show`          | `async Task Show(string title, string? body = "", BitColor color = BitColor.Info, string? cssClass = null, string? cssStyle = null)` | Shows a snackbar with specified options.        |
| `Info`          | `Task Info(string title, string? body = "")`                                                              | Shows an Info snackbar (`BitColor.Info`).     |
| `Success`       | `Task Success(string title, string? body = "")`                                                           | Shows a Success snackbar (`BitColor.Success`).  |
| `Warning`       | `Task Warning(string title, string? body = "")`                                                           | Shows a Warning snackbar (`BitColor.Warning`).  |
| `SevereWarning` | `Task SevereWarning(string title, string? body = "")`                                                     | Shows a SevereWarning snackbar (`BitColor.SevereWarning`). |
| `Error`         | `Task Error(string title, string? body = "")`                                                             | Shows an Error snackbar (`BitColor.Error`).     |

**Note:** The `Show` method likely has overloads or optional parameters to control `AutoDismiss`, `AutoDismissTime`, `Multiline`, `DismissIconName`, etc., for individual items, overriding the container's defaults. Refer to the component's source or specific documentation for the exact signature if needed. The examples primarily show color control via the helper methods (`.Info`, `.Success`, etc.) or the `color` parameter in the base `.Show` method.

### Parameters (Inherited from BitComponentBase)

These apply to the `<BitSnackBar>` container element itself.

| Name             | Type                            | Default Value                      | Description                                                                                     |
| ---------------- | ------------------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                             | The aria-label of the control for screen readers.                                               |
| `Class`          | `string?`                       | `null`                             | Custom CSS class for the root element (`<div class="bit-snb">`) of the container.                 |
| `Dir`            | `BitDir?`                       | `null`                             | Sets the direction (LTR/RTL) for the container and its managed snackbars.                       |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()` | Capture and render additional HTML attributes on the root element.                              |
| `Id`             | `string?`                       | `null`                             | Custom id attribute for the root element. If null, a unique ID (`UniqueId`) will be used.       |
| `IsEnabled`      | `bool`                          | `true`                             | Whether the component is enabled (mostly relevant if interaction is added).                   |
| `Style`          | `string?`                       | `null`                             | Custom CSS style for the root element (`<div class="bit-snb">`) of the container.                 |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`            | Whether the container element is `Visible`, `Hidden` (takes space), or `Collapsed` (no space). |

### Public Members (Inherited from BitComponentBase)

| Name          | Type               | Default Value    | Description                                                                                           |
| ------------- | ------------------ | ---------------- | ----------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()` | Readonly unique ID of the root element, generated at component instantiation.                         |
| `RootElement` | `ElementReference` |                  | Reference to the root DOM element (`<div class="bit-snb">`) of the container.                           |

### Class Styles (BitSnackBarClassStyles)

Used with the `Classes` and `Styles` parameters on `<BitSnackBar>` to target internal elements of the *shown snackbar items*.

| Name            | Type      | Description                                                              |
| --------------- | --------- | ------------------------------------------------------------------------ |
| `Root`          | `string?` | *Likely unused directly, use `.Show(cssClass: ...)` for item root.*        |
| `Container`     | `string?` | Custom CSS classes/styles for the main container `<div>` of a snackbar item. |
| `Header`        | `string?` | Custom CSS classes/styles for the header `<div>` (containing title & dismiss).|
| `DismissButton` | `string?` | Custom CSS classes/styles for the dismiss `<button>`.                    |
| `DismissIcon`   | `string?` | Custom CSS classes/styles for the dismiss icon `<i>`.                   |
| `Title`         | `string?` | Custom CSS classes/styles for the title `<div>`.                         |
| `Body`          | `string?` | Custom CSS classes/styles for the body `<div>`.                          |
| `ProgressBar`   | `string?` | Custom CSS classes/styles for the auto-dismiss progress bar `<div>`.       |

### Enums

#### `BitSnackBarPosition`

Defines where the snackbars appear on the screen.

| Name           | Value | Description         |
| -------------- | ----- | ------------------- |
| `TopStart`     | 0     | Top-left corner.    |
| `TopCenter`    | 1     | Top-center.         |
| `TopEnd`       | 2     | Top-right corner.   |
| `BottomStart`  | 3     | Bottom-left corner. |
| `BottomCenter` | 4     | Bottom-center.      |
| `BottomEnd`    | 5     | Bottom-right corner (Default). |

#### `BitColor`

Defines standard color options, used here for the snackbar type/color passed to `.Show()` or its variants.

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

#### `BitVisibility` (from BitComponentBase)

Controls the rendering and visibility of the *container* element.

| Name        | Value | Description                                                                                       |
| ----------- | ----- | ------------------------------------------------------------------------------------------------- |
| `Visible`   | 0     | The container is visible.                                                                         |
| `Hidden`    | 1     | The container is hidden (`visibility: hidden`), but still occupies space in the layout.           |
| `Collapsed` | 2     | The container is hidden (`display: none`) and does not occupy any space in the layout.            |

#### `BitDir` (from BitComponentBase)

Specifies the text directionality for the container and its items.

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
* **Component Source Code:** [BitSnackBar.razor](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Notifications/SnackBar/BitSnackBar.razor)

