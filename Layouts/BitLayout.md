# BitLayout Component Reference (Blazor UI)

## Overview

The `BitLayout` component serves as a foundational building block for structuring the main user interface of a Blazor application. It provides predefined slots for common layout sections like Header, Footer, Main content, and an optional Navigation Panel (NavPanel), simplifying the creation of consistent and responsive application shells.

**Use Cases:**

*   Defining the primary structure of an application (e.g., Admin dashboards, public-facing websites).
*   Implementing standard layouts with headers, footers, and side navigation.
*   Providing a consistent container for page content across different routes.
*   Managing the visibility and positioning (e.g., sticky, reversed) of core layout elements.

## Key Concepts

*   **Section Slots:** `BitLayout` uses named `RenderFragment` parameters (`Header`, `Main`, `Footer`, `NavPanel`) to define distinct areas within the layout. You place your content for each section within these corresponding tags inside `<BitLayout>`.
*   **NavPanel:** An optional side panel, typically used for navigation menus. Its visibility can be controlled (`HideNavPanel`), its width set (`NavPanelWidth`), and its position relative to the main content reversed (`ReverseNavPanel`).
*   **Sticky Positioning:** The `Header` and `Footer` can be made "sticky" (`StickyHeader`, `StickyFooter`), meaning they remain fixed at the top or bottom of the viewport, respectively, even when the main content scrolls.
*   **Targeted Styling:** The `Classes` and `Styles` parameters allow applying custom CSS classes or inline styles to specific internal elements of the `BitLayout` (like the header container, main content area, etc.) using the `BitLayoutClassStyles` object. This provides fine-grained control over the appearance of each section.

## Usage

### Basic Layout (Header, Main, Footer)

Define the fundamental structure with a header, main content area, and footer.

**CSHTML:**

```csharp
<style>
    /* Basic styling for visual distinction */
    .basic-layout-header {
        padding: 1rem;
        border: 1px dashed blue;
        background-color: #e0e8ff;
        text-align: center;
    }

    .basic-layout-main {
        padding: 1rem;
        border: 1px dashed green;
        background-color: #e0ffe8;
        min-height: 150px; /* Ensure some height for visibility */
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .basic-layout-footer {
        padding: 1rem;
        border: 1px dashed red;
        background-color: #ffe0e8;
        text-align: center;
    }
</style>

<BitLayout>
    <Header>
        <div class="basic-layout-header">Application Header</div>
    </Header>
    <Main>
        <div class="basic-layout-main">Main Page Content Goes Here</div>
    </Main>
    <Footer>
        <div class="basic-layout-footer">Application Footer</div>
    </Footer>
</BitLayout>
```

**Explanation:**

* The `BitLayout` component acts as the main container.
* Content placed within `<Header>`, `<Main>`, and `<Footer>` tags is rendered into the corresponding layout sections.
* Simple CSS classes are used here for visual demonstration of the sections.

### Layout with NavPanel (and Conditional Hiding)

Include a navigation panel alongside the main content and demonstrate how to toggle its visibility.

**CSHTML:**

```csharp
<style>
    .nav-layout-header { padding: 0.75rem; border: 1px solid #ccc; background-color: #f0f0f0; }
    .nav-layout-main { padding: 1rem; border: 1px solid #ccc; background-color: #ffffff; height: 200px; display: flex; align-items: center; justify-content: center; }
    .nav-layout-navpanel { padding: 1rem; border: 1px solid #ccc; background-color: #e8e8e8; height: 100%; display: flex; align-items: center; justify-content: center; }
    .nav-layout-footer { padding: 0.75rem; border: 1px solid #ccc; background-color: #f0f0f0; }
</style>

<BitToggle Label="Hide Navigation Panel" @bind-Value="isNavHidden" />
<br />

<BitLayout HideNavPanel="isNavHidden">
    <Header>
        <div class="nav-layout-header">Header</div>
    </Header>
    <NavPanel>
        <div class="nav-layout-navpanel">Nav Menu</div>
    </NavPanel>
    <Main>
        <div class="nav-layout-main">Main Content</div>
    </Main>
    <Footer>
        <div class="nav-layout-footer">Footer</div>
    </Footer>
</BitLayout>

@code {
    private bool isNavHidden;
}
```

