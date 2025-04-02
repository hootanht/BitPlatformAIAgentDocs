# BitCircularTimePicker Component Reference (`.NET Blazor - Bit Blazor UI`)

## Overview

**Component Name:** `BitCircularTimePicker`

The `BitCircularTimePicker` component provides a user-friendly way to select a single time value (hour and minute) using a visual, clock-like interface. It's presented as a drop-down (callout) from an input field, making it suitable for forms and settings where selecting a specific time is required.

## Core Concepts & Features

*   **Time Selection:** Allows users to pick hours and minutes using a circular clock face interface.
*   **Input Field:** Displays the selected time and acts as the trigger for the time selection callout.
*   **Time Formatting:** Supports both 12-hour (AM/PM) and 24-hour formats (`TimeFormat` property). The displayed value can also be formatted using `ValueFormat`.
*   **Text Input:** Optionally allows users to type the time directly into the input field (`AllowTextInput` property). Requires input matching the specified `ValueFormat`.
*   **Standalone Mode:** Can be rendered directly as a clock face without the input field (`Standalone` property).
*   **Culture Support:** Adapts to different cultures (`Culture` property) for display formats and potentially AM/PM designators.
*   **Customization:**
    *   Labeling: `Label` property and `LabelTemplate` slot.
    *   Icon: Customizable trigger icon (`IconName`, `IconTemplate`) and location (`IconLocation`).
    *   Styling: `Style`, `Class`, and detailed `Styles`/`Classes` objects for granular control over internal elements (input, callout, clock face, numbers, pointer, etc.).
    *   Callout Control: Programmatic opening/closing (`IsOpen`, `OpenCallout` method). Option to show/hide the close button (`ShowCloseButton`).
*   **Data Binding:** Supports standard Blazor two-way data binding (`@bind-Value`) to a `TimeSpan?` variable.
*   **Validation:** Integrates with Blazor's `EditForm` and validation system (`DataAnnotationsValidator`, `ValidationMessage`, `InvalidErrorMessage`).
*   **States:** Supports `Enabled`, `Disabled`, and `ReadOnly` states.
*   **Responsiveness:** Adapts layout for smaller screens (`Responsive` property).
*   **RTL Support:** Supports Right-to-Left text direction (`Dir` property).

## Usage Examples

Below are examples demonstrating common configurations and features of the `BitCircularTimePicker`.

---

### Example 1: Basic Usage

Displays several basic configurations, including label, disabled state, required state, placeholder text, 12/24 hour format switching, and custom icon.

```cshtml
<BitCircularTimePicker Label="Basic CircularTimePicker" />
<BitCircularTimePicker Label="Disabled" IsEnabled="false" />
<BitCircularTimePicker Label="Required" Required />
<BitCircularTimePicker Label="PlaceHolder" Placeholder="Select a time" />
<BitCircularTimePicker Label="TimeFormat (AM/PM)" TimeFormat="BitTimeFormat.TwelveHours" />
<BitCircularTimePicker Label="Custom icon" IconName="@BitIconName.Airplane" />
```

---

### Example 2: Text Input Allowed

Demonstrates enabling direct text input into the field using `AllowTextInput="true"`. The input must match the specified `ValueFormat`.

```cshtml
<BitCircularTimePicker Label="Text input allowed"
                       AllowTextInput="true"
                       ValueFormat="hh:mm"
                       Placeholder="Enter a time (hh:mm)" />
```

*Note: When text input is allowed, clicking the input field opens the picker. Clicking it again while the picker is open closes the picker and enables text editing.*

---

### Example 3: Custom Value Format

Shows how to customize the display format of the selected time in the input field using the `ValueFormat` property.

```cshtml
<BitCircularTimePicker Label="Formatted time"
                       ValueFormat="hh-mm.ss" @* Example: 05-12.30 *@
                       Placeholder="Select a time" />
```

---

