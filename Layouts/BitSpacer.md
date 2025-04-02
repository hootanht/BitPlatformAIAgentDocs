# BitSpacer Component Reference (Blazor UI)

## Overview

The `BitSpacer` component is a simple yet powerful layout utility used primarily within flexible box (flexbox) containers (`display: flex`). Its purpose is to create space between other components. It offers two main modes of operation: creating a flexible, expanding space that pushes adjacent items apart, or creating a fixed-width space.

**Use Cases:**

*   Pushing elements to opposite ends of a container (e.g., aligning items left and right in a header or toolbar).
*   Centering an element within a flex container by placing spacers on either side.
*   Creating fixed horizontal gaps between elements in a flex row.

## Key Concepts

*   **Flexbox Context:** `BitSpacer` is most effective when used as a direct child of an element styled with `display: flex`.
*   **Flexible Space (Default):** When used without the `Width` parameter inside a flex container, `BitSpacer` renders as a `div` with the CSS style `flex-grow: 1`. This causes it to expand and take up any available space along the main axis of the flex container, pushing other items away. If multiple flexible `BitSpacer` components are used, they share the available space equally.
*   **Fixed Space (`Width` Parameter):** When the `Width` parameter is provided with a numerical value, `BitSpacer` renders a `div` that creates a fixed-size horizontal gap using `margin-inline-start` (which respects LTR/RTL directionality). The unit for the `Width` parameter is **pixels**.

## Usage

### Basic Flexible Spacer (within Flex Container)

Use `BitSpacer` without any parameters inside a `display: flex` container to push elements apart.

**CSHTML:**

```csharp
<div style="display: flex; width: 100%; align-items: center; border: 1px dashed grey; padding: 5px;">
    @* Item aligned to the start *@
    <BitButton Variant="BitVariant.Text" IconName="@BitIconName.GlobalNavButton" Title="Menu" />

    @* Spacer pushes Title and Contact button away *@
    <BitSpacer /> 

    @* Centered Title (relative to the spacers) *@
    <BitText Typography="BitTypography.H6">Application Title</BitText>

    @* Spacer pushes Contact button away from Title *@
    <BitSpacer /> 

    @* Item aligned to the end *@
    <BitButton Variant="BitVariant.Text" IconName="@BitIconName.Contact" Title="User Profile" />
</div>
```

**Explanation:**

* The parent `div` is styled with `display: flex` and `align-items: center`.
* The two `<BitSpacer />` components (without `Width`) render as elements with `flex-grow: 1`.
* They expand equally to fill the available horizontal space, pushing the "Menu" button to the left, the "User Profile" button to the right, and effectively centering the "Application Title".

### Fixed Width Spacer

Use the `Width` parameter to create a fixed horizontal gap (in pixels) between elements.

**CSHTML:**

```csharp
<div style="display: flex; width: 100%; align-items: center; border: 1px dashed grey; padding: 5px;">
    <BitProgress Circular Indeterminate aria-label="Loading indicator 1" />

    @* Creates a fixed 64px gap *@
    <BitSpacer Width="64" /> 

    <BitProgress Circular Indeterminate aria-label="Loading indicator 2" />

    @* Creates another fixed 64px gap *@
    <BitSpacer Width="64" /> 

    <BitProgress Circular Indeterminate aria-label="Loading indicator 3" />
    
    @* Flexible spacer to push everything left (optional) *@
    <BitSpacer /> 
</div>
```

**Explanation:**

* The parent `div` uses `display: flex`.
* `<BitSpacer Width="64" />` renders an element that introduces a `margin-inline-start` of 64 pixels, creating a fixed horizontal space between the `BitProgress` components.
* The final, parameterless `BitSpacer` (optional) pushes the group of progress indicators and fixed spacers to the left edge of the container.

## API Reference

### `BitSpacer` Parameters

| Parameter     | Type   | Default Value | Description                                                                                                |
| ------------- | ------ | ------------- | ---------------------------------------------------------------------------------------------------------- |
| `Width`       | `int?` | `null`        | Gets or sets the fixed width of the spacer in **pixels**. If `null`, the spacer becomes flexible (`flex-grow: 1`). |
| *(Inherited)* |        |               | Inherits parameters from `BitComponentBase` (see below).                                                   |

### Inherited Parameters (from `BitComponentBase`)

These parameters are available on `BitSpacer` as it inherits from `BitComponentBase`.

| Parameter        | Type                           | Default Value                       | Description                                                                                             |
| ---------------- | ------------------------------ | ----------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                      | `null`                              | The `aria-label` attribute. Generally not needed for a purely visual spacer unless it conveys meaning. |
| `Class`          | `string?`                      | `null`                              | Custom CSS class(es) to apply to the root `div` element.                                                |
| `Dir`            | `BitDir?`                      | `null`                              | Specifies the text direction (`Ltr`, `Rtl`, `Auto`). Usually not relevant for a spacer.                 |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<string, object>()`  | Allows capturing and rendering additional HTML attributes on the root `div` element.                      |
| `Id`             | `string?`                      | `null`                              | Sets a custom `id` attribute for the root element.                                                      |
| `IsEnabled`      | `bool`                         | `true`                              | Whether the component appears enabled visually. Usually `true` for a spacer.                              |
| `Style`          | `string?`                      | `null`                              | Custom inline CSS styles to apply to the root `div` element. (Note: `flex-grow` or `margin` are set internally based on `Width`). |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`             | Controls the visibility of the component (`Visible`, `Hidden`, `Collapsed`).                            |

### Public Members (from `BitComponentBase`)

These are public members available on the component instance.

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
* Review/Edit the [Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Layouts/Spacer/BitSpacerDemo.razor).
* Review/Edit the [Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Layouts/Spacer/BitSpacer.razor).
