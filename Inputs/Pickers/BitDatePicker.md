# BitDatePicker Component Reference (`.NET Blazor - Bit Blazor UI`)

## Overview

**Component Name:** `BitDatePicker`

The `BitDatePicker` component provides a drop-down control optimized for selecting a single date from a calendar view. It can display contextual information like the day of the week and supports features like week numbers and highlighting. The calendar view can be modified to limit available dates or provide additional context. Optionally, it can include a time picker for selecting both date and time.

## Core Concepts & Features

*   **Date Selection:** Allows users to pick a single date (day, month, year) from a visual calendar interface.
*   **Time Selection (Optional):** Can include a time picker (`ShowTimePicker`) to select hours and minutes alongside the date. `HourStep` and `MinuteStep` control time increments.
*   **Input Field:** Displays the selected date (and time, if enabled) and acts as the trigger for the calendar callout.
*   **Date Formatting:** Supports custom date formatting (`DateFormat`) for display and parsing.
*   **Text Input (Optional):** Allows users to type the date directly into the input field (`AllowTextInput`). Requires input matching the specified `DateFormat`.
*   **Calendar Features:**
    *   `ShowWeekNumbers`: Displays the week number for each row.
    *   `HighlightCurrentMonth` / `HighlightSelectedMonth`: Visually emphasizes the current or selected month in the year picker view.
    *   Navigation: Buttons for previous/next month/year, "Go to Today".
*   **Date Range Constraints:** `MinDate` and `MaxDate` parameters restrict the selectable date range.
*   **Standalone Mode:** Can render the calendar/time picker UI directly without the input field (`Standalone`).
*   **Culture Support:** Adapts calendar formatting (day names, month names, first day of week) based on the provided `Culture`.
*   **Customization:**
    *   Labeling: `Label` property and `LabelTemplate`.
    *   Icon: Customizable trigger icon (`IconName`, `IconTemplate`) and location (`IconLocation`).
    *   Placeholders: `Placeholder` text for the input field.
    *   Templates: `DayCellTemplate`, `MonthCellTemplate`, `YearCellTemplate` for custom rendering within the calendar.
    *   Styling: `Style`, `Class`, and detailed `Styles`/`Classes` objects for granular control over internal elements.
    *   Callout Control: Programmatic opening (`IsOpen`, `OpenCallout` method), `ShowCloseButton`, `AutoClose`.
    *   Clear Button: Option to show a button to clear the selected value (`ShowClearButton`).
*   **Data Binding:** Supports two-way binding (`@bind-Value`) to a `DateTimeOffset?` variable.
*   **Validation:** Integrates with Blazor's `EditForm` and validation system (`DataAnnotationsValidator`, `ValidationMessage`, `InvalidErrorMessage`).
*   **States:** Supports `Enabled`, `Disabled`, and `ReadOnly` states.
*   **Responsiveness:** Optional responsive layout (`Responsive`) for better display on small screens.
*   **RTL Support:** Supports Right-to-Left text direction (`Dir`).
*   **Time Zone:** Allows specifying a `TimeZoneInfo` object to interpret the selected date/time (`TimeZone`).

## Usage Examples

Below are examples demonstrating common configurations and features of the `BitDatePicker`.

---

### Example 1: Basic Usage

Displays various basic configurations: default, disabled, required, placeholder, showing week numbers, highlighting months, enabling the time picker, showing a clear button, and setting an initial `StartingValue`.

```cshtml
<BitDatePicker Label="Basic DatePicker" />
<BitDatePicker Label="Disabled" IsEnabled="false" />
<BitDatePicker Label="Required" Required />
<BitDatePicker Label="PlaceHolder" Placeholder="Select a date" />
<BitDatePicker Label="Week numbers" ShowWeekNumbers />
<BitDatePicker Label="Highlight months" HighlightCurrentMonth HighlightSelectedMonth />
<BitDatePicker Label="TimePicker" ShowTimePicker />
<BitDatePicker Label="Show clear button when has a value" ShowClearButton />
<BitDatePicker Label="StartingValue: December 2020, 20:45" ShowTimePicker StartingValue="startingValue" />
```

```csharp
@code {
    private DateTimeOffset? startingValue = new DateTimeOffset(2020, 12, 4, 20, 45, 0, DateTimeOffset.Now.Offset);
}
```

---

### Example 2: Min & Max Dates

Demonstrates restricting the selectable date range using `MinDate` and `MaxDate`. Dates outside this range will be disabled in the calendar view.