**Explanation:**

* The `<NavPanel>` section is added to contain the navigation content.
* A `BitToggle` controls the `isNavHidden` boolean variable.
* The `HideNavPanel` parameter of `BitLayout` is bound to `isNavHidden`. Toggling the switch will show or hide the `NavPanel` section and adjust the main content area accordingly.

### Applying Custom Styles and Classes

Use the `Styles` and `Classes` parameters with a `BitLayoutClassStyles` object to apply specific styling to internal layout elements.

**CSHTML:**

```csharp
<style>
    /* Style definitions for custom classes */
    .custom-header-class {
        background-color: lightcoral;
        color: white;
        padding: 15px;
        text-align: center;
        font-weight: bold;
        border-bottom: 2px solid darkred;
    }

    .custom-main-container-class { /* Styles the main area containing nav and content */
        border: 3px dotted purple;
    }
    
    .custom-nav-class {
        background-color: lightskyblue;
        border-right: 2px solid darkblue;
        padding: 10px;
        width: 150px; /* Example fixed width */
        box-sizing: border-box;
         display: flex; align-items: center; justify-content: center;
    }

    .custom-main-content-class { /* Styles the specific content area */
        background-color: lightyellow;
        padding: 20px;
         display: flex; align-items: center; justify-content: center;
    }

    .custom-footer-class {
        background-color: lightgreen;
        color: darkgreen;
        padding: 10px;
        text-align: center;
        border-top: 2px solid darkgreen;
    }
</style>

<BitLayout Styles="@(LayoutStyles)" Classes="@(LayoutClasses)">
    <Header>Header Content</Header>
    <NavPanel>Nav Content</NavPanel>
    <Main>Main Content Area</Main>
    <Footer>Footer Content</Footer>
</BitLayout>

@code {
    // Object providing inline styles for specific layout parts
    private BitLayoutClassStyles LayoutStyles = new()
    {
        Main = "min-height: 250px; border-top: 1px solid #aaa; border-bottom: 1px solid #aaa;", // Style for the <main> container
        NavPanel = "/* Inline styles for NavPanel element if needed */",
        MainContent = "font-style: italic;" // Style for the inner main content container
    };

    // Object providing CSS class names for specific layout parts
    private BitLayoutClassStyles LayoutClasses = new()
    {
        Root = "overall-layout-wrapper", // Class for the root div
        Header = "custom-header-class",
        Main = "custom-main-container-class",
        NavPanel = "custom-nav-class",
        MainContent = "custom-main-content-class",
        Footer = "custom-footer-class"
    };
}
```

**Explanation:**

* The `Styles` parameter takes a `BitLayoutClassStyles` object where each property (`Header`, `Main`, `NavPanel`, etc.) contains a string of *inline CSS styles*.
* The `Classes` parameter also takes a `BitLayoutClassStyles` object, but here each property contains a string of *CSS class names* to be applied.
* This allows precise styling hooks into the different generated HTML elements within the `BitLayout` structure without needing complex CSS selectors.

## API Reference

### `BitLayout` Parameters

| Parameter         | Type                       | Default Value | Description                                                                                                     |
| ----------------- | -------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------- |
| `Classes`         | `BitLayoutClassStyles?`    | `null`        | Provides an object to specify custom CSS **classes** for different internal parts of the `BitLayout` (see below). |
| `Footer`          | `RenderFragment?`          | `null`        | The content (`RenderFragment`) to be placed in the footer section. Define using `<Footer>...</Footer>`.           |
| `Header`          | `RenderFragment?`          | `null`        | The content (`RenderFragment`) to be placed in the header section. Define using `<Header>...</Header>`.         |
| `HideNavPanel`    | `bool`                     | `false`       | If `true`, the NavPanel section is hidden, and the main content area expands to fill its space.                 |
| `Main`            | `RenderFragment?`          | `null`        | The content (`RenderFragment`) to be placed in the main section. Define using `<Main>...</Main>`.             |
| `NavPanel`        | `RenderFragment?`          | `null`        | The content (`RenderFragment`) to be placed in the nav panel section. Define using `<NavPanel>...</NavPanel>`.   |
| `NavPanelWidth`   | `int`                      | `0`           | Specifies the width of the `NavPanel` section in pixels. A value of `0` might imply default/auto width.         |
| `ReverseNavPanel` | `bool`                     | `false`       | If `true`, the `NavPanel` is rendered on the right side of the `Main` content instead of the default left side. |
| `Styles`          | `BitLayoutClassStyles?`    | `null`        | Provides an object to specify custom inline CSS **styles** for different internal parts of the `BitLayout`.     |
| `StickyFooter`    | `bool`                     | `false`       | If `true`, the footer section uses sticky positioning to remain visible at the bottom of the viewport.         |
| `StickyHeader`    | `bool`                     | `false`       | If `true`, the header section uses sticky positioning to remain visible at the top of the viewport.          |
| *(Inherited)*     |                            |               | Inherits parameters from `BitComponentBase` (see below).                                                        |

