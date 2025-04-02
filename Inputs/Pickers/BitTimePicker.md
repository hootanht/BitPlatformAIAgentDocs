# BitTimePicker Component Reference

**Purpose:** This document provides a comprehensive reference for the `BitTimePicker` Blazor component. It includes usage examples, API documentation, and styling information intended for use by AI coding assistants (like GitHub Copilot, Cursor) to provide accurate context and code suggestions.

## Overview

A `BitTimePicker` offers a drop-down control optimized for picking a single time value using a clock interface. It's suitable when contextual information (like day of the week, etc., although less relevant for *time* picking specifically) might be considered alongside time selection. The component allows customization of its appearance and behavior, including limiting available times.

## Usage Examples

Here are various ways to use the `BitTimePicker` component:

### 1. Basic Usage

Demonstrates basic instantiation, including disabled, required, and placeholder options.

```cshtml
<BitTimePicker Label="Basic TimePicker" />
<BitTimePicker Label="Disabled" IsEnabled="false" />
<BitTimePicker Label="Required" Required />
<BitTimePicker Label="Placeholder" Placeholder="Select a time..." />
```

### 2. Time Format (12/24 Hour)

Shows how to configure the time picker for 12-hour (AM/PM) or 24-hour format using the `TimeFormat` parameter.

```cshtml
<BitTimePicker TimeFormat="BitTimeFormat.TwelveHours"
               Placeholder="Select a time..."
               Label="12 hours (AM/PM)" />

<BitTimePicker TimeFormat="BitTimeFormat.TwentyFourHours"
               Placeholder="Select a time..."
               Label="24 hours" />
```

### 3. Allow Text Input

Enables users to type the time directly into the input field using the `AllowTextInput` parameter. Note: The entered time must match the component's `TimeFormat`.

```cshtml
<BitTimePicker AllowTextInput Label="Start time" />
```

### 4. Custom Icon

Customizes the icon displayed in the time picker input using `IconName` and controls its position with `IconLocation`.

```cshtml
<BitTimePicker IconName="@BitIconName.HourGlass" Placeholder="Select a time..." />

<BitTimePicker IconName="@BitIconName.HourGlass"
               IconLocation="BitIconLocation.Left"
               Placeholder="Select a time..." />
```

### 5. Value Formatting

Customizes how the selected time value is formatted in the input field using the `ValueFormat` parameter.

```cshtml
<BitTimePicker Placeholder="Select a time..." ValueFormat="hh-mm.ss" />
```

### 6. Data Binding

Demonstrates two-way data binding using `@bind-Value` to link the selected time to a C# `TimeSpan?` variable.

```cshtml
<BitTimePicker @bind-Value="@selectedTime" Placeholder="Select a time..." />
<div>Selected time: @selectedTime?.ToString()</div>
```

```csharp
@code {
    private TimeSpan? selectedTime = new(5, 12, 15);
}
```

### 7. Standalone Mode

Renders the time picker clock view directly without the input field using the `Standalone` parameter.

```cshtml
<BitTimePicker Standalone Label="Standalone picker" />

<BitTimePicker Standalone
               Label="Picker (AM/PM)"
               TimeFormat="BitTimeFormat.TwelveHours" />

<BitTimePicker Standalone
               Label="Disabled"
               IsEnabled="false"
               Value="new(10, 24, 0)"
               TimeFormat="BitTimeFormat.TwelveHours" />
```

### 8. ReadOnly Mode

Makes the time picker input non-editable using the `ReadOnly` parameter, preventing users from manually changing the time value via typing (if `AllowTextInput` is true) or interaction with the picker controls.

```cshtml
<BitTimePicker Label="Basic" ReadOnly @bind-Value="@readOnlyTime" />
<BitTimePicker Label="Text input allowed" ReadOnly AllowTextInput @bind-Value="@readOnlyTime" />
<BitTimePicker Label="Standalone" Standalone ReadOnly @bind-Value="@readOnlyTime" />
<BitTimePicker Label="Standalone TimeFormat (AM/PM)" Standalone ReadOnly TimeFormat="BitTimeFormat.TwelveHours" @bind-Value="@readOnlyTime" />
```

```csharp
@code {
    private TimeSpan? readOnlyTime = new(2, 50, 0);
}
```

### 9. Form Validation