```cshtml
<BitDatePicker Label="Min: Now-5 / Max: Now+5" MinDate="DateTimeOffset.Now.AddDays(-5)" MaxDate="DateTimeOffset.Now.AddDays(5)" />
<BitDatePicker Label="Min: Now-2M / Max: Now+1M" MinDate="DateTimeOffset.Now.AddMonths(-2)" MaxDate="DateTimeOffset.Now.AddMonths(1)" />
<BitDatePicker Label="Min: Now-5Y / Max: Now+1Y" MinDate="DateTimeOffset.Now.AddYears(-5)" MaxDate="DateTimeOffset.Now.AddYears(1)" />
```

---

### Example 3: Hour/Minute Step (Time Picker)

Shows how to control the increment/decrement steps for the hour and minute inputs when `ShowTimePicker` is enabled.

```cshtml
<BitDatePicker ShowTimePicker
               Label="HourStep = 2"
               HourStep="2" />

<BitDatePicker ShowTimePicker
               Label="MinuteStep = 15"
               MinuteStep="15" />
```

---

### Example 4: Custom Date Format

Illustrates formatting the date displayed in the input field using the `DateFormat` property with a custom format string.

```cshtml
<BitDatePicker Label="Formatted Date"
               DateFormat="dd=MM(yy)" @* Example: 02=04(25) *@
               Placeholder="Select a date" />
```

---

### Example 5: Text Input Allowed

Demonstrates enabling direct text input into the field using `AllowTextInput="true"`. The user must enter the date in the exact format specified by `DateFormat`.

```cshtml
<BitDatePicker Label="Text input allowed"
               AllowTextInput
               DateFormat="dd/MM/yyyy" @* Input must match this format *@
               Placeholder="Enter a date (dd/MM/yyyy)" />
```

*Note: Clicking the input opens the picker. Clicking again while open closes the picker and allows text editing.*

---

### Example 6: Data Binding

Shows two-way data binding using `@bind-Value` to link the selected date/time to a `DateTimeOffset?` variable.

```cshtml
<BitDatePicker @bind-Value="@selectedDate" />
<div>Selected date: @selectedDate?.ToString()</div>
```

```csharp
@code {
    private DateTimeOffset? selectedDate = new DateTimeOffset(2020, 1, 17, 0, 0, 0, DateTimeOffset.Now.Offset); // Example initial value
}
```

---

### Example 7: Culture Customization

Demonstrates using specific `CultureInfo` instances to change the language and formatting of the calendar (e.g., month names, day names, first day of week).

```cshtml
@using System.Globalization
@* Assumes CultureInfoHelper provides methods to get specific CultureInfo objects *@

<BitDatePicker Label="fa-IR culture with Farsi names"
               GoToTodayTitle="برو به امروز"
               Culture="CultureInfoHelper.GetFaIrCultureWithFarsiNames()" />

<BitDatePicker Label="fa-IR culture with Fingilish names"
               GoToTodayTitle="Boro be emrouz"
               Culture="CultureInfoHelper.GetFaIrCultureWithFingilishNames()" />
```

---

### Example 8: Time Zone Specification

Shows how to specify a `TimeZoneInfo` for the DatePicker. This affects how the `DateTimeOffset` value is interpreted and potentially displayed, especially when `ShowTimePicker` is enabled.

```cshtml
@using System; // For TimeZoneInfo

<BitDatePicker @bind-Value="@timeZoneDate1" ShowTimePicker Label="Default TimeZone" />
<div>Selected date (Local): @timeZoneDate1?.ToString()</div>

<br/><br/>

@{
    TimeZoneInfo? timeZoneInfo = null;
    try { timeZoneInfo = TimeZoneInfo.FindSystemTimeZoneById("Pacific/Niue"); } catch { /* Handle case where TimeZone is not found */ }
}
@if (timeZoneInfo is not null) {
    <div>"@timeZoneInfo.Id" TimeZone:</div><br/>
    <BitDatePicker TimeZone="timeZoneInfo" @bind-Value="@timeZoneDate2" ShowTimePicker Label="Specific TimeZone"/>
    <div>Selected date (Specific TZ): @timeZoneDate2?.ToString()</div>
} else {
    <div>Could not load specific TimeZoneInfo.</div>
}
```

```csharp
@code {
    private DateTimeOffset? timeZoneDate1;
    private DateTimeOffset? timeZoneDate2;
}
```

*Note: Time zone data availability can vary depending on the runtime environment (OS, project settings).*

---

### Example 9: Standalone Mode

Renders the calendar UI directly without the input field using `Standalone="true"`. Useful for embedding the calendar within other components.

```cshtml
<BitDatePicker Label="Basic DatePicker" Standalone />
<BitDatePicker Label="Disabled" IsEnabled="false" Standalone />
<BitDatePicker Label="Week numbers" ShowWeekNumbers Standalone />
<BitDatePicker Label="Highlight months" HighlightCurrentMonth HighlightSelectedMonth Standalone />
<BitDatePicker Label="TimePicker" ShowTimePicker Standalone />
```

