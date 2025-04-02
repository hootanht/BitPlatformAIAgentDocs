# BitDateRangePicker Component Reference (`.NET Blazor - Bit Blazor UI`)

## Overview

**Component Name:** `BitDateRangePicker`

The `BitDateRangePicker` component provides a drop-down control optimized for selecting a date range (start date and end date) from a calendar view. It's useful when users need to specify a period, and contextual information like the day of the week is important. The calendar view can be customized to limit available dates or provide additional context. Optionally, it can include time pickers for selecting specific times along with the dates.

## Core Concepts & Features

*   **Date Range Selection:** Allows users to select a start date and an end date from a visual calendar interface.
*   **Time Selection (Optional):** Can include time pickers (`ShowTimePicker`) for selecting start and end times. `HourStep` and `MinuteStep` control time increments.
*   **Input Field:** Displays the selected date range and acts as the trigger for the calendar callout.
*   **Date Formatting:** Supports custom date formatting (`DateFormat`) for display and parsing. A separate `ValueFormat` controls how the selected range is displayed in the input field.
*   **Text Input (Optional):** Allows users to type the date range directly into the input field (`AllowTextInput`). Requires input matching the specified `DateFormat`.
*   **Calendar Features:**
    *   `ShowWeekNumbers`: Displays the week number for each row.
    *   `HighlightCurrentMonth` / `HighlightSelectedMonth`: Visually emphasizes months in the year picker view.
    *   Navigation: Buttons for previous/next month/year, "Go to Today".
*   **Date Range Constraints:** `MinDate` and `MaxDate` restrict the overall selectable date range. `MaxRange` limits the maximum duration between the start and end dates.
*   **Standalone Mode:** Can render the calendar UI directly without the input field (`Standalone`).
*   **Culture Support:** Adapts calendar formatting based on the provided `Culture`.
*   **Customization:**
    *   Labeling: `Label` property and `LabelTemplate`.
    *   Icon: Customizable trigger icon (`IconName`, `IconTemplate`) and location (`IconLocation`).
    *   Placeholders: `Placeholder` text for the input field.
    *   Templates: `DayCellTemplate`, `MonthCellTemplate`, `YearCellTemplate` for custom rendering within the calendar.
    *   Styling: `Style`, `Class`, and detailed `Styles`/`Classes` objects for granular control.
    *   Callout Control: Programmatic opening (`IsOpen`, `OpenCallout` method), `ShowCloseButton`, `AutoClose`.
    *   Clear Button: Option to show a button to clear the selected value (`ShowClearButton`).
*   **Data Binding:** Supports two-way binding (`@bind-Value`) to a `BitDateRangePickerValue?` object, which contains `StartDate` and `EndDate` (`DateTimeOffset?`) properties.
*   **Validation:** Integrates with Blazor's `EditForm` and validation system.
*   **States:** Supports `Enabled`, `Disabled`, and `ReadOnly` states.
*   **Responsiveness:** Optional responsive layout (`Responsive`) for small screens.
*   **RTL Support:** Supports Right-to-Left text direction (`Dir`).
*   **Time Zone:** Allows specifying a `TimeZoneInfo` object (`TimeZone`).

## Usage Examples

Below are examples demonstrating common configurations and features of the `BitDateRangePicker`.

---

### Example 1: Basic Usage

Displays various basic configurations: default, disabled, required, placeholder, showing week numbers, highlighting months, enabling the time picker, showing a clear button, custom icon, disabled auto-close, and setting an initial `StartingValue`.

```cshtml
<BitDateRangePicker Label="Basic DateRangePicker" />
<BitDateRangePicker Label="Disabled" IsEnabled="false" />
<BitDateRangePicker Label="Required" Required />
<BitDateRangePicker Label="PlaceHolder" Placeholder="Select a date range" />
<BitDateRangePicker Label="Week numbers" ShowWeekNumbers />
<BitDateRangePicker Label="Highlight months" HighlightCurrentMonth HighlightSelectedMonth />
<BitDateRangePicker Label="TimePicker" ShowTimePicker />
<BitDateRangePicker Label="Show clear button when has a value" ShowClearButton />
<BitDateRangePicker Label="Custom Icon" IconName="@BitIconName.Airplane" />
<BitDateRangePicker Label="Disabled AutoClose" AutoClose="false" />
<BitDateRangePicker Label="StartingValue: December 2020, Start Time: 10:12, End Time: 16:59" ShowTimePicker StartingValue="startingValue" />

```

```csharp
@code {
    private BitDateRangePickerValue? startingValue = new()
    {
        StartDate = new DateTimeOffset(2020, 12, 4, 10, 12, 0, DateTimeOffset.Now.Offset),
        EndDate = new DateTimeOffset(2020, 12, 4, 16, 59, 0, DateTimeOffset.Now.Offset),
    };
}
```