### Example 4: Data Binding

Illustrates two-way data binding using `@bind-Value` to link the selected time to a `TimeSpan?` variable in the C# code.

```cshtml
<BitCircularTimePicker @bind-Value="@selectedTime" />
<div>Selected time: @selectedTime?.ToString()</div>
```

```csharp
@code {
    private TimeSpan? selectedTime = new(5, 12, 15); // Example initial value
}
```

---

### Example 5: Culture Customization

Demonstrates using a specific `CultureInfo` (e.g., Farsi) to affect the display of AM/PM designators and potentially number rendering.

```cshtml
@using System.Globalization
@* Assumes CultureInfoHelper.GetFaIrCultureWithFarsiNames() provides a valid CultureInfo object *@

<BitCircularTimePicker Label="fa-IR culture"
                       TimeFormat="BitTimeFormat.TwelveHours"
                       Culture="CultureInfoHelper.GetFaIrCultureWithFarsiNames()" />
```

---

### Example 6: Standalone Mode

Renders the time picker clock face directly without the associated input field using the `Standalone="true"` property. Useful for embedding the picker directly into a custom UI.

```cshtml
<BitCircularTimePicker Label="Basic CircularTimePicker" Standalone />
<BitCircularTimePicker Label="Disabled" IsEnabled="false" Standalone />
<BitCircularTimePicker Label="PlaceHolder" Placeholder="Select a time" Standalone /> @* Placeholder not visible in standalone *@
<BitCircularTimePicker Label="TimeFormat (AM/PM)" TimeFormat="BitTimeFormat.TwelveHours" Standalone />
```

---

### Example 7: ReadOnly Mode

Shows the effect of `ReadOnly="true"`. The user can open the picker and see the selected time, but cannot change it via the UI or text input (if allowed). The bound value remains unchanged by user interaction.

```cshtml
<BitCircularTimePicker Label="Basic CircularTimePicker" ReadOnly @bind-Value="@readOnlyTime" />

<BitCircularTimePicker Label="Text input allowed" ReadOnly AllowTextInput @bind-Value="@readOnlyTime" />

<BitCircularTimePicker Label="Standalone CircularTimePicker" Standalone ReadOnly @bind-Value="@readOnlyTime" />

<BitCircularTimePicker Label="Standalone TimeFormat (AM/PM)" Standalone ReadOnly TimeFormat="BitTimeFormat.TwelveHours" @bind-Value="@readOnlyTime" />
```

```csharp
@code {
    private TimeSpan? readOnlyTime = new(2, 50, 0);
}
```

---

### Example 8: Custom Templates

Illustrates using `LabelTemplate` and `IconTemplate` to provide custom rendering for the label and the trigger icon. Also shows programmatically opening the callout using `@ref` and the `OpenCallout` method.

```cshtml
<BitCircularTimePicker @ref="circularTimePicker">
    <LabelTemplate>
        Custom label <BitButton Variant="BitVariant.Text" IconName="@BitIconName.AlarmClock" OnClick="OpenCallout"></BitButton>
    </LabelTemplate>
</BitCircularTimePicker>

<BitCircularTimePicker Label="Custom left-handed icon"
                       IconLocation="BitIconLocation.Left"
                       Placeholder="Select a time">
    <IconTemplate>
        <img src="https://img.icons8.com/fluency/2x/clock.png" width="24" height="24" />
    </IconTemplate>
</BitCircularTimePicker>
```

```csharp
@code {
    private BitCircularTimePicker circularTimePicker;

    private async Task OpenCallout()
    {
        await circularTimePicker.OpenCallout();
    }
}
```

---

### Example 9: Responsive Mode

Demonstrates the `Responsive` property, which adjusts the callout's appearance (often making it full-width or modal-like) on smaller screens for better usability.

```cshtml
<BitCircularTimePicker Label="Response CircularTimePicker"
                       Placeholder="Select a time"
                       Responsive />
```

