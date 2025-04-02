# Bit Blazor UI Loading Components

**Version:** (Based on the provided HTML snapshot)
**Purpose:** This document provides a reference guide for using the various Loading components available in the Bit Blazor UI library. It covers different types of loaders, customization options like labels, colors, and sizes, and includes detailed API information.

---

## Overview

The Bit Blazor UI library offers a suite of native loading components featuring visually appealing animations. These components are suitable for indicating wait times or ongoing processes in your Blazor application.

---

## Available Loading Components

The following loading components are available:

*   `BitBarsLoading`
*   `BitCircleLoading`
*   `BitDotsRingLoading`
*   `BitDualRingLoading`
*   `BitEllipsisLoading`
*   `BitGridLoading`
*   `BitHeartLoading`
*   `BitHourglassLoading`
*   `BitRingLoading`
*   `BitRippleLoading`
*   `BitRollerLoading`
*   `BitSpinnerLoading`

---

## Usage Examples

Below are examples demonstrating how to use and customize the loading components.

### 1. Basic Usage

To use a loading component, simply add its tag to your Razor file. Here are examples of all available types with default settings:

```cshtml
<BitBarsLoading />

<BitCircleLoading />

<BitDotsRingLoading />

<BitDualRingLoading />

<BitEllipsisLoading />

<BitGridLoading />

<BitHeartLoading />

<BitHourglassLoading />

<BitRingLoading />

<BitRippleLoading />

<BitRollerLoading />

<BitSpinnerLoading />
```

*(Note: The visual representation shows each component type rendered.)*

### 2. Adding a Label

You can add descriptive text next to the loading indicator using the `Label` parameter.

```cshtml
<BitGridLoading Label="Loading" />
```

*(Note: The visual representation shows the `BitGridLoading` component with the text "Loading" displayed, typically above it by default.)*

### 3. Positioning the Label (`LabelPosition`)

Control where the label appears relative to the loading indicator using the `LabelPosition` parameter, which accepts values from the `BitLabelPosition` enum.

```cshtml
@* Default position is Top *@
<BitDotsRingLoading Label="Top" LabelPosition="BitLabelPosition.Top" />

<BitDotsRingLoading Label="Bottom" LabelPosition="BitLabelPosition.Bottom" />

<BitDotsRingLoading Label="Start" LabelPosition="BitLabelPosition.Start" />

<BitDotsRingLoading Label="End" LabelPosition="BitLabelPosition.End" />
```

*(Note: The visual representation shows four `BitDotsRingLoading` components, each with the label ("Top", "Bottom", "Start", "End") positioned accordingly.)*

* `BitLabelPosition.Top`: Label above the indicator.
* `BitLabelPosition.Bottom`: Label below the indicator.
* `BitLabelPosition.Start`: Label to the left of the indicator (or right in RTL).
* `BitLabelPosition.End`: Label to the right of the indicator (or left in RTL).

### 4. Custom Label Content (`LabelTemplate`)

For more complex label content (e.g., HTML formatting, icons), use the `LabelTemplate` child content instead of the `Label` parameter.

```cshtml
<BitEllipsisLoading>
    <LabelTemplate>
        <div style="color:green"><b>Loading</b></div>
    </LabelTemplate>
</BitEllipsisLoading>
```

*(Note: The visual representation shows the `BitEllipsisLoading` component with the text "Loading" displayed in bold green.)*

### 5. Setting the Color (`Color`)

Use the `Color` parameter with the `BitColor` enum to apply predefined theme colors to the loading indicator.

```cshtml
<BitBarsLoading Label="Primary" Color="BitColor.Primary" />

<BitCircleLoading Label="Secondary" Color="BitColor.Secondary" />

<BitDotsRingLoading Label="Tertiary" Color="BitColor.Tertiary" />

<BitDualRingLoading Label="Info" Color="BitColor.Info" />

<BitEllipsisLoading Label="Success" Color="BitColor.Success" />

<BitGridLoading Label="Warning" Color="BitColor.Warning" />

<BitHeartLoading Label="SevereWarning" Color="BitColor.SevereWarning" />

<BitHourglassLoading Label="Error" Color="BitColor.Error" />
```