---

### Example 2: Min & Max Date / Range Constraints

Demonstrates restricting the selectable date range using `MinDate`, `MaxDate`, and limiting the maximum duration between start and end dates using `MaxRange`.

```cshtml
<BitDateRangePicker Label="Min: Now-5 / Max: Now+5" MinDate="DateTimeOffset.Now.AddDays(-5)" MaxDate="DateTimeOffset.Now.AddDays(5)" />
<BitDateRangePicker Label="Min: Now-2M / Max: Now+1M" MinDate="DateTimeOffset.Now.AddMonths(-2)" MaxDate="DateTimeOffset.Now.AddMonths(1)" />
<BitDateRangePicker Label="Min: Now-5Y / Max: Now+1Y" MinDate="DateTimeOffset.Now.AddYears(-5)" MaxDate="DateTimeOffset.Now.AddYears(1)" />
<BitDateRangePicker Label="MaxRange: 2d 4h 30m" MaxRange="new TimeSpan(2, 4, 30, 0)" ShowTimePicker />
```

---

### Example 3: Hour/Minute Step (Time Picker)

Shows how to control the increment/decrement steps for the hour and minute inputs when `ShowTimePicker` is enabled, using `HourStep` and `MinuteStep`.

```cshtml
<BitDateRangePicker ShowTimePicker
                    Label="HourStep = 2"
                    HourStep="2" />

<BitDateRangePicker ShowTimePicker
                    Label="MinuteStep = 15"
                    MinuteStep="15" />
```

---

### Example 4: Date Formatting

Illustrates formatting the date displayed in the input field using `DateFormat` and customizing the range display string using `ValueFormat`.

* `DateFormat`: Controls how individual dates are formatted *within* the component and for parsing text input.
* `ValueFormat`: A format string with placeholders `{0}` (start date) and `{1}` (end date) to define how the selected range appears in the input field.

```cshtml
<BitDateRangePicker Label="DateFormat: 'dd=MM(yy)'"
                    DateFormat="dd=MM(yy)" />

<BitDateRangePicker Label="ValueFormat: 'Dep: {0}, Arr: {1}'"
                    ValueFormat="Dep: {0}, Arr: {1}" />
```

---

### Example 5: Text Input Allowed

Demonstrates enabling direct text input. The user must enter dates matching the `DateFormat`. The component parses the input to determine the range.

```cshtml
<BitDateRangePicker Label="Text input allowed"
                    AllowTextInput
                    DateFormat="dd/MM/yyyy" @* Input must match this format *@
                    Placeholder="Enter a date range (dd/MM/yyyy - dd/MM/yyyy)" />
```

*Note: Parsing range text input can be complex; usually relies on a separator like '-' or requires specific formatting.*

---

### Example 6: Data Binding

Shows two-way data binding using `@bind-Value` to link the selected range to a `BitDateRangePickerValue?` object in C#.

```cshtml
<BitDateRangePicker @bind-Value="@selectedDateRange" />
<div>From: <b>@selectedDateRange?.StartDate?.ToString()</b></div>
<div>To: <b>@selectedDateRange?.EndDate?.ToString()</b></div>
```

```csharp
@code {
    private BitDateRangePickerValue? selectedDateRange = new()
    {
        StartDate = new DateTimeOffset(2020, 1, 17, 0, 0, 0, DateTimeOffset.Now.Offset),
        EndDate = new DateTimeOffset(2020, 1, 25, 0, 0, 0, DateTimeOffset.Now.Offset)
    };
}
```

---

### Example 7: Culture Customization

Demonstrates using specific `CultureInfo` instances for localization, affecting month/day names and potentially number/date formatting.

```cshtml
@using System.Globalization
@* Assumes CultureInfoHelper provides methods to get specific CultureInfo objects *@

<BitDateRangePicker Label="fa-IR culture with Farsi names"
                    GoToTodayTitle="برو به امروز"
                    ValueFormat="شروع: {0}, پایان: {1}"
                    Culture="CultureInfoHelper.GetFaIrCultureWithFarsiNames()" />

<BitDateRangePicker Label="fa-IR culture with Fingilish names"
                    GoToTodayTitle="Boro be emrouz"
                    ValueFormat="Shoro: {0}, Payan: {1}"
                    Culture="CultureInfoHelper.GetFaIrCultureWithFingilishNames()" />
```

---

### Example 8: Time Zone Specification

Shows how to specify a `TimeZoneInfo`. This affects the interpretation and display of the `DateTimeOffset` values, especially important when `ShowTimePicker` is true.