---

### Example 10: Validation

Shows integration with Blazor's `EditForm` validation. A `[Required]` attribute on the model ensures a time must be selected. Also shows using `InvalidErrorMessage` for custom validation messages when `AllowTextInput` is enabled and invalid text is entered.

```cshtml
<style>
    .validation-summary { color: red; /* Basic styling for summary */ }
    .validation-message { color: red; }
</style>

<EditForm Model="formValidationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
    <DataAnnotationsValidator />

    <div class="validation-summary">
        <ValidationSummary />
    </div>

    <div>
        <BitCircularTimePicker @bind-Value="formValidationModel.Time"
                               AllowTextInput="true"
                               Placeholder="Select a time"
                               Label="Time required" />
        <ValidationMessage For="@(() => formValidationModel.Time)" />
    </div>
    <br />
    <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
</EditForm>

@if (!string.IsNullOrEmpty(successMessage))
{
    <BitMessage Color="BitColor.Success">@successMessage</BitMessage>
}

<hr />

<EditForm Model="formValidationModel">
    <DataAnnotationsValidator />
    <div>
        <BitCircularTimePicker @bind-Value="formValidationModel.Time"
                               AllowTextInput="true"
                               Label="Custom Invalid Error Message"
                               InvalidErrorMessage="Invalid Time!!!" /> @* Shown when text input is invalid *@
        <ValidationMessage For="@(() => formValidationModel.Time)" />
    </div>
    <br />
    <div class="validation-summary">
        <ValidationSummary />
    </div>
</EditForm>
```

```csharp
@using System.ComponentModel.DataAnnotations;

@code {
    public class FormValidationCircularTimePickerModel
    {
        [Required(ErrorMessage = "Please select a time.")]
        public TimeSpan? Time { get; set; }
    }

    private FormValidationCircularTimePickerModel formValidationModel = new();
    private string successMessage = string.Empty;

    private async Task HandleValidSubmit()
    {
        successMessage = "Form Submitted Successfully!";
        await Task.Delay(3000); // Simulate submission
        successMessage = string.Empty;
        formValidationModel = new(); // Reset form
        StateHasChanged();
    }

    private void HandleInvalidSubmit()
    {
        successMessage = string.Empty;
        // Optional: Logic for invalid submission
    }
}
```

---

### Example 11: Style & Class Customization

Demonstrates extensive customization using inline `Style`, CSS `Class` on the root, and the `Styles` and `Classes` parameters to target internal elements like the input, callout, toolbar, clock face, pointer, and numbers.

```cshtml
<style>
    /* Example CSS rules (simplified from original HTML) */
    .custom-class { /* Styles for the root element via Class */ }
    .custom-root { /* Styles for the root element via Classes */ }
    .custom-label { /* Styles for the label via Classes */ }
    .custom-input { /* Styles for the input element via Classes */ }
    .custom-input-container { /* Styles for the input container via Classes */ }
    .custom-focus .custom-input-container::after { /* Focus effect via Classes */ }
    .custom-toolbar { /* Styles for the callout toolbar via Classes */ }
    .custom-clock-face { /* Styles for the clock face via Classes */ }
    /* ... other custom classes for clock elements ... */
</style>

@* Component's Style & Class: *@
<BitCircularTimePicker Style="margin: 1rem; box-shadow: dodgerblue 0 0 1rem;" />
<BitCircularTimePicker Class="custom-class" />

@* Styles & Classes objects for granular control: *@
<BitCircularTimePicker Label="Styles Demo"
                       Styles="@(new() { Root = "margin-inline: 1rem;",
                                         Focused = "--focused-background: #b2b2b25a;", /* Example CSS Variable */
                                         Input = "padding: 0.5rem;",
                                         InputContainer = "background: var(--focused-background);",
                                         HourButton = "color: gray;",
                                         MinuteButton = "color: gray;",
                                         HourMinuteSeparator = "color: gray;",
                                         Toolbar = "background-color: transparent;",
                                         ClockFace= "box-shadow: dodgerblue 0 0 1rem;",
                                         ClockPointerThumb = "background-color: blue;" })" />

<BitCircularTimePicker @bind-Value="@classesValue"
                       Label="Classes Demo"
                       Classes="@(new() { Root = "custom-root",
                                          Focused = "custom-focus",
                                          Input = "custom-input",
                                          InputContainer = "custom-input-container",
                                          Label = $"custom-label{(classesValue is null ? string.Empty : " custom-label-top")}",
                                          Toolbar = "custom-toolbar",
                                          ClockPin = "custom-clock-pin",
                                          ClockFace = "custom-clock-face",
                                          ClockNumber = "custom-clock-number",
                                          ClockPointer = "custom-clock-pointer",
                                          ClockPointerThumb = "custom-clock-pointer-thumb",
                                          ClockSelectedNumber = "custom-clock-selected-number",
                                          ClockPointerThumbMinute = "custom-clock-pointer-thumb-minute" })" />

```