*(Note: The visual representation shows various loading components, each displaying its corresponding label and styled with the specified `BitColor`.)*

See the `BitColor` enum definition in the API section for all available options.

### 6. Setting a Custom Color (`CustomColor`)

If the predefined `BitColor` options are insufficient, you can provide any valid CSS color string (e.g., name, hex, RGB, HSL) using the `CustomColor` parameter.

```cshtml
<BitBarsLoading Label="brown" CustomColor="brown" />

<BitCircleLoading Label="rgb(0 107 185 / 75%)" CustomColor="rgb(0 107 185 / 75%)" />

<BitDotsRingLoading Label="#426985" CustomColor="#426985" />

<BitDualRingLoading Label="hsl(106 100% 22% / 1)" CustomColor="hsl(106 100% 22% / 1)" />
```

*(Note: The visual representation shows various loading components styled with the specified custom CSS colors.)*

**Note:** If both `Color` and `CustomColor` are set, `CustomColor` takes precedence.

### 7. Adjusting the Size (`Size` and `CustomSize`)

Control the overall size of the loading indicator and its label using the `Size` parameter with the `BitSize` enum, or specify an exact pixel dimension using `CustomSize`.

```cshtml
@* Using predefined sizes *@
<BitHourglassLoading Label="Small" Size="BitSize.Small" />

<BitHourglassLoading Label="Medium" Size="BitSize.Medium" /> @* Default size *@

<BitHourglassLoading Label="Large" Size="BitSize.Large" />

@* Using a custom pixel size *@
<BitHourglassLoading Label="Custom (128)" CustomSize="128" />
```

*(Note: The visual representation shows `BitHourglassLoading` components rendered at Small, Medium, Large, and a custom 128px size.)*

* See the `BitSize` enum definition in the API section for predefined options.
* `CustomSize` expects an integer representing the size in pixels.
* **Note:** If both `Size` and `CustomSize` are set, `CustomSize` takes precedence.

---

## API Reference

This section details the parameters available for the Loading components. Most parameters are defined in the base `BitLoading` component and inherited by specific types (like `BitBarsLoading`, `BitCircleLoading`, etc.).

### `BitLoading` Parameters

These parameters are common to all loading components.

| Name          | Type                         | Default Value | Description                                                 |
| :------------ | :--------------------------- | :------------ | :---------------------------------------------------------- |
| `Color`       | `BitColor?`                  | `null`        | The general color of the loading component (uses `BitColor` enum). |
| `CustomColor` | `string?`                    | `null`        | The custom CSS color of the loading component (overrides `Color`). |
| `CustomSize`  | `int?`                       | `null`        | The custom size of the loading component in pixels (overrides `Size`). |
| `Label`       | `string?`                    | `null`        | The text content of the label for the loading component.     |
| `LabelPosition`| `BitLabelPosition?`          | `null` (defaults to `Top`) | The position of the label relative to the indicator (uses `BitLabelPosition` enum). |
| `LabelTemplate`| `RenderFragment?`          | `null`        | Custom Razor content for the label (overrides `Label`).     |
| `Size`        | `BitSize?`                   | `null` (defaults to `Medium`) | The predefined size of the loading component (uses `BitSize` enum). |

### `BitComponentBase` Parameters

These parameters are inherited from the base Blazor component class and are available on all Bit Blazor UI components, including Loaders.