---

### Example 10: ReadOnly Mode

Demonstrates the `ReadOnly` parameter. The user can view the calendar and the selected date but cannot change the value via the UI or text input.

```cshtml
<BitDatePicker Label="Basic" ReadOnly @bind-Value="readOnlyDate" />
<BitDatePicker Label="Text input allowed" ReadOnly AllowTextInput @bind-Value="readOnlyDate" />
<BitDatePicker Label="Standalone" ReadOnly Standalone @bind-Value="readOnlyDate" />
<BitDatePicker Label="Standalone with TimePicker" ReadOnly ShowTimePicker Standalone @bind-Value="readOnlyDate" />
```

```csharp
@code {
    private DateTimeOffset? readOnlyDate = DateTimeOffset.Now;
}
```

---

### Example 11: Custom Templates

Shows how to use `LabelTemplate`, `DayCellTemplate`, `MonthCellTemplate`, and `YearCellTemplate` to customize the rendering of different parts of the DatePicker UI.

```cshtml
<style>
    /* Example CSS for templates */
    .day-cell { width: 28px; height: 28px; position: relative; display: inline-block; line-height: 28px; }
    .weekend-cell { color: red; }
    .badge { /* Style for the red dot */ }
    .year-suffix { /* Style for the 'AC' suffix */ }
</style>

<BitDatePicker>
    <LabelTemplate>
        Custom label <BitIcon IconName="@BitIconName.Calendar" />
    </LabelTemplate>
</BitDatePicker>

<BitDatePicker Label="DayCellTemplate">
    <DayCellTemplate>
        <span class="day-cell@(context.DayOfWeek == DayOfWeek.Sunday ? " weekend-cell" : null)">
            @context.Day
            @if (context.Day % 5 is 0)
            {
                <span class="badge"></span> @* Example: Add a badge every 5 days *@
            }
        </span>
    </DayCellTemplate>
</BitDatePicker>

<BitDatePicker Label="MonthCellTemplate">
    <MonthCellTemplate>
        <div style="width:28px; padding:3px; color:black; background:@(context.Month == 1 ? "lightcoral" : "yellowgreen")">
            @CultureInfo.CurrentUICulture.DateTimeFormat.GetAbbreviatedMonthName(context.Month)
        </div>
    </MonthCellTemplate>
</BitDatePicker>

<BitDatePicker Label="YearCellTemplate">
    <YearCellTemplate>
        <span style="position: relative">
            @context @* context is the year integer *@
            <span class="year-suffix">AC</span>
        </span>
    </YearCellTemplate>
</BitDatePicker>
```

---

### Example 12: Responsive Mode

Enables responsive behavior for the calendar callout using the `Responsive` property.

```cshtml
<BitDatePicker Label="Response DatePicker"
               Responsive
               ShowWeekNumbers
               Placeholder="Select a date" />
```

---

### Example 13: Validation

Integrates `BitDatePicker` within an `EditForm` using `DataAnnotationsValidator`. The `[Required]` attribute on the model ensures a date must be selected.

```cshtml
<style>
    .validation-message { color: red; }
</style>

<EditForm Model="validationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
    <DataAnnotationsValidator />

    <BitDatePicker @bind-Value="validationModel.Date" Label="Date Required" />
    <ValidationMessage For="@(() => validationModel.Date)" />

    <br/>
    <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
    <BitButton ButtonType="BitButtonType.Reset" Variant="BitVariant.Outline"
               OnClick="@(() => { validationModel = new(); SuccessMessage = string.Empty; })">
        Reset
    </BitButton>
</EditForm>

@* Display success message or handle submission state *@
@if (!string.IsNullOrEmpty(SuccessMessage))
{
     <BitMessage Color="BitColor.Success">@SuccessMessage</BitMessage>
}
```

```csharp
@using System.ComponentModel.DataAnnotations

@code {
    public class BitDatePickerValidationModel
    {
        [Required(ErrorMessage = "Date is required.")]
        public DateTimeOffset? Date { get; set; }
    }

    private BitDatePickerValidationModel validationModel = new();
    private string SuccessMessage = string.Empty;

    private void HandleValidSubmit() {
        SuccessMessage = "Form submitted successfully!";
        // Process valid form data
    }
    private void HandleInvalidSubmit() {
        SuccessMessage = string.Empty;
        // Handle invalid form data
    }
}
```

---

### Example 14: Style & Class Customization

Demonstrates applying custom styles and classes to the root element and various internal parts using `Style`, `Class`, `Styles`, and `Classes` parameters for detailed theming.