```csharp
@code {
    private TimeSpan? classesValue;
}
```

---

### Example 12: RTL (Right-to-Left) Support

Shows how to render the `BitCircularTimePicker` in a Right-to-Left layout using `Dir="BitDir.Rtl"`.

```cshtml
<div dir="rtl"> @* Container div sets overall direction *@
    <BitCircularTimePicker Dir="BitDir.Rtl" Label="انتخابگر زمان (راست به چپ)" />
</div>
```

---

## API Reference

### `BitCircularTimePicker` Parameters

Parameters specific to or overriding behavior for the `BitCircularTimePicker` component.

| Name                      | Type                                  | Default Value                       | Description                                                                                                      |
| :------------------------ | :------------------------------------ | :---------------------------------- | :--------------------------------------------------------------------------------------------------------------- |
| `AllowTextInput`          | `bool`                                | `false`                             | If true, allows the user to type a time directly into the input field. Parsing requires matching `ValueFormat`.  |
| `AutoClose`               | `bool`                                | `false`                             | (Currently seems less relevant without explicit picker actions) Intended to auto-close after selection if actions were present. |
| `CalloutAriaLabel`        | `string`                              | `"Clock"`                           | Aria-label for the time picker callout/popup, used by screen readers.                                             |
| `CalloutHtmlAttributes`   | `Dictionary<string, object>`          | `new Dictionary<string, object>()`  | Additional HTML attributes to apply to the callout wrapper element.                                              |
| `Classes`                 | `BitCircularTimePickerClassStyles?`   | `null`                              | Custom CSS classes for different internal parts. See `BitCircularTimePickerClassStyles` section below.             |
| `CloseButtonTitle`        | `string`                              | `"Close time picker"`               | Tooltip text for the close button inside the callout (if `ShowCloseButton` is true).                            |
| `Culture`                 | `CultureInfo`                         | `CultureInfo.CurrentUICulture`      | Specifies the culture used for formatting time (e.g., AM/PM designators).                                        |
| `EditMode`                | `BitCircularTimePickerEditMode`       | `Normal`                            | Controls which parts (hour/minute) are editable in the clock face. See enum below.                              |
| `HasBorder`               | `bool`                                | `true`                              | If `false`, removes the default border around the input field wrapper.                                           |
| `IconLocation`            | `BitIconLocation`                     | `Right`                             | Position of the trigger icon (Left or Right). See enum below.                                                   |
| `IconName`                | `string`                              | `"Clock"`                           | Name of the icon (from `BitIconName` or custom font) displayed as the trigger.                                   |
| `IconTemplate`            | `RenderFragment?`                     | `null`                              | Custom `RenderFragment` for rendering the trigger icon. Overrides `IconName`.                                    |
| `InvalidErrorMessage`     | `string?`                             | `null`                              | Custom error message displayed when `AllowTextInput` is true and the entered text is invalid.                   |
| `IsOpen`                  | `bool`                                | `false`                             | Controls the visibility of the time picker callout. Can be used with `@bind-IsOpen` for programmatic control.  |
| `Label`                   | `string?`                             | `null`                              | Text label displayed above or next to the input field.                                                          |
| `LabelTemplate`           | `RenderFragment?`                     | `null`                              | Custom `RenderFragment` for rendering the label. Overrides `Label`.                                             |
| `OnClick`                 | `EventCallback`                       |                                     | Callback invoked when the input wrapper (the clickable area) is clicked.                                         |
| `OnFocus`                 | `EventCallback`                       |                                     | Callback invoked when the input element receives focus (bubbles).                                                |
| `OnFocusIn`               | `EventCallback`                       |                                     | Callback invoked when the input element receives focus (does not bubble).                                        |
| `OnFocusOut`              | `EventCallback`                       |                                     | Callback invoked when the input element loses focus.                                                             |
| `OnSelectTime`            | `EventCallback<TimeSpan?>`            |                                     | Callback invoked when a time is selected from the clock face or successfully parsed from text input.           |
| `Placeholder`             | `string?`                             | `null`                              | Placeholder text displayed in the input field when no value is selected.                                         |
| `Responsive`              | `bool`                                | `false`                             | If `true`, enables responsive behavior, adjusting the callout layout on smaller screens.                      |
| `ShowCloseButton`         | `bool`                                | `false`                             | If `true`, displays a close button within the time picker callout header.                                        |
| `Standalone`              | `bool`                                | `false`                             | If `true`, renders only the clock face UI without the input field and callout mechanism.                        |
| `Styles`                  | `BitCircularTimePickerClassStyles?`   | `null`                              | Custom CSS inline styles for different internal parts. See `BitCircularTimePickerClassStyles` section below.       |
| `TabIndex`                | `int`                                 | `0`                                 | The `tabindex` attribute for the input field, controlling focus order.                                           |
| `TimeFormat`              | `BitTimeFormat`                       | `TwentyFourHours`                   | Specifies whether to use 12-hour (AM/PM) or 24-hour format in the clock face UI. See enum below.           |
| `Underlined`              | `bool`                                | `false`                             | If `true`, applies an underlined style to the input field instead of the default border.                         |
| `ValueFormat`             | `string?`                             | `null`                              | Specifies the format string used to display the selected `Value` in the input field (e.g., "HH:mm", "hh:mm tt"). Also used for parsing when `AllowTextInput` is true. Defaults to culture-specific short time format. |
| **Inherited Parameters**  |                                       |                                     | *Includes parameters from `BitInputBase<TimeSpan?>` and `BitComponentBase` (see following sections).*            |