```cshtml
@using System; // For TimeZoneInfo

<BitDateRangePicker @bind-Value="@timeZoneDateRange1" ShowTimePicker Label="Default TimeZone"/>
<div>Selected date range (Local): from @(timeZoneDateRange1?.StartDate?.ToString() ?? "-") to @(timeZoneDateRange1?.EndDate?.ToString() ?? "-")</div>

<br/><br/>

@{
    TimeZoneInfo? timeZoneInfo = null;
    try { timeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("Pacific/Niue"); } catch { /* Handle case where TimeZone is not found */ }
}
@if (timeZoneInfo is not null) {
    <div>"@timeZoneInfo.Id" TimeZone:</div><br/>
    <BitDateRangePicker TimeZone="timeZoneInfo" @bind-Value="@timeZoneDateRange2" ShowTimePicker Label="Specific TimeZone"/>
    <div>Selected date range (Specific TZ): from @(timeZoneDateRange2?.StartDate?.ToString() ?? "-") to @(timeZoneDateRange2?.EndDate?.ToString() ?? "-")</div>
} else {
    <div>Could not load specific TimeZoneInfo.</div>
}
```

```csharp
@code {
    private BitDateRangePickerValue? timeZoneDateRange1 = new();
    private BitDateRangePickerValue? timeZoneDateRange2 = new();
}
```

*Note: Time zone data availability depends on the runtime environment.*

---

### Example 9: Standalone Mode

Renders the calendar UI directly without the input field using `Standalone="true"`.

```cshtml
<BitDateRangePicker Label="Basic DatePicker" Standalone />
<BitDateRangePicker Label="Disabled" IsEnabled="false" Standalone />
<BitDateRangePicker Label="Week numbers" ShowWeekNumbers Standalone />
<BitDateRangePicker Label="Highlight months" HighlightCurrentMonth HighlightSelectedMonth Standalone />
<BitDateRangePicker Label="TimePicker" ShowTimePicker Standalone />
```

---

### Example 10: ReadOnly Mode

Demonstrates the `ReadOnly` parameter. The user can view the calendar and the selected range but cannot modify it.

```cshtml
<BitDateRangePicker Label="Basic" ReadOnly @bind-Value="readOnlyDateRange" />
<BitDateRangePicker Label="Text input allowed" ReadOnly AllowTextInput @bind-Value="readOnlyDateRange" />
<BitDateRangePicker Label="Standalone" ReadOnly Standalone @bind-Value="readOnlyDateRange" />
<BitDateRangePicker Label="Standalone with TimePicker" ReadOnly ShowTimePicker Standalone @bind-Value="readOnlyDateRange" />
```

```csharp
@code {
    private BitDateRangePickerValue? readOnlyDateRange = new()
    {
        StartDate = new DateTimeOffset(2024, 12, 8, 12, 15, 0, DateTimeOffset.Now.Offset),
        EndDate = new DateTimeOffset(2024, 12, 12, 16, 45, 0, DateTimeOffset.Now.Offset),
    };
}
```

---

### Example 11: Custom Templates

Illustrates using `LabelTemplate`, `DayCellTemplate`, `MonthCellTemplate`, and `YearCellTemplate` for customized rendering.

```cshtml
<style>
    /* Example CSS for templates */
    .day-cell { /* Styles for day cell container */ }
    .weekend-cell { /* Style for weekend days */ }
    .badge { /* Style for badge on specific days */ }
    .year-suffix { /* Style for 'AC' suffix on year */ }
</style>

<BitDateRangePicker>
    <LabelTemplate>
        Custom label <BitIcon IconName="@BitIconName.Calendar" />
    </LabelTemplate>
</BitDateRangePicker>

<BitDateRangePicker Label="DayCellTemplate">
    <DayCellTemplate>
        <span class="day-cell@(context.DayOfWeek == DayOfWeek.Sunday ? " weekend-cell" : null)">
            @context.Day
            @if (context.Day % 5 is 0) { <span class="badge"></span> }
        </span>
    </DayCellTemplate>
</BitDateRangePicker>

<BitDateRangePicker Label="MonthCellTemplate">
    <MonthCellTemplate>
        <div style="width:28px; padding:3px; color:black; background:@(context.Month == 1 ? "lightcoral" : "yellowgreen")">
            @CultureInfo.CurrentUICulture.DateTimeFormat.GetAbbreviatedMonthName(context.Month)
        </div>
    </MonthCellTemplate>
</BitDateRangePicker>

<BitDateRangePicker Label="YearCellTemplate">
    <YearCellTemplate>
        <span style="position: relative">
            @context @* context is the year integer *@
            <span class="year-suffix">AC</span>
        </span>
    </YearCellTemplate>
</BitDateRangePicker>
```

---

### Example 12: Responsive Mode

Enables responsive layout adjustments for the calendar callout.

```cshtml
<BitDateRangePicker Label="Response DateRangePicker"
                    Responsive
                    ShowWeekNumbers
                    Placeholder="Select a date range" />
```