*(Refer to the CSS in the original HTML and the `BitDatePickerClassStyles` section below for targeting specific elements)*

```cshtml
<style>
    /* Example CSS (refer to original HTML for full set) */
    .custom-class { /* Root style via Class */ }
    .custom-root { /* Root style via Classes */ }
    .custom-label { /* Label style via Classes */ }
    .custom-input { /* Input style via Classes */ }
    .custom-day-picker { /* Day picker wrapper style */ }
    /* ... etc ... */
</style>

@* Component's Style & Class: *@
<BitDatePicker Style="margin: 1rem; box-shadow: dodgerblue 0 0 1rem;" />
<BitDatePicker Class="custom-class" />

@* Styles object for inline styles on internal parts: *@
<BitDatePicker ShowTimePicker
               Styles="@(new() { Root = "margin-inline: 1rem;",
                                 InputContainer = "background: var(--focused-background);",
                                 Group = "border: 1px solid mediumseagreen;",
                                 /* ... other styles ... */ })" />

@* Classes object for applying CSS classes to internal parts: *@
<BitDatePicker @bind-Value="@classesValue" Label="Classes Demo"
               Classes="@(new() { Root = "custom-root",
                                  Input = "custom-input",
                                  Label = $"custom-label{(classesValue is null ? string.Empty : " custom-label-top")}",
                                  DayPickerWrapper = "custom-day-picker",
                                  /* ... other classes ... */ })" />
```

```csharp
@code {
    private DateTimeOffset? classesValue;
}
```

---

### Example 15: RTL (Right-to-Left) Support

Shows the `BitDatePicker` rendered in RTL mode using `Dir="BitDir.Rtl"`.

```cshtml
<div dir="rtl"> @* Container div sets overall direction *@
    <BitDatePicker Dir="BitDir.Rtl" Label="انتخابگر تاریخ (راست به چپ)" />
</div>
```

---

## API Reference

### `BitDatePicker` Parameters