Integrates `BitTimePicker` within an `EditForm` for validation using standard Blazor validation attributes and components.

```cshtml
<EditForm Model="formValidationTimePickerModel" OnValidSubmit="HandleValidSubmit">
    <DataAnnotationsValidator />
    <div class="validation-summary">
        <ValidationSummary />
    </div>
    <div class="example-content">
        <BitTimePicker @bind-Value="formValidationTimePickerModel.Time"
                       AllowTextInput
                       Label="Time required"
                       AriaLabel="Select a time"
                       Placeholder="Select a time..."
                       InvalidErrorMessage="Invalid Time!" />
        <ValidationMessage For="@(() => formValidationTimePickerModel.Time)" />
    </div>
    <br />
    <BitButton ButtonType="BitButtonType.Submit">
        Submit
    </BitButton>
</EditForm>
```

```csharp
@code {
    public class FormValidationTimePickerModel
    {
        [Required(ErrorMessage = "Time is required.")] // Example validation attribute
        public TimeSpan? Time { get; set; }
    }

    private FormValidationTimePickerModel formValidationTimePickerModel = new();

    private async Task HandleValidSubmit()
    {
        Console.WriteLine("Form Submitted Successfully!");
        // Simulate submission logic
        await Task.Delay(1000);
        // Optionally reset form
        // formValidationTimePickerModel = new();
        // StateHasChanged();
    }
}
```

*Note: The C# model in the original HTML seems to use `DateTimeOffset?` and a different class name (`FormValidationCircularTimePickerModel`). The example here is adjusted for a more typical `TimeSpan?` validation scenario for `BitTimePicker`.*

### 10. Responsive Mode

Makes the time picker callout adapt to smaller screens using the `Responsive` parameter. `ShowCloseButton` adds a close button, often useful in responsive/mobile views.

```cshtml
<BitTimePicker Responsive
               ShowCloseButton
               Placeholder="Select a time..." />
```

### 11. Custom Templates (Label & Icon)

Allows customizing the `Label` and `Icon` sections using `LabelTemplate` and `IconTemplate`.

```cshtml
<BitTimePicker @ref="timePicker" Placeholder="Select a time...">
    <LabelTemplate>
        Custom label <BitButton Variant="BitVariant.Text" IconName="@BitIconName.AlarmClock" OnClick="OpenCallout"></BitButton>
    </LabelTemplate>
</BitTimePicker>

<BitTimePicker Label="Custom icon" Placeholder="Select a time...">
    <IconTemplate>
        <img src="https://img.icons8.com/fluency/2x/clock.png" width="24" height="24" />
    </IconTemplate>
</BitTimePicker>
```

```csharp
@code {
    private BitTimePicker timePicker;

    private async Task OpenCallout()
    {
        await timePicker.OpenCallout();
    }
}
```

### 12. Hour/Minute Step

Configures the increment/decrement step for hours and minutes using `HourStep` and `MinuteStep`.

```cshtml
<BitTimePicker HourStep="2"
               Label="HourStep = 2"
               Placeholder="Select a time..." />

<BitTimePicker MinuteStep="15"
               Label="MinuteStep = 15"
               Placeholder="Select a time..." />
```

### 13. Style & Class Customization

Demonstrates applying custom CSS via `Style`, `Class`, `Styles`, and `Classes` parameters.

**Inline Style & CSS Class:**

```cshtml
<style>
    .custom-class {
        overflow: hidden;
        margin-inline: 1rem;
        border-radius: 1rem;
        border: 2px solid tomato;
    }
    .custom-class *, .custom-class *:after { /* Example: Reset internal borders */
        border: none;
    }
</style>

<BitTimePicker Style="margin: 1rem; box-shadow: dodgerblue 0 0 1rem;" />
<BitTimePicker Class="custom-class" />
```

**Detailed Styles & Classes Parameters:**