---

### Example 13: Validation

Integrates `BitDateRangePicker` within an `EditForm`. The `[Required]` attribute (or custom validation) would typically apply to the `BitDateRangePickerValue` object or its `StartDate`/`EndDate` properties in the model.

```cshtml
<style>
    .validation-message { color: red; }
</style>

<EditForm Model="validationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
    <DataAnnotationsValidator />

    <BitDateRangePicker @bind-Value="validationModel.DateRange" Label="Date Range Required"/>
    @* ValidationMessage might need custom logic or apply to StartDate/EndDate individually *@
    <ValidationMessage For="@(() => validationModel.DateRange)" />
    <ValidationMessage For="@(() => validationModel.DateRange.StartDate)" />
    <ValidationMessage For="@(() => validationModel.DateRange.EndDate)" />

    <br/>
    <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
    @* ... Reset button ... *@
</EditForm>
```

```csharp
@using System.ComponentModel.DataAnnotations

@code {
    public class BitDateRangePickerValidationModel
    {
        [Required(ErrorMessage = "Date range is required.")]
        [DateRangeRequired(ErrorMessage = "Both start and end dates are required.")] // Example custom validator
        public BitDateRangePickerValue? DateRange { get; set; } = new(); // Initialize to avoid null ref on bind
    }

    // Example custom validator (implementation not shown)
    public class DateRangeRequiredAttribute : ValidationAttribute { /* ... */ }

    private BitDateRangePickerValidationModel validationModel = new();
    private string SuccessMessage = string.Empty;

    private void HandleValidSubmit() { SuccessMessage = "Form Submitted!"; /* ... */ }
    private void HandleInvalidSubmit() { SuccessMessage = string.Empty; /* ... */ }
}
```

*Note: Validating the `BitDateRangePickerValue` object itself or its nullable `StartDate`/`EndDate` properties might require custom validation attributes or logic, as `[Required]` might not behave as expected on the complex object directly.*

---

### Example 14: Style & Class Customization (Detailed)

Demonstrates applying custom styles/classes using `Style`, `Class`, `Styles`, and `Classes` for detailed visual control.

*(Refer to the CSS in the original HTML and the `BitDateRangePickerClassStyles` section below for targeting specific elements)*

```cshtml
<style>
    /* Example CSS (refer to original HTML for full set) */
    .custom-class { /* Root style via Class */ }
    .custom-root { /* Root style via Classes */ }
    .custom-input-container { /* Input container via Classes */ }
    .custom-day-picker { /* Day picker wrapper style */ }
    .custom-start-end { /* Style for start/end selection days */ }
    .custom-selected-days { /* Style for days within the range */ }
    /* ... etc ... */
</style>

@* Component's Style & Class: *@
<BitDateRangePicker Style="margin: 1rem; box-shadow: dodgerblue 0 0 1rem;" />
<BitDateRangePicker Class="custom-class" />

@* Styles object for inline styles on internal parts: *@
<BitDateRangePicker ShowTimePicker
                    Styles="@(new() { /* ... styles mapping to BitDateRangePickerClassStyles properties ... */ })" />

@* Classes object for applying CSS classes to internal parts: *@
<BitDateRangePicker @bind-Value="@classesValue" Label="Classes Demo"
                    Classes="@(new() { Root = "custom-root",
                                       InputContainer = "custom-input-container",
                                       DayPickerWrapper = "custom-day-picker",
                                       StartAndEndSelectionDays = "custom-start-end",
                                       SelectedDayButtons = "custom-selected-days",
                                       /* ... other class mappings ... */ })" />
```

```csharp
@code {
    private BitDateRangePickerValue? classesValue;
}
```

---

### Example 15: RTL (Right-to-Left) Support

Shows the `BitDateRangePicker` rendered in RTL mode using `Dir="BitDir.Rtl"`.

```cshtml
<div dir="rtl"> @* Container div sets overall direction *@
    <BitDateRangePicker Dir="BitDir.Rtl" Label="انتخابگر محدوده تاریخ" />
</div>
```

---

## API Reference

### `BitDateRangePicker` Parameters