---

### `BitCircularTimePicker` Public Members

Methods accessible via `@ref`.

| Name           | Type            | Description                                           |
| :------------- | :-------------- | :---------------------------------------------------- |
| `OpenCallout()`| `Task`          | Programmatically opens the time picker callout/popup. |
| `CloseCallout()`| `Task`         | Programmatically closes the time picker callout/popup.|

---

### `BitInputBase<TValue>` Parameters (Inherited by `BitCircularTimePicker`, where `TValue` is `TimeSpan?`)

Base class for input components, handling value binding and validation integration.

| Name                | Type                                  | Default Value | Description                                                                                                         |
| :------------------ | :------------------------------------ | :------------ | :------------------------------------------------------------------------------------------------------------------ |
| `DisplayName`       | `string?`                             | `null`        | A user-friendly name for the field, used in validation error messages. If not set, derived from `ValueExpression`. |
| `InputHtmlAttributes` | `IReadOnlyDictionary<string, object>?`| `null`        | Additional HTML attributes to apply directly to the underlying `<input type="text">` element used for display/text input. |
| `Name`              | `string?`                             | `null`        | The `name` attribute of the input element, useful for form submission or JavaScript interaction.                 |
| `NoValidate`        | `bool`                                | `false`       | If `true`, suppresses the generation of validation attributes (like `required`) on the input element.            |
| `OnChange`          | `EventCallback<TValue?>` (`TimeSpan?`)|               | A callback invoked when the `Value` changes (either by selection or text input).                                    |
| `ReadOnly`          | `bool`                                | `false`       | If `true`, makes the input field non-editable and prevents opening the callout via click.                         |
| `Required`          | `bool`                                | `false`       | If `true`, adds required styling cues. Validation logic relies on model attributes (e.g., `[Required]`).           |
| `Value`             | `TValue?` (`TimeSpan?`)               | `null`        | The current `TimeSpan` value. Use with `@bind-Value` for two-way data binding.                                   |
| `ValueChanged`      | `EventCallback<TValue?>` (`TimeSpan?`)|               | An `EventCallback` used implicitly by `@bind-Value` for two-way binding updates.                                  |
| `ValueExpression`   | `Expression<Func<TValue?>>?`          | `null`        | An expression used implicitly by `@bind-Value` to identify the bound property, enabling validation integration. |