| Name                       | Type                                  | Default Value                  | Description                                                                                                   |
| :------------------------- | :------------------------------------ | :----------------------------- | :------------------------------------------------------------------------------------------------------------ |
| `AllowTextInput`           | `bool`                                | `false`                        | Whether to allow direct text input. Parsing depends on `DateFormat`.                                          |
| `AutoClose`                | `bool`                                | `true`                         | Whether the calendar callout closes automatically after selecting a date.                                     |
| `CalloutAriaLabel`         | `string`                              | `"Calendar"`                   | Aria-label for the calendar callout popup.                                                                     |
| `CalloutHtmlAttributes`    | `Dictionary<string, object>`          | `new Dictionary...`            | Additional HTML attributes for the callout wrapper element.                                                   |
| `Classes`                  | `BitDatePickerClassStyles?`           | `null`                         | Custom CSS classes for internal parts. See `BitDatePickerClassStyles` below.                                    |
| `Culture`                  | `CultureInfo`                         | `CultureInfo.CurrentUICulture` | CultureInfo used for formatting dates, month/day names.                                                       |
| `DateFormat`               | `string?`                             | `null`                         | Format string for displaying the date in the input field and parsing text input. Defaults to culture's short date pattern. |
| `DayCellTemplate`          | `RenderFragment<DateTimeOffset>?`     | `null`                         | Custom template for rendering individual day cells in the calendar. `context` is the date of the cell.       |
| `GoToNextMonthTitle`       | `string`                              | `"Go to next month"`           | Tooltip for the next month navigation button.                                                                 |
| `GoToNextYearRangeTitle`   | `string`                              | `"Next year range {0} - {1}"`  | Tooltip for the next year range button in year picker view. `{0}` and `{1}` are start/end years.            |
| `GoToNextYearTitle`        | `string`                              | `"Go to next year {0}"`        | Tooltip for the next year navigation button. `{0}` is the next year.                                         |
| `GoToPrevMonthTitle`       | `string`                              | `"Go to previous month"`       | Tooltip for the previous month navigation button.                                                             |
| `GoToPrevYearRangeTitle`   | `string`                              | `"Previous year range {0} - {1}"`| Tooltip for the previous year range button in year picker view. `{0}` and `{1}` are start/end years.      |
| `GoToPrevYearTitle`        | `string`                              | `"Go to previous year {0}"`    | Tooltip for the previous year navigation button. `{0}` is the previous year.                                 |
| `GoToTodayTitle`           | `string`                              | `"Go to today"`                | Tooltip for the "Go to Today" button.                                                                         |
| `HasBorder`                | `bool`                                | `true`                         | If `false`, removes the default border around the input field wrapper. *Note: Default is true unlike example table.* |
| `HighlightCurrentMonth`    | `bool`                                | `false`                        | Whether to visually highlight the current month in the month picker view.                                      |
| `HighlightSelectedMonth`   | `bool`                                | `false`                        | Whether to visually highlight the selected month in the month picker view.                                     |
| `HourStep`                 | `int`                                 | `1`                            | Increment/decrement step for the hour input when `ShowTimePicker` is true.                                    |
| `IconLocation`             | `BitIconLocation`                     | `Right`                        | Position of the calendar icon (Left or Right). See enum below.                                                |
| `IconName`                 | `string`                              | `"CalendarMirrored"`           | Name of the icon used as the trigger.                                                                         |
| `IconTemplate`             | `RenderFragment?`                     | `null`                         | Custom `RenderFragment` for the trigger icon. Overrides `IconName`.                                           |
| `InvalidErrorMessage`      | `string?`                             | `null`                         | Custom error message shown when `AllowTextInput` is true and the input is invalid.                            |
| `IsMonthPickerVisible`     | `bool`                                | `true`                         | Whether the month picker (year view) is shown initially when the header is clicked. *Note: Seems internal/behavioral.*|
| `IsOpen`                   | `bool`                                | `false`                        | Controls the visibility of the calendar callout. Use with `@bind-IsOpen`.                                     |
| `Label`                    | `string?`                             | `null`                         | Text label for the DatePicker.                                                                                |
| `LabelTemplate`            | `RenderFragment?`                     | `null`                         | Custom `RenderFragment` for the label. Overrides `Label`.                                                    |
| `MaxDate`                  | `DateTimeOffset?`                     | `null`                         | The latest allowable date that can be selected.                                                               |
| `MinDate`                  | `DateTimeOffset?`                     | `null`                         | The earliest allowable date that can be selected.                                                             |
| `MinuteStep`               | `int`                                 | `1`                            | Increment/decrement step for the minute input when `ShowTimePicker` is true.                                  |
| `MonthCellTemplate`        | `RenderFragment<DateTimeOffset>?`     | `null`                         | Custom template for rendering individual month cells in the year view. `context` is a date within that month. |
| `MonthPickerToggleTitle`   | `string`                              | `"{0}, change month"`          | Tooltip for the month/year header button (used to switch views). `{0}` is the current month/year text.        |
| `OnClick`                  | `EventCallback`                       |                                | Callback invoked when the input wrapper is clicked.                                                           |
| `OnFocus`                  | `EventCallback`                       |                                | Callback invoked when the input element gains focus (bubbles).                                                |
| `OnFocusIn`                | `EventCallback`                       |                                | Callback invoked when the input element gains focus (does not bubble).                                       |
| `OnFocusOut`               | `EventCallback`                       |                                | Callback invoked when the input element loses focus.                                                          |
| `OnSelectDate`             | `EventCallback<DateTimeOffset?>`      |                                | Callback invoked when a date is selected or successfully parsed. *Note: Use `@bind-Value` or `ValueChanged` typically.* |
| `Placeholder`              | `string`                              | `string.Empty`                 | Placeholder text shown in the input field when no date is selected.                                           |
| `Responsive`               | `bool`                                | `false`                        | If `true`, enables responsive layout adjustments for the callout on smaller screens.                        |
| `SelectedDateAriaAtomic`   | `string`                              | `"Selected date {0}"`          | Format string for the `aria-live` region announcing the selected date. `{0}` is the formatted date.        |
| `ShowClearButton`          | `bool`                                | `false`                        | If `true`, shows a clear button next to the input when a date is selected.                                     |
| `ShowCloseButton`          | `bool`                                | `false`                        | If `true`, shows a close button ('X') in the callout header.                                                 |
| `ShowGoToToday`            | `bool`                                | `true`                         | Whether the "Go to Today" button is visible in the calendar views.                                            |
| `ShowMonthPickerAsOverlay` | `bool`                                | `false`                        | If `true`, the month/year picker view appears as an overlay instead of replacing the day view.                |
| `ShowTimePicker`           | `bool`                                | `false`                        | If `true`, includes the time picker UI below the calendar day view.                                           |
| `ShowWeekNumbers`          | `bool`                                | `false`                        | If `true`, displays week numbers (1-53) alongside each week row in the calendar.                               |
| `StartingValue`            | `DateTimeOffset?`                     | `null`                         | The date the calendar defaults to showing when opened if no `Value` is initially set.                           |
| `Standalone`               | `bool`                                | `false`                        | If `true`, renders only the calendar/time picker UI without the input field and callout.                       |
| `Styles`                   | `BitDatePickerClassStyles?`           | `null`                         | Custom CSS inline styles for internal parts. See `BitDatePickerClassStyles` below.                             |
| `TabIndex`                 | `int`                                 | `0`                            | The `tabindex` of the DatePicker's input field.                                                               |
| `TimeFormat`               | `BitTimeFormat`                       | `TwentyFourHours`              | Specifies 12-hour or 24-hour format for the time picker UI (if shown). See enum below.                       |
| `TimeZone`                 | `TimeZoneInfo?`                       | `null`                         | Specifies the `TimeZoneInfo` to use for interpreting and displaying dates/times. Defaults to local time zone. |
| `Underlined`               | `bool`                                | `false`                        | If `true`, applies an underlined style to the input field.                                                   |
| `WeekNumberTitle`          | `string`                              | `"Week number {0}"`            | Tooltip format string for the week number display. `{0}` is the week number.                                  |
| `YearCellTemplate`         | `RenderFragment<int>?`                | `null`                         | Custom template for rendering individual year cells in the year range view. `context` is the year integer.    |
| `YearPickerToggleTitle`    | `string`                              | `"{0}, change year"`           | Tooltip for the year header button in the month picker view. `{0}` is the current year.                       |
| `YearRangePickerToggleTitle`| `string`                              | `"{0} - {1}, change month"`    | Tooltip for the year range header button in the year picker view. `{0}` and `{1}` are the start/end years. |
| **Inherited Parameters**   |                                       |                                | *Includes parameters from `BitInputBase<DateTimeOffset?>` and `BitComponentBase`.*                              |