| Name                       | Type                                  | Default Value                     | Description                                                                                                      |
| :------------------------- | :------------------------------------ | :-------------------------------- | :--------------------------------------------------------------------------------------------------------------- |
| `AllowTextInput`           | `bool`                                | `false`                         | Whether text input is allowed. Parsing depends on `DateFormat`.                                                  |
| `AutoClose`                | `bool`                                | `true`                          | Whether the callout closes automatically after selecting the end date.                                          |
| `CalloutAriaLabel`         | `string`                              | `"Calendar"`                    | Aria-label for the callout popup.                                                                               |
| `CalloutHtmlAttributes`    | `Dictionary<string, object>`          | `new Dictionary...`             | Additional HTML attributes for the callout element.                                                              |
| `Classes`                  | `BitDateRangePickerClassStyles?`      | `null`                          | Custom CSS classes for internal parts. See `BitDateRangePickerClassStyles` below.                              |
| `CloseButtonTitle`         | `string`                              | `"Close date range picker"`     | Tooltip for the close button (if shown).                                                                        |
| `Culture`                  | `CultureInfo`                         | `CultureInfo.CurrentUICulture`  | CultureInfo for formatting and localization.                                                                   |
| `DateFormat`               | `string?`                             | `null`                          | Format for displaying/parsing dates. Defaults to culture's short date.                                            |
| `DayCellTemplate`          | `RenderFragment<DateTimeOffset>?`     | `null`                          | Custom template for rendering day cells. `context` is the date.                                                 |
| `GoToNextMonthTitle`       | `string`                              | `"Go to next month"`            | Tooltip for the next month button.                                                                              |
| `GoToNextYearRangeTitle`   | `string`                              | `"Next year range {0} - {1}"`   | Tooltip for the next year range button.                                                                          |
| `GoToNextYearTitle`        | `string`                              | `"Go to next year {0}"`         | Tooltip for the next year button.                                                                               |
| `GoToPrevMonthTitle`       | `string`                              | `"Go to previous month"`        | Tooltip for the previous month button.                                                                          |
| `GoToPrevYearRangeTitle`   | `string`                              | `"Previous year range {0} - {1}"`| Tooltip for the previous year range button.                                                                    |
| `GoToPrevYearTitle`        | `string`                              | `"Go to previous year {0}"`     | Tooltip for the previous year button.                                                                           |
| `GoToTodayTitle`           | `string`                              | `"Go to today"`                 | Tooltip for the "Go to Today" button.                                                                           |
| `HasBorder`                | `bool`                                | `true`                          | Whether the input wrapper has a border. *Note: Default is true, differing from API table in HTML.*                |
| `HighlightCurrentMonth`    | `bool`                                | `false`                         | Whether to highlight the current month in the month picker view.                                                  |
| `HighlightSelectedMonth`   | `bool`                                | `false`                         | Whether to highlight the selected month(s) in the month picker view.                                             |
| `HideTimePickerTitle`      | `string`                              | `"Hide time picker"`            | Tooltip for the button toggling the time picker visibility (if shown).                                           |
| `HourStep`                 | `int`                                 | `1`                             | Step for hour input increments/decrements.                                                                       |
| `IconLocation`             | `BitIconLocation`                     | `Right`                         | Position of the calendar icon. See enum below.                                                                 |
| `IconName`                 | `string`                              | `"CalendarMirrored"`            | Name of the trigger icon.                                                                                      |
| `IconTemplate`             | `RenderFragment?`                     | `null`                          | Custom template for the trigger icon.                                                                            |
| `InvalidErrorMessage`      | `string?`                             | `null`                          | Custom error message for invalid text input.                                                                     |
| `IsMonthPickerVisible`     | `bool`                                | `true`                          | Whether the month picker (year view) is shown initially. *Note: Seems internal/behavioral.*                    |
| `IsOpen`                   | `bool`                                | `false`                         | Controls the visibility of the callout. Use with `@bind-IsOpen`.                                                |
| `Label`                    | `string?`                             | `null`                          | Text label for the component.                                                                                  |
| `LabelTemplate`            | `RenderFragment?`                     | `null`                          | Custom template for the label.                                                                                 |
| `MaxRange`                 | `TimeSpan?`                           | `null`                          | Maximum allowed duration between the start and end dates.                                                      |
| `MaxDate`                  | `DateTimeOffset?`                     | `null`                          | Maximum selectable date.                                                                                       |
| `MinDate`                  | `DateTimeOffset?`                     | `null`                          | Minimum selectable date.                                                                                       |
| `MinuteStep`               | `int`                                 | `1`                             | Step for minute input increments/decrements.                                                                     |
| `MonthCellTemplate`        | `RenderFragment<DateTimeOffset>?`     | `null`                          | Custom template for rendering month cells. `context` is a date within the month.                              |
| `MonthPickerToggleTitle`   | `string`                              | `"{0}, change month"`           | Tooltip for the month/year header button. `{0}` is month/year.                                                |
| `OnClick`                  | `EventCallback`                       |                                 | Callback for clicks on the input wrapper.                                                                      |
| `OnFocus`                  | `EventCallback`                       |                                 | Callback for when the input gains focus (bubbles).                                                            |
| `OnFocusIn`                | `EventCallback`                       |                                 | Callback for when the input gains focus (no bubble).                                                          |
| `OnFocusOut`               | `EventCallback`                       |                                 | Callback for when the input loses focus.                                                                      |
| `OnSelectDate`             | `EventCallback<BitDateRangePickerValue?>`|                              | Callback invoked when the date range value changes. *Note: Use `@bind-Value` or `ValueChanged` typically.*      |
| `Placeholder`              | `string`                              | `string.Empty`                  | Placeholder text for the input field.                                                                          |
| `Responsive`               | `bool`                                | `false`                         | Enables responsive layout for small screens.                                                                  |
| `SelectedDateAriaAtomic`   | `string`                              | `"Selected date {0}"`           | Format string for `aria-live` announcement of selected date(s). `{0}` is replaced by the formatted date/range. |
| `ShowClearButton`          | `bool`                                | `false`                         | If `true`, shows a clear ('X') button in the input field when a value is selected.                             |
| `ShowCloseButton`          | `bool`                                | `false`                         | If `true`, shows a close button in the callout header.                                                          |
| `ShowGoToToday`            | `bool`                                | `true`                          | Whether the "Go to Today" button is visible.                                                                  |
| `ShowMonthPickerAsOverlay` | `bool`                                | `false`                         | If `true`, the month/year picker appears as an overlay.                                                        |
| `ShowTimePicker`           | `bool`                                | `false`                         | If `true`, includes the time picker UI for start and end times.                                                |
| `ShowTimePickerAsOverlay`  | `bool`                                | `false`                         | *Likely a typo in API doc, might be same as `ShowMonthPickerAsOverlay` or non-functional.*                   |
| `ShowTimePickerTitle`      | `string`                              | `"Show time picker"`            | Tooltip for the button toggling time picker visibility (if applicable).                                         |
| `ShowWeekNumbers`          | `bool`                                | `false`                         | If `true`, displays week numbers in the calendar grid.                                                        |
| `Standalone`               | `bool`                                | `false`                         | If `true`, renders only the calendar UI without the input/callout.                                            |
| `StartingValue`            | `BitDateRangePickerValue?`            | `null`                          | The initial date range displayed when the picker opens if `Value` is not set.                                    |
| `Styles`                   | `BitDateRangePickerClassStyles?`      | `null`                          | Custom inline CSS styles for internal parts. See `BitDateRangePickerClassStyles` below.                        |
| `TabIndex`                 | `int`                                 | `0`                             | `tabindex` for the input field.                                                                               |
| `TimeFormat`               | `BitTimeFormat`                       | `TwentyFourHours`               | Format (12/24h) for the time picker UI. See enum below.                                                       |
| `TimeZone`                 | `TimeZoneInfo?`                       | `null`                          | TimeZone used for interpreting dates/times. Defaults to local.                                                |
| `Underlined`               | `bool`                                | `false`                         | If `true`, applies an underlined style to the input field.                                                   |
| `ValueFormat`              | `string`                              | `"Start: {0} - End: {1}"`       | Format string for displaying the selected range in the input. `{0}`=StartDate, `{1}`=EndDate.                 |
| `WeekNumberTitle`          | `string`                              | `"Week number {0}"`             | Tooltip format for week numbers. `{0}` is the week number.                                                     |
| `YearCellTemplate`         | `RenderFragment<int>?`                | `null`                          | Custom template for rendering year cells. `context` is the year integer.                                     |
| `YearPickerToggleTitle`    | `string`                              | `"{0}, change year"`            | Tooltip for the year header button. `{0}` is the year.                                                       |
| `YearRangePickerToggleTitle`| `string`                              | `"{0} - {1}, change month"`     | Tooltip for the year range header button. `{0}`/`{1}` are start/end years.                                  |
| **Inherited Parameters**   |                                       |                                 | *Includes parameters from `BitInputBase<BitDateRangePickerValue?>` and `BitComponentBase`.*                     |