| Name           | Type                            | Default Value                        | Description                                                                                     |
| :------------- | :------------------------------ | :----------------------------------- | :---------------------------------------------------------------------------------------------- |
| `AriaLabel`    | `string?`                       | `null`                               | The `aria-label` attribute for accessibility.                                                   |
| `Class`        | `string?`                       | `null`                               | Custom CSS class(es) to apply to the root element.                                              |
| `Dir`          | `BitDir?`                       | `null`                               | Sets the component's text direction (LTR/RTL/Auto) using the `BitDir` enum.                   |
| `HtmlAttributes`| `Dictionary<string, object>`  | `new Dictionary<string, object>()` | Captures and renders additional HTML attributes.                                                |
| `Id`           | `string?`                       | `null`                               | Custom `id` attribute for the root element. If `null`, a unique ID (`UniqueId`) is generated. |
| `IsEnabled`    | `bool`                          | `true`                               | Whether the component is functionally enabled. (Note: Loaders are visual; this might have limited effect). |
| `Style`        | `string?`                       | `null`                               | Custom inline CSS styles to apply to the root element.                                          |
| `Visibility`   | `BitVisibility`                 | `BitVisibility.Visible`              | Controls the component's visibility (`Visible`, `Hidden`, `Collapsed`) using the `BitVisibility` enum. |

### `BitComponentBase` Public Members

| Name          | Type               | Default Value      | Description                                                                               |
| :------------ | :----------------- | :----------------- | :---------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()`   | A read-only unique identifier generated for the component instance upon construction.      |
| `RootElement` | `ElementReference` | *(N/A)*            | Provides a reference to the component's root HTML element (useful for JavaScript interop). |

---

## Enum Definitions

### `BitColor` Enum

Used by the `Color` parameter to set predefined theme colors.

| Name          | Value | Description               |
| :------------ | :---- | :------------------------ |
| `Primary`     | `0`   | Primary theme color.    |
| `Secondary`   | `1`   | Secondary theme color.  |
| `Tertiary`    | `2`   | Tertiary theme color.   |
| `Info`        | `3`   | Informational theme color.|
| `Success`     | `4`   | Success theme color.      |
| `Warning`     | `5`   | Warning theme color.      |
| `SevereWarning`| `6`   | Severe Warning theme color.|
| `Error`       | `7`   | Error theme color.        |

### `BitLabelPosition` Enum

Used by the `LabelPosition` parameter.

| Name   | Value | Description                             |
| :----- | :---- | :-------------------------------------- |
| `Top`  | `0`   | Label above the indicator.            |
| `End`  | `1`   | Label after the indicator (right/left). |
| `Bottom`| `2`   | Label below the indicator.            |
| `Start`| `3`   | Label before the indicator (left/right).|

### `BitSize` Enum

Used by the `Size` parameter.

| Name   | Value | Description                |
| :----- | :---- | :------------------------- |
| `Small`| `0`   | Renders the small size.  |
| `Medium`| `1`   | Renders the medium size. |
| `Large`| `2`   | Renders the large size.  |

### `BitVisibility` Enum

Used by the `Visibility` parameter.

| Name      | Value | Description                                                         |
| :-------- | :---- | :------------------------------------------------------------------ |
| `Visible` | `0`   | Component is rendered and visible.                                |
| `Hidden`  | `1`   | Component is hidden (`visibility: hidden`), but preserves space. |
| `Collapsed`| `2`   | Component is not rendered (`display: none`), consumes no space.    |

### `BitDir` Enum

Used by the `Dir` parameter to control text directionality.

| Name | Value | Description                                                   |
| :--- | :---- | :------------------------------------------------------------ |
| `Ltr`| `0`   | Left-to-right direction.                                    |
| `Rtl`| `1`   | Right-to-left direction.                                    |
| `Auto`| `2`   | Browser automatically determines direction based on content. |

---

## Feedback & Source Code

* **Report Issues:** [File an Issue on GitHub](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Start Discussions:** [Start a Discussion on GitHub](https://github.com/bitfoundation/bitplatform/discussions/new/choose)
* **View/Edit Page Source:** [Loading Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Progress/Loading/BitLoadingDemo.razor)
* **View/Edit Component Source:** [BitLoading Base Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Progress/Loading/Base/BitLoading.razor) (Note: Specific loader implementations like `BitBarsLoading` have their own files in nearby directories).