```css
/* Add these styles to your app's CSS */
.custom-root {
    height: 3rem; margin: 1rem; display: flex; align-items: end;
    position: relative; border-radius: 0.5rem;
}
.custom-label {
    top: 0; left: 0; z-index: 1; padding: 0; font-size: 1rem;
    color: darkgray; position: absolute; transform-origin: top left;
    transform: translate(0, 22px) scale(1);
    transition: color 200ms cubic-bezier(0, 0, 0.2, 1) 0ms, transform 200ms cubic-bezier(0, 0, 0.2, 1) 0ms;
}
.custom-label-top { /* Applied when there's a value */
    transform: translate(0, 1.5px) scale(0.75);
}
.custom-input { padding: 0; font-size: 1rem; font-weight: 900; }
.custom-input-container { border-radius: 0; position: relative; border-width: 0 0 1px 0; }
.custom-input-container::after {
    content: ''; width: 0; height: 2px; border: none; position: absolute;
    inset: 100% 0 0 50%; background-color: blueviolet;
    transition: width 0.3s ease, left 0.3s ease;
}
.custom-focus .custom-input-container::after { left: 0; width: 100%; }
.custom-focus .custom-label { color: blueviolet; transform: translate(0, 1.5px) scale(0.75); }
.custom-button { border-radius: 50%; background-color: blueviolet; }
```

```cshtml
<BitTimePicker Placeholder="Select a time..."
               Styles="@(new() { Root = "margin-inline: 1rem;",
                                 Focused = "--focused-background: #b2b2b25a;", // Custom CSS variable example
                                 Input = "padding: 0.5rem;",
                                 InputContainer = "background: var(--focused-background);",
                                 IncreaseHourButton = "color: dodgerblue;",
                                 DecreaseHourButton = "color: dodgerblue;",
                                 IncreaseMinuteButton = "color: dodgerblue;",
                                 DecreaseMinuteButton = "color: dodgerblue;" })" />

<BitTimePicker @bind-Value="@classesValue"
               Label="Select a time"
               Classes="@(new() { Root = "custom-root",
                                  Focused = "custom-focus",
                                  Input = "custom-input",
                                  InputContainer = "custom-input-container",
                                  Label = $"custom-label{(classesValue is null ? string.Empty : " custom-label-top")}",
                                  IncreaseHourButton = "custom-button",
                                  DecreaseHourButton = "custom-button",
                                  IncreaseMinuteButton = "custom-button",
                                  DecreaseMinuteButton = "custom-button" })" />
```

```csharp
@code {
    private TimeSpan? classesValue;
}
```

### 14. Right-to-Left (RTL)

Configures the component for RTL layouts using the `Dir` parameter.

```cshtml
<BitTimePicker Dir="BitDir.Rtl"
               Standalone
               Label="تایم"
               Value="new(10, 24, 0)"
               TimeFormat="BitTimeFormat.TwelveHours" />

<BitTimePicker Dir="BitDir.Rtl"
               ShowCloseButton
               Label="تایم"
               Placeholder="تایم خود را انتخاب کنید..." />
```

## API Reference

### BitTimePicker Parameters