---

*Inherited `BitInputBase<BitDateRangePickerValue?>` and `BitComponentBase` parameters and public members are similar to those listed in previous components, adapted for the `BitDateRangePickerValue` type.*

---

### `BitDateRangePickerValue` Class (Value Type)

Represents the selected date range.

| Property  | Type             | Description                               |
| :-------- | :--------------- | :---------------------------------------- |
| `StartDate` | `DateTimeOffset?`| The selected start date and time (nullable). |
| `EndDate` | `DateTimeOffset?`| The selected end date and time (nullable).   |

---

### `BitDateRangePickerClassStyles` Properties (Used by `Classes` and `Styles` parameters)

Defines CSS classes or styles for specific internal parts of the `BitDateRangePicker`. *This inherits many properties from `BitDatePickerClassStyles` and adds range-specific ones.*

| Property                     | Type      | Description                                                                        | Inherited From `DatePicker`? |
| :--------------------------- | :-------- | :--------------------------------------------------------------------------------- | :----------------------- |
| `Root`                       | `string?` | Root element.                                                                      | Yes                      |
| `Focused`                    | `string?` | Root element when focused.                                                          | Yes                      |
| `Label`                      | `string?` | Label element.                                                                     | Yes                      |
| `InputWrapper`               | `string?` | Input wrapper `div`.                                                               | Yes                      |
| `InputContainer`             | `string?` | Input & icon container `div`.                                                      | Yes                      |
| `Input`                      | `string?` | Input element.                                                                     | Yes                      |
| `Icon`                       | `string?` | Calendar icon element.                                                             | Yes                      |
| `Overlay`                    | `string?` | Callout overlay `div`.                                                             | Yes                      |
| `Callout`                    | `string?` | Callout main `div`.                                                                | Yes                      |
| `CalloutContainer`           | `string?` | Callout inner container `div`.                                                     | Yes                      |
| `Group`                      | `string?` | Main group `div` inside callout.                                                   | Yes                      |
| `DayPickerWrapper`           | `string?` | Day picker grid wrapper `div`.                                                     | Yes                      |
| `DayPickerHeader`            | `string?` | Day picker header `div`.                                                           | Yes                      |
| `DayPickerMonth`             | `string?` | Month/year display element.                                                        | Yes                      |
| `DayPickerNavWrapper`        | `string?` | Month/year navigation buttons wrapper `div`.                                       | Yes                      |
| `PrevMonthNavButton`         | `string?` | Previous month button.                                                             | Yes                      |
| `PrevMonthNavIcon`           | `string?` | Previous month icon.                                                               | Yes                      |
| `GoToTodayButton`            | `string?` | "Go to Today" button.                                                              | Yes                      |
| `GoToTodayIcon`              | `string?` | "Go to Today" icon.                                                                | Yes                      |
| `CloseButton`                | `string?` | Callout close button (if shown).                                                   | Yes                      |
| `CloseButtonIcon`            | `string?` | Close button icon.                                                                 | Yes                      |
| `NextMonthNavButton`         | `string?` | Next month button.                                                                 | Yes                      |
| `NextMonthNavIcon`           | `string?` | Next month icon.                                                                   | Yes                      |
| `DaysHeaderRow`              | `string?` | Day names header row `div`.                                                        | Yes                      |
| `WeekNumbersHeader`          | `string?` | Week number header cell (if shown).                                                | Yes                      |
| `DaysRow`                    | `string?` | Each week row `div`.                                                               | Yes                      |
| `WeekNumber`                 | `string?` | Week number cell `div` (if shown).                                                 | Yes                      |
| `DayButton`                  | `string?` | Individual day button.                                                             | Yes                      |
| `TodayDayButton`             | `string?` | Today's day button.                                                                | Yes                      |
| `StartDayButton`             | `string?` | Selected start day button.                                                         | **No**                   |
| `SelectedDayButtons`         | `string?` | Buttons for days *within* the selected range (excluding start/end).               | **No**                   |
| `EndDayButton`               | `string?` | Selected end day button.                                                           | **No**                   |
| `StartAndEndSelectionDays`   | `string?` | Buttons for *both* start and end days (if different styles are needed than range). | **No**                   |
| `TimePickerContainer`        | `string?` | Time picker main container `div`.                                                  | Yes                      |
| `StartTimePickerWrapper`     | `string?` | Start time picker inputs/buttons wrapper.                                          | **No**                   |
| `EndTimePickerWrapper`       | `string?` | End time picker inputs/buttons wrapper.                                            | **No**                   |
| `TimePickerWrapper`          | `string?` | General wrapper for time inputs (used by both start/end).                           | Yes                      |
| `TimePickerHourInput`        | `string?` | Hour input element.                                                                | Yes                      |
| `TimePickerMinuteInput`      | `string?` | Minute input element.                                                              | Yes                      |
| `TimePickerDivider`          | `string?` | Divider (`:`) between hour/minute.                                                 | Yes                      |
| `StartTimeIncreaseHourButton`| `string?` | Start time - increase hour button.                                                 | **No**                   |
| `StartTimeDecreaseHourButton`| `string?` | Start time - decrease hour button.                                                 | **No**                   |
| `StartTimeIncreaseMinuteButton`|`string?`| Start time - increase minute button.                                               | **No**                   |
| `StartTimeDecreaseMinuteButton`|`string?`| Start time - decrease minute button.                                               | **No**                   |
| `EndTimeIncreaseHourButton`  | `string?` | End time - increase hour button.                                                   | **No**                   |
| `EndTimeDecreaseHourButton`  | `string?` | End time - decrease hour button.                                                   | **No**                   |
| `EndTimeIncreaseMinuteButton`| `string?` | End time - increase minute button.                                                 | **No**                   |
| `EndTimeDecreaseMinuteButton`| `string?` | End time - decrease minute button.                                                 | **No**                   |
| `StartTimePickerAmPmContainer`| `string?`| Start time AM/PM container.                                                        | **No**                   |
| `EndTimePickerAmPmContainer` | `string?` | End time AM/PM container.                                                          | **No**                   |
| `TimePickerAmPmContainer`    | `string?` | General AM/PM container style.                                                     | Yes                      |
| `TimePickerAmButton`         | `string?` | AM button style.                                                                   | Yes                      |
| `TimePickerPmButton`         | `string?` | PM button style.                                                                   | Yes                      |
| `Divider`                    | `string?` | Main divider between day picker and month/year picker.                           | Yes                      |
| `YearMonthPickerWrapper`     | `string?` | Month/year picker wrapper `div`.                                                   | Yes                      |
| `MonthPickerHeader`          | `string?` | Month picker header `div`.                                                         | Yes                      |
| `YearPickerToggleButton`     | `string?` | Year picker toggle button (in month view).                                         | Yes                      |
| `MonthPickerNavWrapper`      | `string?` | Month picker navigation wrapper `div`.                                             | Yes                      |
| `PrevYearNavButton`          | `string?` | Previous year button (in month view).                                              | Yes                      |
| `PrevYearNavIcon`            | `string?` | Previous year icon.                                                                | Yes                      |
| `NextYearNavButton`          | `string?` | Next year button (in month view).                                                  | Yes                      |
| `NextYearNavIcon`            | `string?` | Next year icon.                                                                    | Yes                      |
| `MonthsContainer`            | `string?` | Month buttons container `div`.                                                     | Yes                      |
| `MonthsRow`                  | `string?` | Each row `div` of month buttons.                                                   | Yes                      |
| `MonthButton`                | `string?` | Individual month button.                                                           | Yes                      |
| `SelectedMonthButton`        | `string?` | Style for selected month button(s).                                                | Yes                      |
| `CurrentMonthButton`         | `string?` | Style for current month button (if highlighted).                                   | Yes                      |
| `YearPickerHeader`           | `string?` | Year picker header `div`.                                                          | Yes                      |
| `MonthPickerToggleButton`    | `string?` | Month picker toggle button (in year view).                                         | Yes                      |
| `YearPickerNavWrapper`       | `string?` | Year picker navigation wrapper `div`.                                              | Yes                      |
| `PrevYearRangeNavButton`     | `string?` | Previous year range button.                                                        | Yes                      |
| `PrevYearRangeNavIcon`       | `string?` | Previous year range icon.                                                          | Yes                      |
| `NextYearRangeNavButton`     | `string?` | Next year range button.                                                            | Yes                      |
| `NextYearRangeNavIcon`       | `string?` | Next year range icon.                                                              | Yes                      |
| `YearsContainer`             | `string?` | Year buttons container `div`.                                                      | Yes                      |
| `YearsRow`                   | `string?` | Each row `div` of year buttons.                                                    | Yes                      |
| `YearButton`                 | `string?` | Individual year button.                                                            | Yes                      |
| `SelectedYearButton`         | `string?` | Style for selected year button.                                                    | Yes                      |
| `CurrentYearButton`          | `string?` | Style for current year button (if highlighted).                                    | Yes                      |