---

### `BitInputBase<TValue>` Public Members (Inherited by `BitCircularTimePicker`)

| Name                      | Type                 | Description                                                                                                |
| :------------------------ | :------------------- | :--------------------------------------------------------------------------------------------------------- |
| `InputElement`            | `ElementReference`   | Provides a reference to the underlying `<input type="text">` element.                                      |
| `FocusAsync()`            | `() => ValueTask`    | Programmatically sets focus to the input element.                                                          |
| `FocusAsync(bool preventScroll)` | `(bool) => ValueTask`| Programmatically sets focus, optionally preventing the browser from scrolling the element into view. |

---

### `BitComponentBase` Parameters (Base for all Bit components, Inherited by `BitCircularTimePicker`)

Common parameters for all Bit Blazor UI components.

| Name             | Type                            | Default Value                       | Description                                                                                                 |
| :--------------- | :------------------------------ | :---------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                              | Defines a string value that labels the input element for accessibility, overriding the visual `Label` association if needed. |
| `Class`          | `string?`                       | `null`                              | Custom CSS class(es) to apply to the root element (`div`) of the component.                                 |
| `Dir`            | `BitDir?`                       | `null`                              | Sets the text direction (`ltr`, `rtl`, `auto`) for the component. See `BitDir` enum below.                    |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()`  | Allows capturing and rendering arbitrary HTML attributes (splatting) on the root element (`div`) of the component. |
| `Id`             | `string?`                       | `null`                              | Custom `id` attribute for the root element (`div`). If not provided, the component's `UniqueId` is used.      |
| `IsEnabled`      | `bool`                          | `true`                              | Whether the component is enabled. If `false`, it appears grayed out and cannot be interacted with.          |
| `Style`          | `string?`                       | `null`                              | Custom inline CSS style(s) to apply to the root element (`div`) of the component.                           |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`             | Controls whether the component is visible, hidden (occupies space), or collapsed (no space). See `BitVisibility` enum below. |

---

### `BitComponentBase` Public Members (Base for all Bit components, Inherited by `BitCircularTimePicker`)