| Name                  | Type                              | Default Value                  | Description                                                                                            |
| :-------------------- | :-------------------------------- | :----------------------------- | :----------------------------------------------------------------------------------------------------- |
| `AllowTextInput`      | `bool`                            | `false`                        | Whether the TimePicker allows direct input of a time string.                                           |
| `CalloutAriaLabel`    | `string`                          | `"Clock"`                      | Aria label for the time picker popup (callout) for screen readers.                                     |
| `CalloutHtmlAttributes`| `Dictionary<string, object>`      | `new()`                        | Additional HTML attributes for the callout element.                                                    |
| `Classes`             | `BitTimePickerClassStyles?`       | `null`                         | Custom CSS classes for different internal elements of the TimePicker. See `BitTimePickerClassStyles`.    |
| `CloseButtonTitle`    | `string`                          | `"Close time picker"`          | Tooltip text for the close button (if `ShowCloseButton` is true).                                      |
| `Culture`             | `CultureInfo`                     | `CultureInfo.CurrentUICulture` | Specifies the culture for formatting and parsing time values.                                          |
| `DropDirection`       | `BitDropDirection`                | `TopAndBottom`                 | Determines the preferred opening direction of the callout.                                             |
| `HasBorder`           | `bool`                            | `true`                         | Determines if the TimePicker input field has a border.                                                 |
| `HourStep`            | `int`                             | `1`                            | The step value for incrementing/decrementing the hour.                                                 |
| `IconName`            | `string?`                         | `"Clock"`                      | The name of the BitFluentIcon to display.                                                              |
| `IconLocation`        | `BitIconLocation`                 | `Right`                        | Position of the icon within the input field (Left or Right).                                           |
| `IconTemplate`        | `RenderFragment?`                 | `null`                         | Custom Razor content to render as the icon. Overrides `IconName`.                                      |
| `IsOpen`              | `bool`                            | `false`                        | Controls whether the time picker callout is currently open. Use `@bind-IsOpen` for two-way binding.    |
| `Label`               | `string?`                         | `null`                         | Text label displayed above the time picker input.                                                      |
| `LabelTemplate`       | `RenderFragment?`                 | `null`                         | Custom Razor content for the label area. Overrides `Label`.                                            |
| `MinuteStep`          | `int`                             | `1`                            | The step value for incrementing/decrementing the minute.                                               |
| `OnClick`             | `EventCallback<MouseEventArgs>`   | ``                            | Callback invoked when the time picker input area is clicked.                                           |
| `OnFocus`             | `EventCallback<FocusEventArgs>`   | ``                            | Callback invoked when the component receives focus (combined focus event).                             |
| `OnFocusIn`           | `EventCallback<FocusEventArgs>`   | ``                            | Callback invoked when focus enters the component.                                                      |
| `OnFocusOut`          | `EventCallback<FocusEventArgs>`   | ``                            | Callback invoked when focus leaves the component.                                                      |
| `OnSelectTime`        | `EventCallback<TimeSpan?>`        | ``                            | Callback invoked when a time is selected or cleared.                                                   |
| `Placeholder`         | `string?`                         | `null`                         | Placeholder text displayed in the input field when no value is selected.                               |
| `Responsive`          | `bool`                            | `false`                        | Enables responsive mode, typically making the callout full-width on small screens.                     |
| `ShowCloseButton`     | `bool`                            | `false`                        | Shows a close button within the callout, useful for `Responsive` mode.                                 |
| `Styles`              | `BitTimePickerClassStyles?`       | `null`                         | Custom inline CSS styles for different internal elements of the TimePicker. See `BitTimePickerClassStyles`. |
| `Standalone`          | `bool`                            | `false`                        | Renders only the clock view (callout content) without the input field wrapper.                         |
| `TabIndex`            | `int`                             | `0`                            | The tab index of the time picker input field.                                                          |
| `TimeFormat`          | `BitTimeFormat`                   | `TwentyFourHours`              | Specifies whether to use 12-hour (AM/PM) or 24-hour format.                                            |
| `Underlined`          | `bool`                            | `false`                        | Renders the input field with an underline style instead of a full border.                              |
| `ValueFormat`         | `string?`                         | `null`                         | A standard or custom .NET time format string to control how the selected `Value` is displayed.       |
| **Inherited Parameters** |                                   |                                | (See BitInputBase and BitComponentBase sections below)                                                 |
| `Value`               | `TimeSpan?`                       | `null`                         | The selected time value. Use `@bind-Value` for two-way binding. (Inherited from `BitInputBase<TimeSpan?>`) |
| `IsEnabled`           | `bool`                            | `true`                         | Whether the component is enabled. (Inherited from `BitComponentBase`)                                  |
| `Visibility`          | `BitVisibility`                   | `Visible`                      | Controls component visibility (`Visible`, `Hidden`, `Collapsed`). (Inherited from `BitComponentBase`)    |
| `Id`                  | `string?`                         | `null`                         | Custom HTML id for the root element. (Inherited from `BitComponentBase`)                               |
| `Style`               | `string?`                         | `null`                         | Custom inline CSS style for the root element. (Inherited from `BitComponentBase`)                      |
| `Class`               | `string?`                         | `null`                         | Custom CSS class for the root element. (Inherited from `BitComponentBase`)                             |
| `AriaLabel`           | `string?`                         | `null`                         | Aria-label for accessibility. (Inherited from `BitComponentBase`)                                      |
| `Dir`                 | `BitDir?`                         | `null`                         | Sets the text direction (`Ltr`, `Rtl`, `Auto`). (Inherited from `BitComponentBase`)                    |
| `HtmlAttributes`      | `Dictionary<string, object>`      | `new()`                        | Additional HTML attributes for the root element. (Inherited from `BitComponentBase`)                   |
| `ReadOnly`            | `bool`                            | `false`                        | Makes the input read-only. (Inherited from `BitInputBase<TimeSpan?>`)                                 |
| `Required`            | `bool`                            | `false`                        | Marks the input as required (adds `required` attribute, visually indicates). (Inherited from `BitInputBase<TimeSpan?>`) |
| `InputHtmlAttributes` | `IReadOnlyDictionary<string, object>?` | `null`                       | Additional HTML attributes specifically for the underlying input element. (Inherited from `BitInputBase<TimeSpan?>`) |
| `DisplayName`         | `string?`                         | `null`                         | Display name for validation messages. (Inherited from `BitInputBase<TimeSpan?>`)                        |
| `Name`                | `string?`                         | `null`                         | `name` attribute for the input element. (Inherited from `BitInputBase<TimeSpan?>`)                      |
| `NoValidate`          | `bool`                            | `false`                        | Disables built-in browser validation (`novalidate`). (Inherited from `BitInputBase<TimeSpan?>`)         |
| `OnChange`            | `EventCallback<TimeSpan?>`        | ``                            | Callback for when the value changes. **Use `@bind-Value` or `ValueChanged` instead for `BitTimePicker`**. (Inherited from `BitInputBase<TimeSpan?>`) |