---

*Related Enums (`BitTimeFormat`, `BitIconLocation`, `BitVisibility`, `BitDir`) are the same as those defined in the `BitDatePicker` and `BitCircularTimePicker` references.*

---

## Key Considerations & Best Practices

* **Value Type:** Binds to `BitDateRangePickerValue?`, which contains nullable `StartDate` and `EndDate` of type `DateTimeOffset?`. Handle potential nulls when accessing these properties.
* **Date Range Logic:** The component handles selecting the start date first, then the end date. Highlighting between selected dates is done automatically.
* **MaxRange:** Use `MaxRange` to enforce limitations on the duration between start and end dates (e.g., maximum 7-day booking).
* **Time Picker Integration:** When `ShowTimePicker` is true, users can set both start and end times. `HourStep` and `MinuteStep` apply to both time pickers.
* **Formatting:** `DateFormat` applies to individual date parsing/display within the calendar. `ValueFormat` specifically controls how the selected *range* (start and end dates) is displayed in the main input field.
* **Validation:** Validate the `BitDateRangePickerValue` object or its `StartDate`/`EndDate` properties in your model, possibly using custom validation attributes to ensure both dates are present or that the end date is after the start date.
* **Standalone Mode:** Useful for embedding the calendar range selection directly into a larger UI without the input field trigger.
* **Culture & TimeZone:** Crucial for correct localization and date/time interpretation. Test thoroughly based on expected user locales and time zones.
* **Accessibility:** Ensure clear labeling (`Label` or `LabelTemplate`). The component provides ARIA roles for the calendar grid and buttons.