| Name          | Type               | Default Value    | Description                                                                                                      |
| :------------ | :----------------- | :--------------- | :--------------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()` | A read-only, unique identifier (GUID) generated automatically for each component instance. Useful for `id` refs. |
| `RootElement` | `ElementReference` |                  | Provides a reference to the root HTML element (`div`) of the component.                                          |

---

### `BitCircularTimePickerClassStyles` Properties (Used by `Classes` and `Styles` parameters)

Defines CSS classes or styles for specific internal parts of the `BitCircularTimePicker`.

| Property                | Type      | Description                                                               | Maps to Element(s)           |
| :---------------------- | :-------- | :------------------------------------------------------------------------ | :--------------------------- |
| `Root`                  | `string?` | The main container `div` element.                                         | Root `div.bit-ctp`           |
| `Focused`               | `string?` | Class/style applied to the `Root` when the input has focus.               | Root `div.bit-ctp`           |
| `Label`                 | `string?` | The `<label>` element.                                                    | `label.bit-ctp-lbl`          |
| `InputWrapper`          | `string?` | The `div` wrapping the input and icon.                                    | `div.bit-ctp-wrp`            |
| `InputContainer`        | `string?` | The `div` directly containing the input and icon elements.                 | `div.bit-ctp-icn`            |
| `Input`                 | `string?` | The `<input type="text">` element.                                        | `input.bit-ctp-inp`          |
| `Icon`                  | `string?` | The icon element (`<i>` or custom template) used as the trigger.          | `i.bit-ctp-ico` / Template   |
| `Overlay`               | `string?` | The overlay `div` shown behind the callout when open (if applicable).   | `div.bit-ctp-ovl`            |
| `Callout`               | `string?` | The main callout `div` element containing the clock UI.                   | `div.bit-ctp-cal`            |
| `CalloutContainer`      | `string?` | The inner container `div` within the callout, holding the content.        | `div.bit-ctp-cac`            |
| `Toolbar`               | `string?` | The header `div` in the callout containing hour/minute/AM/PM controls.    | `div.bit-ctp-tbr`            |
| `HourMinuteContainer`   | `string?` | The `div` specifically holding the hour, separator, and minute buttons.   | `div.bit-ctp-hmc`            |
| `HourButton`            | `string?` | The `<button>` displaying/selecting the hour.                             | `button.bit-ctp-txt` (hour)  |
| `MinuteButton`          | `string?` | The `<button>` displaying/selecting the minute.                           | `button.bit-ctp-txt` (minute)|
| `HourMinuteSeparator`   | `string?` | The `<span>` separating the hour and minute buttons.                      | `span.bit-ctp-txt` (:)       |
| `HourMinuteText`        | `string?` | General style for the text inside hour/minute/separator elements.         | `button/span.bit-ctp-txt`    |
| `AmPmContainer`         | `string?` | The `div` holding the AM and PM buttons (in 12-hour mode).              | `div.bit-ctp-apc`            |
| `AmButton`              | `string?` | The `<button>` for selecting AM.                                          | `button.bit-ctp-apb` (AM)    |
| `PmButton`              | `string?` | The `<button>` for selecting PM.                                          | `button.bit-ctp-apb` (PM)    |
| `SelectedButtons`       | `string?` | Class/style applied to the *currently active* hour/minute/AM/PM button.   | `button.bit-ctp-ina`         |
| `ClockContainer`        | `string?` | The `div` containing the clock face itself.                               | `div.bit-ctp-clk`            |
| `ClockFace`             | `string?` | The main `div` representing the circular clock face background/area.      | `div.bit-ctp-clf`            |
| `ClockPin`              | `string?` | The central pin `div` element on the clock face.                        | `div.bit-ctp-pin`            |
| `ClockNumber`           | `string?` | The `<p>` elements displaying the hour/minute numbers around the clock.    | `p.bit-ctp-num`              |
| `ClockSelectedNumber`   | `string?` | Class/style applied to the currently selected number (`<p>`).           | `p.bit-ctp-sel`              |
| `ClockPointer`          | `string?` | The `div` representing the clock pointer/hand.                            | `div.bit-ctp-ptr`            |
| `ClockPointerThumb`     | `string?` | The `div` at the end of the clock pointer (the thumb).                   | `div.bit-ctp-pth`            |
| `ClockPointerThumbMinute`| `string?`| Specific class/style for the minute pointer thumb (may differ slightly). | `div.bit-ctp-pth` (minute)   |
| `CloseButton`           | `string?` | The close `<button>` element in the callout header (if shown).          | (Not explicitly shown in HTML, likely internal)|
| `CloseButtonIcon`       | `string?` | The icon (`<i>`) inside the close button.                               | (Not explicitly shown in HTML, likely internal)|

---

### Related Enums

#### `BitTimeFormat` Enum (for `TimeFormat` parameter)

| Name              | Value | Description                                      |
| :---------------- | :---- | :----------------------------------------------- |
| `TwentyFourHours` | 0     | Use 24-hour format (00-23) in the clock UI.    |
| `TwelveHours`     | 1     | Use 12-hour format (1-12 with AM/PM) in the clock UI. |

#### `BitCircularTimePickerEditMode` Enum (for `EditMode` parameter)

| Name          | Value | Description                                 |
| :------------ | :---- | :------------------------------------------ |
| `Normal`      | 0     | Both hours and minutes can be edited.       |
| `OnlyMinutes` | 1     | Only the minutes part can be edited.        |
| `OnlyHours`   | 2     | Only the hours part can be edited.          |

#### `BitIconLocation` Enum (for `IconLocation` parameter)

| Name    | Value | Description                          |
| :------ | :---- | :----------------------------------- |
| `Left`  | 0     | Render the icon to the left of the input. |
| `Right` | 1     | Render the icon to the right of the input. |

#### `BitVisibility` Enum (for `Visibility` parameter)

Controls the rendering and visibility of the component.

| Name        | Value | Description                                                                        | CSS Effect           |
| :---------- | :---- | :--------------------------------------------------------------------------------- | :------------------- |
| `Visible`   | 0     | The component is rendered and visible (default).                                   | (standard display)   |
| `Hidden`    | 1     | The component is not visible, but still occupies its space in the layout.          | `visibility: hidden` |
| `Collapsed` | 2     | The component is not rendered and does not occupy any space in the layout.         | `display: none`      |

#### `BitDir` Enum (for `Dir` parameter)

Specifies the text directionality of the component's content.

| Name   | Value | Description                                                                                                  | Corresponds to HTML `dir` |
| :----- | :---- | :----------------------------------------------------------------------------------------------------------- | :------------------------ |
| `Ltr`  | 0     | Left-to-right text direction (e.g., English).                                                                | `ltr`                     |
| `Rtl`  | 1     | Right-to-left text direction (e.g., Arabic, Hebrew).                                                         | `rtl`                     |
| `Auto` | 2     | The browser determines the direction based on the text content using a basic algorithm.                        | `auto`                    |

---

## Key Considerations & Best Practices

* **Value Type:** The component binds to a `TimeSpan?` (nullable TimeSpan). Ensure your model property matches this type.
* **Text Input Parsing:** When `AllowTextInput` is true, the component attempts to parse the entered text based on the `ValueFormat` and `Culture`. If parsing fails, the value might become null or trigger validation errors. Provide clear `Placeholder` text and consider using `InvalidErrorMessage` for better user feedback.
* **Formatting:** Use `ValueFormat` to control how the selected time is displayed in the input field. Standard .NET TimeSpan format strings can be used (e.g., `hh\:mm`, `HH:mm:ss`, `hh:mm tt`).
* **Standalone Usage:** When `Standalone` is true, the component only renders the clock UI. You'll typically handle the `Value` binding and potentially `OnSelectTime` callback to integrate it into your custom layout. The input-related parameters (`Placeholder`, `Label`, `IconName`, etc.) have no effect in standalone mode.
* **Responsiveness:** Enable the `Responsive` flag for better usability on mobile devices, where the callout might become a full-screen modal or adopt a different layout.
* **Accessibility:** Ensure a `Label` or `LabelTemplate` is provided for screen reader association. The `CalloutAriaLabel` helps describe the popup's purpose.