*Note: `BitTimePicker` inherits from `BitInputBase<TimeSpan?>` which inherits from `BitComponentBase`.*

### BitTimePickerClassStyles Properties

Used with the `Classes` and `Styles` parameters to target specific internal elements.

| Property             | Type      | Description                                                             |
| :------------------- | :-------- | :---------------------------------------------------------------------- |
| `Root`               | `string?` | Root element of the component.                                          |
| `Focused`            | `string?` | Class applied to the root when the component has focus.                 |
| `Label`              | `string?` | The label element.                                                      |
| `InputWrapper`       | `string?` | The wrapper div containing the input and icon.                          |
| `InputContainer`     | `string?` | The container div directly around the input and icon.                   |
| `Input`              | `string?` | The main text input element.                                            |
| `Icon`               | `string?` | The icon element.                                                       |
| `Overlay`            | `string?` | The overlay element shown when the callout is open (for modality).      |
| `Callout`            | `string?` | The callout (popup) main element.                                       |
| `CalloutContainer`   | `string?` | The container inside the callout holding the time inputs.               |
| `TimeInputContainer` | `string?` | The container for the hour, minute, and AM/PM inputs.                   |
| `HourInputContainer` | `string?` | The specific container for the hour input and its buttons.              |
| `IncreaseHourButton` | `string?` | The button to increase the hour.                                        |
| `IncreaseHourIcon`   | `string?` | The icon inside the increase hour button.                               |
| `HourInput`          | `string?` | The numeric input element for the hour.                                 |
| `DecreaseHourButton` | `string?` | The button to decrease the hour.                                        |
| `DecreaseHourIcon`   | `string?` | The icon inside the decrease hour button.                               |
| `HourMinuteSeparator`| `string?` | The separator element (usually ':') between hour and minute inputs.     |
| `MinuteInputContainer`| `string?` | The specific container for the minute input and its buttons.            |
| `IncreaseMinuteButton`| `string?` | The button to increase the minute.                                      |
| `IncreaseMinuteIcon` | `string?` | The icon inside the increase minute button.                             |
| `MinuteInput`        | `string?` | The numeric input element for the minute.                               |
| `DecreaseMinuteButton`| `string?` | The button to decrease the minute.                                      |
| `DecreaseMinuteIcon` | `string?` | The icon inside the decrease minute button.                             |
| `AmPmContainer`      | `string?` | The container for the AM/PM buttons (visible in 12-hour format).        |
| `AmButton`           | `string?` | The AM button.                                                          |
| `PmButton`           | `string?` | The PM button.                                                          |
| `CloseButton`        | `string?` | The close button element inside the callout (if `ShowCloseButton`=true). |
| `CloseButtonIcon`    | `string?` | The icon inside the close button.                                       |

### Public Members (Methods)