### `BitLayoutClassStyles` Properties

This class is used by the `Classes` and `Styles` parameters of `BitLayout` to target specific internal elements. Each property accepts a `string?`.

| Property      | Target Element Description                                                                | Usage with `Classes` Param  | Usage with `Styles` Param     |
| ------------- | ----------------------------------------------------------------------------------------- | --------------------------- | ----------------------------- |
| `Root`        | The main root `div` element of the entire `BitLayout` component.                          | Apply CSS class(es)       | Apply inline CSS style(s)   |
| `Header`      | The `<header>` element containing the `Header` `RenderFragment`.                          | Apply CSS class(es)       | Apply inline CSS style(s)   |
| `Main`        | The `<main>` element that wraps both the `NavPanel` (if present) and the `MainContent`.   | Apply CSS class(es)       | Apply inline CSS style(s)   |
| `NavPanel`    | The `div` element containing the `NavPanel` `RenderFragment`.                             | Apply CSS class(es)       | Apply inline CSS style(s)   |
| `MainContent` | The `div` element specifically wrapping the `Main` `RenderFragment` content.              | Apply CSS class(es)       | Apply inline CSS style(s)   |
| `Footer`      | The `<footer>` element containing the `Footer` `RenderFragment`.                          | Apply CSS class(es)       | Apply inline CSS style(s)   |

### Inherited Parameters (from `BitComponentBase`)

| Parameter        | Type                           | Default Value                       | Description                                                                                 |
| ---------------- | ------------------------------ | ----------------------------------- | ------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                      | `null`                              | The `aria-label` attribute for the root element, improving accessibility.                   |
| `Class`          | `string?`                      | `null`                              | Custom CSS class(es) to apply to the **root** element (`div`) of the `BitLayout`. Use `Classes.Root` for more specificity. |
| `Dir`            | `BitDir?`                      | `null`                              | Specifies the text direction (`Ltr`, `Rtl`, `Auto`) for the layout content.               |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<string, object>()`  | Allows capturing and rendering additional HTML attributes on the root element (`div`).      |
| `Id`             | `string?`                      | `null`                              | Sets a custom `id` attribute for the root element.                                          |
| `IsEnabled`      | `bool`                         | `true`                              | Whether the component appears enabled visually.                                               |
| `Style`          | `string?`                      | `null`                              | Custom inline CSS styles for the **root** element (`div`). Use `Styles.Root` for more specificity. |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`             | Controls the visibility of the entire `BitLayout` component (`Visible`, `Hidden`, `Collapsed`). |

### Public Members (from `BitComponentBase`)

| Member        | Type               | Default Value      | Description                                                                                                |
| ------------- | ------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()`   | A read-only unique identifier (`Guid`) generated for each component instance.                              |
| `RootElement` | `ElementReference` | *(N/A)*            | An `ElementReference` pointing to the root DOM element (`div`) of the component. Useful for JS interop. |

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
| `Auto` | `2`   | The browser determines the direction based on the content.                                                                                                    | `auto`               |

## Feedback

* Provide feedback via [GitHub Issues](https://github.com/bitfoundation/bitplatform/issues/new/choose).
* Start a discussion on [GitHub Discussions](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
* Review/Edit the [Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Layouts/Layout/BitLayoutDemo.razor).
* Review/Edit the [Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Layouts/Layout/BitLayout.razor).