---

### `BitDatePicker` Public Members

Methods accessible via `@ref`.

| Name            | Type                 | Description                                           |
| :-------------- | :------------------- | :---------------------------------------------------- |
| `OpenCallout()` | `Task`               | Programmatically opens the date picker callout/popup. |
| `CloseCallout()`| `Task`               | Programmatically closes the date picker callout/popup.|

---

*Inherited `BitInputBase<DateTimeOffset?>` and `BitComponentBase` parameters and members are similar to those listed in the `BitCircularTimePicker` reference, but apply to `DateTimeOffset?` values and the DatePicker's structure.*

---

### `BitDatePickerClassStyles` Properties (Used by `Classes` and `Styles` parameters)

Defines CSS classes or styles for specific internal parts of the `BitDatePicker`.

| Property                       | Type      | Description                                                              | Maps to Element(s) (approximate) |
| :----------------------------- | :-------- | :----------------------------------------------------------------------- | :--------------------------------|
| `Root`                         | `string?` | The main container `div`.                                                | `div.bit-dtp`                    |
| `Focused`                      | `string?` | Applied to `Root` when the input is focused.                             | `div.bit-dtp`                    |
| `Label`                        | `string?` | The `<label>` element.                                                   | `label.bit-dtp-lbl`              |
| `InputWrapper`                 | `string?` | The `div` wrapping the input and icon.                                   | `div.bit-dtp-wrp`                |
| `InputContainer`               | `string?` | The `div` directly containing the input and icon.                        | `div.bit-dtp-icn`                |
| `Input`                        | `string?` | The `<input type="text">` element.                                       | `input.bit-dtp-inp`              |
| `Icon`                         | `string?` | The calendar icon element (`<i>` or custom).                             | `i.bit-dtp-ico` / Template     |
| `Overlay`                      | `string?` | The overlay `div` shown behind the callout (if applicable).            | `div.bit-dtp-ovl`                |
| `Callout`                      | `string?` | The main callout `div` element.                                          | `div.bit-dtp-cal`                |
| `CalloutContainer`             | `string?` | The inner container `div` within the callout.                            | `div.bit-dtp-cac`                |
| `Group`                        | `string?` | The main group `div` inside the callout container.                      | `div.bit-dtp-grp`                |
| `DayPickerWrapper`             | `string?` | The wrapper `div` for the day picking view (calendar grid).             | `div.bit-dtp-dwp`                |
| `DayPickerHeader`              | `string?` | The header `div` containing month/year and navigation buttons.         | `div.bit-dtp-pkh`                |
| `DayPickerMonth`               | `string?` | The element displaying the current month/year text.                     | `div.bit-dtp-pkt` / `button.bit-dtp-ptb` |
| `DayPickerNavWrapper`          | `string?` | The `div` containing the month/year navigation buttons.                | `div.bit-dtp-nbc`                |
| `PrevMonthNavButton`           | `string?` | The previous month navigation `<button>`.                               | `button.bit-dtp-nbt` (prev)      |
| `PrevMonthNavIcon`             | `string?` | The icon inside the previous month button.                             | `i` (prev)                       |
| `GoToTodayButton`              | `string?` | The "Go to Today" `<button>`.                                          | `button.bit-dtp-gtb`             |
| `GoToTodayIcon`                | `string?` | The icon inside the "Go to Today" button.                              | `i.bit-dtp-gti`                  |
| `CloseButton`                  | `string?` | The close `<button>` in the header (if `ShowCloseButton` is true).     | (Internal)                       |
| `CloseButtonIcon`              | `string?` | The icon inside the close button.                                      | (Internal)                       |
| `NextMonthNavButton`           | `string?` | The next month navigation `<button>`.                                   | `button.bit-dtp-nbt` (next)      |
| `NextMonthNavIcon`             | `string?` | The icon inside the next month button.                                 | `i` (next)                       |
| `DaysHeaderRow`                | `string?` | The `div` containing the day-of-week headers (S, M, T...).             | `div.bit-dtp-dgh`                |
| `WeekNumbersHeader`            | `string?` | The header cell for the week numbers column (if `ShowWeekNumbers`).    | `div.bit-dtp-wlb` (first)        |
| `DaysRow`                      | `string?` | Each `div` representing a week row in the calendar grid.                | `div.bit-dtp-dgr`                |
| `WeekNumber`                   | `string?` | The `div` displaying the week number (if `ShowWeekNumbers`).           | `div.bit-dtp-wnm`                |
| `DayButton`                    | `string?` | Each individual day `<button>` in the grid.                             | `button.bit-dtp-dbt`             |
| `TodayDayButton`               | `string?` | Class applied to the `DayButton` representing today's date.             | `button.bit-dtp-dtd`             |
| `SelectedDayButton`            | `string?` | Class applied to the `DayButton` representing the selected date.        | `button.bit-dtp-dbs`             |
| `OtherMonthDayButton`          | `string?` | Class applied to `DayButton`s representing days from the prev/next month.| `button.bit-dtp-dbo`             |
| `DisabledDayButton`            | `string?` | Class applied to `DayButton`s that are outside the min/max range.       | (Internal, uses `disabled`)     |
| `TimePickerContainer`          | `string?` | The main `div` container for the time picker UI (if `ShowTimePicker`). | `div.bit-dtp-twp`                |
| `TimePickerWrapper`            | `string?` | The inner wrapper for the time inputs and buttons.                   | `div.bit-dtp-tic`                |
| `TimePickerDivider`            | `string?` | The divider (`:`) element between hour and minute inputs.             | `div.bit-dtp-tdv`                |
| `TimePickerHourInput`          | `string?` | The hour `<input type="number">`.                                     | `input.bit-dtp-tin` (hour)       |
| `TimePickerMinuteInput`        | `string?` | The minute `<input type="number">`.                                   | `input.bit-dtp-tin` (minute)     |
| `TimePickerIncreaseHourButton` | `string?` | The button to increase the hour value.                               | `button.bit-dtp-tbt` (up, hour)  |
| `TimePickerDecreaseHourButton` | `string?` | The button to decrease the hour value.                               | `button.bit-dtp-tbt` (down, hour)|
| `TimePickerIncreaseMinuteButton`|`string?` | The button to increase the minute value.                             | `button.bit-dtp-tbt` (up, minute)|
| `TimePickerDecreaseMinuteButton`|`string?` | The button to decrease the minute value.                             | `button.bit-dtp-tbt` (down, min) |
| `TimePickerAmPmContainer`      | `string?` | The container for AM/PM buttons (if using 12H format).               | (Internal, within `TimePickerWrapper`) |
| `TimePickerAmButton`           | `string?` | The AM selection button.                                             | (Internal `button`)              |
| `TimePickerPmButton`           | `string?` | The PM selection button.                                             | (Internal `button`)              |
| `Divider`                      | `string?` | The main divider `div` between day picker and month/year picker.     | `div.bit-dtp-dvd`                |
| `YearMonthPickerWrapper`       | `string?` | The wrapper `div` for the month/year picker view.                     | `div.bit-dtp-mwp`                |
| `MonthPickerHeader`            | `string?` | The header `div` in the month picker view (contains year, nav buttons).| `div.bit-dtp-pkh` (month view)   |
| `YearPickerToggleButton`       | `string?` | The `<button>` displaying the current year (clickable to change view).  | `button.bit-dtp-ptb` (month view)|
| `MonthPickerNavWrapper`        | `string?` | The `div` containing year navigation buttons in the month picker view.| `div.bit-dtp-nbc` (month view)   |
| `PrevYearNavButton`            | `string?` | The previous year navigation `<button>` in the month picker view.     | `button.bit-dtp-nbt` (prev year) |
| `PrevYearNavIcon`              | `string?` | The icon in the previous year button.                               | `i` (prev year)                  |
| `NextYearNavButton`            | `string?` | The next year navigation `<button>` in the month picker view.         | `button.bit-dtp-nbt` (next year) |
| `NextYearNavIcon`              | `string?` | The icon in the next year button.                                    | `i` (next year)                  |
| `MonthsContainer`              | `string?` | The `div` containing the grid of month buttons.                      | `div.bit-dtp-pkc` (month view)   |
| `MonthsRow`                    | `string?` | Each `div` representing a row of month buttons.                        | `div.bit-dtp-pkr` (month view)   |
| `MonthButton`                  | `string?` | Each individual month `<button>`.                                      | `button.bit-dtp-pkb`             |
| `SelectedMonthButton`          | `string?` | Class applied to the selected month button.                            | `button.bit-dtp-pkb[aria-selected="true"]` |
| `CurrentMonthButton`           | `string?` | Class applied to the current month button (if `HighlightCurrentMonth`). | `button.bit-dtp-pcm`             |
| `YearPickerHeader`             | `string?` | The header `div` in the year picker view (contains year range, nav).  | `div.bit-dtp-pkh` (year view)    |
| `MonthPickerToggleButton`      | `string?` | The `<button>` displaying the year range (clickable to change view).    | `button.bit-dtp-ptb` (year view) |
| `YearPickerNavWrapper`         | `string?` | The `div` containing year range navigation buttons.                   | `div.bit-dtp-nbc` (year view)    |
| `PrevYearRangeNavButton`       | `string?` | The previous year range navigation `<button>`.                         | `button.bit-dtp-nbt` (prev range)|
| `PrevYearRangeNavIcon`         | `string?` | The icon in the previous year range button.                            | `i` (prev range)                 |
| `NextYearRangeNavButton`       | `string?` | The next year range navigation `<button>`.                             | `button.bit-dtp-nbt` (next range)|
| `NextYearRangeNavIcon`         | `string?` | The icon in the next year range button.                                | `i` (next range)                 |
| `YearsContainer`               | `string?` | The `div` containing the grid of year buttons.                        | `div.bit-dtp-pkc` (year view)    |
| `YearsRow`                     | `string?` | Each `div` representing a row of year buttons.                         | `div.bit-dtp-pkr` (year view)    |
| `YearButton`                   | `string?` | Each individual year `<button>`.                                       | `button.bit-dtp-pkb`             |
| `SelectedYearButton`           | `string?` | Class applied to the selected year button.                             | `button.bit-dtp-pkb[aria-selected="true"]` |
| `CurrentYearButton`            | `string?` | Class applied to the current year button (if `HighlightCurrentMonth`). | (Likely needs specific style)    |