| Name                        | Return Type         | Description                                  |
| :-------------------------- | :------------------ | :------------------------------------------- |
| `FocusAsync(bool preventScroll = false)` | `ValueTask`         | Sets focus to the time picker input element. |
| **Inherited Members**       |                     |                                              |
| `RootElement`               | `ElementReference`  | Reference to the root HTML element. (From `BitComponentBase`) |
| `InputElement`              | `ElementReference`  | Reference to the underlying input element. (From `BitInputBase<TValue>`) |
| `UniqueId`                  | `Guid`              | Readonly unique identifier for the component instance. (From `BitComponentBase`) |

### Relevant Enums

**BitTimeFormat**

| Name              | Value | Description                            |
| :---------------- | :---- | :------------------------------------- |
| `TwentyFourHours` | `0`   | Use 24-hour format (00-23).            |
| `TwelveHours`     | `1`   | Use 12-hour format (1-12) with AM/PM. |

**BitIconLocation**

| Name    | Value | Description                       |
| :------ | :---- | :-------------------------------- |
| `Left`  | `0`   | Icon appears on the left side.  |
| `Right` | `1`   | Icon appears on the right side. |

**BitDropDirection**

| Name           | Value | Description                                                   |
| :------------- | :---- | :------------------------------------------------------------ |
| `All`          | `0`   | Direction determined automatically based on available space. |
| `TopAndBottom` | `1`   | Prefer opening to the top or bottom.                         |

**BitVisibility**

| Name        | Value | Description                                                          |
| :---------- | :---- | :------------------------------------------------------------------- |
| `Visible`   | `0`   | Component is visible.                                                |
| `Hidden`    | `1`   | Component is hidden (`visibility: hidden`), preserves layout space. |
| `Collapsed` | `2`   | Component is hidden (`display: none`), removes layout space.        |

**BitDir**

| Name   | Value | Description                                                        |
| :----- | :---- | :----------------------------------------------------------------- |
| `Ltr`  | `0`   | Left-to-right text direction.                                      |
| `Rtl`  | `1`   | Right-to-left text direction.                                      |
| `Auto` | `2`   | Direction determined by the browser based on content/environment. |

---
*This Markdown file was generated based on the HTML structure provided and aims to be a functional reference for AI code generation tools.*

**Explanation of the Markdown File:**

1.  **Header:** Clearly states the component (`BitTimePicker`) and the intended audience (AI Agent).
2.  **Purpose:** Explains *why* this file exists – to help the AI provide better assistance.
3.  **Overview:** Provides a concise description of the component's function, taken from the original HTML.
4.  **Usage Examples:**
    *   Uses `## Usage` for the main section and `###` for each specific example (Basic, Time Format, etc.).
    *   Includes a brief description explaining the purpose of each example.
    *   Provides fenced code blocks (```) with language identifiers (`cshtml`, `csharp`, `css`) for easy reading and parsing. Code is extracted directly from the `pre > code` tags in the HTML.
    *   Combines CSHTML and C# (`@code`) blocks where relevant for specific examples like Binding or Validation.
5.  **API Reference:**
    *   Uses `## API Reference` for the main section.
    *   Uses `###` subheadings for specific parameter sets (`BitTimePicker Parameters`), style classes (`BitTimePickerClassStyles Properties`), public members, and enums.
    *   Uses Markdown tables (`| Header | ... | \n |---|---| ... | \n | Value | ... |`) to present API information clearly. This is much better for AI parsing than trying to replicate the HTML table structure directly.
    *   Parameter names, types, and default values are often enclosed in backticks (`) for clarity as code elements.
    *   Includes inherited parameters from base classes (`BitInputBase`, `BitComponentBase`) directly within the main parameter table for convenience, clearly marking them. Alternatively, separate tables could be used, as done in the original HTML (the generated MD includes both the direct parameters and tables for base class parameters/members for completeness based on the source HTML structure).
    *   Lists relevant Enums with their members and descriptions in separate tables.
6.  **Formatting:** Uses standard Markdown for headings, code blocks, tables, bold text (`**`), and inline code (`)`).
7.  **Completeness:** Aims to capture all the distinct examples and API details present in the source HTML.
8.  **Clarity:** Descriptions are kept concise and focused on the purpose of the parameter or example.
9.  **AI Friendliness:** The structured format (headings, code blocks, tables) makes it easier for an AI to segment the information and retrieve relevant parts when asked about specific features or parameters.

This Markdown file provides a solid foundation for an AI agent to understand and suggest code related to the `BitTimePicker` component.