---

### Related Enums

* **`BitTimeFormat`:** (See `BitCircularTimePicker` reference) - Controls 12/24 hour format for the time picker.
* **`BitIconLocation`:** (See `BitCircularTimePicker` reference) - Controls icon position (Left/Right).
* **`BitVisibility`:** (See `BitCircularTimePicker` reference) - Controls component visibility (Visible/Hidden/Collapsed).
* **`BitDir`:** (See `BitCircularTimePicker` reference) - Controls text direction (Ltr/Rtl/Auto).

---

## Key Considerations & Best Practices

* **Value Type:** Binds to `DateTimeOffset?`. Ensure your model property matches. The `DateTimeOffset` includes timezone information, which might be relevant depending on how you use the `TimeZone` parameter.
* **Formatting vs. Parsing:** `DateFormat` controls both display and parsing (if `AllowTextInput` is true). Ensure the format is unambiguous and provide clear placeholders if text input is enabled. Invalid text input will result in a `null` value or validation errors.
* **Min/Max Dates:** Use `MinDate` and `MaxDate` to prevent users from selecting invalid dates (e.g., past dates for a future booking).
* **Culture:** Set the `Culture` property explicitly if you need specific localization (month/day names, first day of week) different from the application's current culture.
* **Time Picker:** Enable `ShowTimePicker` only when both date and time selection are required. Use `HourStep` and `MinuteStep` for specific time interval requirements.
* **Standalone Mode:** Use `Standalone` when you need to embed the calendar UI directly, bypassing the input field and callout mechanism. Handle value changes via `@bind-Value` or `OnSelectDate`.
* **Templates:** Use templates (`DayCellTemplate`, `MonthCellTemplate`, `YearCellTemplate`) for advanced visual customization, like highlighting specific dates (holidays, weekends), adding badges, or changing the appearance based on context.
* **Responsiveness:** Consider enabling `Responsive` for better user experience on mobile devices.
* **Time Zone:** Be mindful of `TimeZone` implications, especially in distributed applications or when dealing with users across different regions. Test thoroughly based on your target runtime and configuration.
* **Accessibility:** Always provide a `Label` or `LabelTemplate` for proper screen reader association. The component includes ARIA attributes, but context within your application is crucial.