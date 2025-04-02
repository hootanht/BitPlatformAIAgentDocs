# BitCalendar Blazor Component

**Objective:** This document provides context and reference information about the `BitCalendar` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's features, generate relevant code snippets, and explain its usage.

**Key Component:** `BitCalendar`

---

## Overview

The `BitCalendar` control allows users to select and view a single date or a range of dates. It comprises three distinct views: month view, year view, and decade view.

---

## Usage Examples

**1. Basic**

*   **Description**: Demonstrates fundamental `BitCalendar` configurations including default usage, disabled state (`IsEnabled="false"`), showing week numbers (`ShowWeekNumbers="true"`), highlighting the current and selected months (`HighlightCurrentMonth`, `HighlightSelectedMonth`), and integrating a time picker (`ShowTimePicker="true"`) with a starting value (`StartingValue`).
*   **Code**:
    ```cshtml
    <BitCalendar />
    <BitCalendar IsEnabled="false" />
    <BitCalendar ShowWeekNumbers="true" />
    <BitCalendar HighlightCurrentMonth="true" HighlightSelectedMonth="true" />
    <BitCalendar ShowTimePicker="true" StartingValue="startingValue" />
    ```
    ```csharp
    @code {
        private DateTimeOffset? startingValue = new DateTimeOffset(2020, 12, 4, 20, 45, 0, DateTimeOffset.Now.Offset);
    }
    ```

**2. Min & Max**

*   **Description**: Illustrates how to set minimum (`MinDate`) and maximum (`MaxDate`) selectable dates, restricting the user's selection range by days, months, or years relative to the current date (`DateTimeOffset.Now`).
*   **Code**:
    ```cshtml
    <BitCalendar MinDate="DateTimeOffset.Now.AddDays(-5)" MaxDate="DateTimeOffset.Now.AddDays(5)" />
    <BitCalendar MinDate="DateTimeOffset.Now.AddMonths(-2)" MaxDate="DateTimeOffset.Now.AddMonths(1)" />
    <BitCalendar MinDate="DateTimeOffset.Now.AddYears(-5)" MaxDate="DateTimeOffset.Now.AddYears(1)" />
    ```

**3. Style & Class**

*   **Description**: Showcases applying custom styles and classes. Examples include using the `Style` attribute for inline styles, the `Class` attribute for assigning a CSS class to the root element, and the `Styles` and `Classes` parameters for targeting specific internal elements of the calendar (like the root, day pickers, buttons, headers, etc.) for detailed customization.
*   **Code**: (Includes CSS for context)
    ```css
    .custom-class {
        margin: 1rem;
        background: #8a2be270;
        border-radius: 1rem;
        box-shadow: blueviolet 0 0 1rem;
    }

    /* Styles for the 'Classes' parameter example */
    .custom-root { margin: 1rem; border-radius: 0.5rem; background-color: #211e1b; }
    .custom-day-picker { border: 1px solid #e9981e; background-color: #211e1b; border-end-start-radius: 0.5rem; border-start-start-radius: 0.5rem; }
    .custom-day-month, .custom-next-month, .custom-prev-month { color: white; }
    .custom-day { color: #e9981e; margin: 0.15rem; border-radius: 50%; border: 1px solid #e9981e; }
    .custom-today-day { color: #211e1b; background-color: #e9981e; }
    .custom-week-header { color: white; margin: 0.15rem; }
    .custom-day-header { height: 2rem; color: white; margin: 0.15rem; padding-bottom: 0.5rem; border-bottom: 1px solid #e9981e; }
    .custom-year-picker { border: 1px solid #211e1b; background-color: #e9981e; border-end-end-radius: 0.5rem; border-start-end-radius: 0.5rem; }
    ```
    ```cshtml
    <BitCalendar Style="margin: 1rem; border-radius: 1rem; background: #a5104457;" />

    <BitCalendar Class="custom-class" />

    <BitCalendar ShowTimePicker="true"
                 Styles="@(new() { Root = "margin: 1rem; border: 1px solid mediumseagreen; background: #1c73324d;",
                                   Divider = "border-color: mediumseagreen;",
                                   DayPickerMonth = "color: darkgreen;",
                                   TodayDayButton = "background-color: green;",
                                   SelectedDayButton = "background-color: limegreen;",
                                   TimePickerIncreaseHourButton = "background-color: limegreen;",
                                   TimePickerIncreaseMinuteButton = "background-color: limegreen;",
                                   TimePickerDecreaseHourButton = "background-color: limegreen;",
                                   TimePickerDecreaseMinuteButton = "background-color: limegreen;" })" />

    <BitCalendar Classes="@(new() { Root = "custom-root",
                                 DayPickerWrapper = "custom-day-picker",
                                 DayButton = "custom-day",
                                 TodayDayButton = "custom-today-day",
                                 PrevMonthNavButton = "custom-prev-month",
                                 NextMonthNavButton = "custom-next-month",
                                 DayPickerMonth = "custom-day-month",
                                 DayPickerHeader = "custom-day-header",
                                 WeekNumbersHeader = "custom-week-header",
                                 YearMonthPickerWrapper = "custom-year-picker" })" />
    ```

**4. Binding**

*   **Description**: Shows how to bind the selected date value using `@bind-Value`. The example displays the selected date below the calendar.
*   **Code**:
    ```cshtml
    <BitCalendar @bind-Value="@selectedDate" />
    <div>Selected date: @selectedDate.ToString()</div>
    ```
    ```csharp
    @code {
        private DateTimeOffset? selectedDate = new DateTimeOffset(2023, 8, 19, 0, 0, 0, DateTimeOffset.Now.Offset);
    }
    ```

**5. Culture**

*   **Description**: Demonstrates localization using the `Culture` parameter. It shows examples using Farsi (fa-IR) culture with both standard Farsi and "Fingilish" (Farsi using Latin characters) month/day names. It also mentions using `CultureInfoHelper` for creating custom cultures. The `GoToToday` parameter is used to provide localized text for the "Go to today" button.
*   **Code**:
    ```cshtml
    <BitCalendar GoToToday="برو به امروز" Culture="CultureInfoHelper.GetFaIrCultureWithFarsiNames()" />
    <BitCalendar GoToToday="Boro be emrouz" Culture="CultureInfoHelper.GetFaIrCultureWithFingilishNames()" />
    ```

**6. Templates**

*   **Description**: Explains how to customize the rendering of individual cells using templates: `DayCellTemplate`, `MonthCellTemplate`, and `YearCellTemplate`. Examples include adding badges to specific days, changing background colors for months, and adding a suffix to the year display.
*   **Code**: (Includes CSS for context)
    ```css
    .day-cell { width: 28px; height: 28px; position: relative; }
    .weekend-cell { color: red; }
    .badge { top: 2px; right: 2px; width: 8px; height: 8px; position: absolute; border-radius: 50%; background-color: red; }
    .year-suffix { position: absolute; bottom: 10px; right: -12px; height: 12px; color: gray; font-size: 8px; }
    ```
    ```cshtml
    <BitCalendar>
        <DayCellTemplate>
            <span class="day-cell@(context.DayOfWeek == DayOfWeek.Sunday ? " weekend-cell" : null)">
                @context.Day
                @if (context.Day % 5 is 0)
                {
                    <span class="badge"></span>
                }
            </span>
        </DayCellTemplate>
    </BitCalendar>

    <BitCalendar>
        <MonthCellTemplate>
            <div style="width:28px;padding:3px;color:black;background:@(context.Month == 1 ? "lightcoral" : "yellowgreen")">
                @Culture.DateTimeFormat.GetAbbreviatedMonthName(context.Month)
            </div>
        </MonthCellTemplate>
    </BitCalendar>

    <BitCalendar>
        <YearCellTemplate>
            <span style="position: relative">
                @context
                <span class="year-suffix">AC</span>
            </span>
        </YearCellTemplate>
    </BitCalendar>
    ```

**7. MonthPicker**

*   **Description**: Shows how to control the visibility (`ShowMonthPicker`) and positioning (`ShowMonthPickerAsOverlay`) of the month picker view. `ShowMonthPickerAsOverlay` determines if the month picker appears on top of the day picker or beside it.
*   **Code**:
    ```cshtml
    <BitCalendar ShowMonthPicker="@showMonthPicker" />
    <BitToggleButton OnText="MonthPicker visible" OffText="MonthPicker invisible" @bind-IsChecked="@showMonthPicker" />

    <BitCalendar ShowMonthPickerAsOverlay="@showMonthPickerAsOverlay" />
    <BitToggleButton OnText="Position Overlay" OffText="Position Besides" @bind-IsChecked="@showMonthPickerAsOverlay" />
    ```
    ```csharp
    @code {
        private bool showMonthPicker = true;
        private bool showMonthPickerAsOverlay;
    }
    ```

**8. TimePicker**

*   **Description**: Integrates the time picker with the calendar using `ShowTimePicker="true"` and binds the selected date and time using `@bind-Value`.
*   **Code**:
    ```cshtml
    <BitCalendar @bind-Value="@selectedDateTime" ShowTimePicker="true" />
    <div>Selected DateTime: @selectedDateTime.ToString()</div>
    ```
    ```csharp
    @code {
        private DateTimeOffset? selectedDateTime = DateTimeOffset.Now;
    }
    ```

**9. Hour/Minute Step**

*   **Description**: Customizes the step value for incrementing/decrementing hours (`HourStep`) and minutes (`MinuteStep`) in the time picker.
*   **Code**:
    ```cshtml
    <BitCalendar ShowTimePicker="true" HourStep="2" />
    <BitCalendar ShowTimePicker="true" MinuteStep="15" />
    ```

**10. Validation**

*   **Description**: Demonstrates using `BitCalendar` within an `EditForm` for validation purposes. It uses `DataAnnotationsValidator` and `@bind-Value` to link the calendar's selected date to a model property with validation attributes (like `[Required]`). `ValidationMessage` displays errors.
*   **Code**:
    ```cshtml
    <style>
        .validation-message { color: red; }
    </style>

    <EditForm Model="validationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
        <DataAnnotationsValidator />

        <BitCalendar @bind-Value="validationModel.Date" />
        <ValidationMessage For="@(() => validationModel.Date)" />

        <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
        <BitButton ButtonType="BitButtonType.Reset" Variant="BitVariant.Outline"
                   OnClick="@(() => { validationModel = new(); SuccessMessage=string.Empty; })">
            Reset
        </BitButton>
    </EditForm>
    ```
    ```csharp
    @code {
        public class BitCalendarValidationModel
        {
            [Required]
            public DateTimeOffset? Date { get; set; }
        }

        private BitCalendarValidationModel validationModel = new();

        private void HandleValidSubmit() { /* Logic for valid submission */ }
        private void HandleInvalidSubmit() { /* Logic for invalid submission */ }
    }
    ```

**11. RTL**

*   **Description**: Shows how to render the calendar in a right-to-left layout using `Dir="BitDir.Rtl"`.
*   **Code**:
    ```cshtml
    <BitCalendar Dir="BitDir.Rtl" />
    ```

---

## API Reference

**BitCalendar Parameters**

| Name                         | Type                            | Default                                            | Description                                                                       |
| :--------------------------- | :------------------------------ | :------------------------------------------------- | :-------------------------------------------------------------------------------- |
| `Classes`                    | `BitCalendarClassStyles?`       | `null`                                             | Custom CSS classes for different parts.                                           |
| `Culture`                    | `CultureInfo`                   | `CultureInfo.CurrentUICulture`                     | CultureInfo for the Calendar (localization).                                      |
| `DateFormat`                 | `string?`                       | `null`                                             | Custom format string for the date display.                                        |
| `DayCellTemplate`            | `RenderFragment<DateTimeOffset>?` | `null`                                             | Custom template for rendering day cells.                                          |
| `GoToNextMonthTitle`         | `string`                        | `Go to next month`                                 | Tooltip for the next month navigation button.                                     |
| `GoToNextYearRangeTitle`     | `string`                        | `Next year range {0} - {1}`                        | Tooltip for the next year range navigation button.                                |
| `GoToNextYearTitle`          | `string`                        | `Go to next year {0}`                              | Tooltip for the next year navigation button.                                      |
| `GoToPrevMonthTitle`         | `string`                        | `Go to previous month`                             | Tooltip for the previous month navigation button.                                 |
| `GoToPrevYearRangeTitle`     | `string`                        | `Previous year range {0} - {1}`                    | Tooltip for the previous year range navigation button.                            |
| `GoToPrevYearTitle`          | `string`                        | `Go to previous year {0}`                          | Tooltip for the previous year navigation button.                                  |
| `GoToTodayTitle`             | `string`                        | `Go to today`                                      | Tooltip for the "Go to today" button.                                             |
| `GoToNowTitle`               | `string`                        | `Go to now`                                        | Tooltip for the "Go to now" button (in time picker).                            |
| `HighlightCurrentMonth`      | `bool`                          | `false`                                            | Highlights the current month in the month picker view.                            |
| `HighlightSelectedMonth`     | `bool`                          | `false`                                            | Highlights the selected month in the month picker view.                           |
| `HideTimePickerTitle`        | `string`                        | `Hide time picker`                                 | Tooltip for the hide time picker button.                                          |
| `InvalidErrorMessage`        | `string?`                       | `null`                                             | Custom validation error message for invalid input.                                |
| `ShowMonthPicker`            | `bool`                          | `true`                                             | Whether the month/year picker view is shown alongside the day view.               |
| `MaxDate`                    | `DateTimeOffset?`               | `null`                                             | Maximum allowable date.                                                           |
| `MinDate`                    | `DateTimeOffset?`               | `null`                                             | Minimum allowable date.                                                           |
| `MonthCellTemplate`          | `RenderFragment<DateTimeOffset>?` | `null`                                             | Custom template for rendering month cells.                                        |
| `MonthPickerToggleTitle`     | `string`                        | `{0}, change month`                                | Tooltip for the month picker toggle button in the day view header.                |
| `ShowMonthPickerAsOverlay`   | `bool`                          | `false`                                            | Shows the month picker as an overlay instead of alongside the day picker.         |
| `OnSelectDate`               | `EventCallback<DateTimeOffset?>`|                                                    | Callback triggered when a date is selected.                                       |
| `SelectedDateAriaAtomic`     | `string`                        | `Selected date {0}`                                | Format string for the aria-atomic announcement when a date is selected.         |
| `ShowGoToToday`              | `bool`                          | `true`                                             | Shows/hides the "Go to today" button.                                             |
| `ShowTimePicker`             | `bool`                          | `false`                                            | Shows/hides the time picker controls.                                             |
| `ShowTimePickerTitle`        | `string`                        | `Show time picker`                                 | Tooltip for the show time picker button.                                          |
| `ShowWeekNumbers`            | `bool`                          | `false`                                            | Shows/hides the week number column.                                               |
| `ShowGoToNow`                | `bool`                          | `true`                                             | Shows/hides the "Go to now" button in the time picker.                            |
| `StartingValue`              | `DateTimeOffset?`               | `null`                                             | The date/time the calendar initially displays if `Value` is null.                 |
| `Styles`                     | `BitCalendarClassStyles?`       | `null`                                             | Custom CSS styles for different parts.                                            |
| `TimeFormat`                 | `BitTimeFormat`                 | `BitTimeFormat.TwentyFourHours`                    | Time format (`TwentyFourHours`, `TwelveHours`).                                   |
| `WeekNumberTitle`            | `string`                        | `Week number {0}`                                  | Tooltip format for the week number display.                                       |
| `YearCellTemplate`           | `RenderFragment<int>?`          | `null`                                             | Custom template for rendering year cells.                                         |
| `YearPickerToggleTitle`      | `string`                        | `{0}, change year`                                 | Tooltip for the year picker toggle button in the month view header.               |
| `YearRangePickerToggleTitle` | `string`                        | `{0} - {1}, change month`                          | Tooltip for the year range picker toggle button in the year view header.          |
| `HourStep`                   | `int`                           | `1`                                                | Step value for hour increments/decrements in the time picker.                   |
| `MinuteStep`                 | `int`                           | `1`                                                | Step value for minute increments/decrements in the time picker.                 |
| *(Inherited)*                | *(See BitInputBase)*            |                                                    |                                                                                   |

**BitInputBase Parameters (Inherited)**

| Name                | Type                              | Default              | Description                                                                    |
| :------------------ | :-------------------------------- | :------------------- | :----------------------------------------------------------------------------- |
| `DisplayName`       | `string?`                         | `null`               | Display name for the field (used in validation messages).                      |
| `InputHtmlAttributes`| `IReadOnlyDictionary<string, object>?`| `null`               | Additional attributes applied to the internal input element (if applicable). |
| `Name`              | `string?`                         | `null`               | `name` attribute for the input, allowing form association.                   |
| `NoValidate`        | `bool`                            | `false`              | Disables built-in validation.                                                  |
| `OnChange`          | `EventCallback<DateTimeOffset?>`  |                      | Callback when the bound `Value` changes.                                       |
| `ReadOnly`          | `bool`                            | `false`              | Makes the input read-only (visual state, may not prevent programmatic changes).|
| `Required`          | `bool`                            | `false`              | Marks the input as required (visual cue, use validation attributes for logic).|
| `Value`             | `DateTimeOffset?`                 | `null`               | The selected date/time value (use `@bind-Value`).                              |
| *(Inherited)*       | *(See BitComponentBase)*          |                      |                                                                                |

**BitComponentBase Parameters (Inherited)**

| Name           | Type                         | Default                   | Description                                                           |
| :------------- | :--------------------------- | :------------------------ | :-------------------------------------------------------------------- |
| `AriaLabel`    | `string?`                    | `null`                    | Aria-label for accessibility.                                         |
| `Class`        | `string?`                    | `null`                    | Custom CSS class for the root element.                                |
| `Dir`          | `BitDir?`                    | `null`                    | Component direction (`Ltr`, `Rtl`, `Auto`).                           |
| `HtmlAttributes`| `Dictionary<string, object>` | `new Dictionary<>()`      | Additional HTML attributes to render on the root element.               |
| `Id`           | `string?`                    | `null`                    | Custom ID for the root element (defaults to `UniqueId`).              |
| `IsEnabled`    | `bool`                       | `true`                    | Whether the component is enabled.                                     |
| `Style`        | `string?`                    | `null`                    | Custom CSS style for the root element.                                |
| `Visibility`   | `BitVisibility`              | `BitVisibility.Visible`   | Component visibility (`Visible`, `Hidden`, `Collapsed`).              |

**BitComponentBase Public Members (Inherited)**

| Name        | Type               | Default          | Description                                       |
| :---------- | :----------------- | :--------------- | :------------------------------------------------ |
| `UniqueId`  | `Guid`             | `Guid.NewGuid()` | Readonly unique ID assigned at construction.      |
| `RootElement` | `ElementReference` |                  | `ElementReference` for the root DOM element.    |

**BitCalendarClassStyles Properties (for `Classes`/`Styles`)**

| Name                         | Type      | Default | Description                                                            |
| :--------------------------- | :-------- | :------ | :--------------------------------------------------------------------- |
| `Root`                       | `string?` | `null`  | CSS class/style for the root element.                                  |
| `Container`                  | `string?` | `null`  | CSS class/style for the main container.                                |
| `DayPickerWrapper`           | `string?` | `null`  | CSS class/style for the day picker wrapper.                            |
| `DayPickerHeader`            | `string?` | `null`  | CSS class/style for the day picker header.                             |
| `DayPickerMonth`             | `string?` | `null`  | CSS class/style for the month text in the day picker header.           |
| `DayPickerNavWrapper`        | `string?` | `null`  | CSS class/style for the navigation button container in day picker.     |
| `PrevMonthNavButton`         | `string?` | `null`  | CSS class/style for the previous month button.                         |
| `PrevMonthNavIcon`           | `string?` | `null`  | CSS class/style for the previous month icon.                           |
| `GoToTodayButton`            | `string?` | `null`  | CSS class/style for the "Go to today" button.                          |
| `GoToTodayIcon`              | `string?` | `null`  | CSS class/style for the "Go to today" icon.                            |
| `NextMonthNavButton`         | `string?` | `null`  | CSS class/style for the next month button.                             |
| `NextMonthNavIcon`           | `string?` | `null`  | CSS class/style for the next month icon.                               |
| `DaysHeaderRow`              | `string?` | `null`  | CSS class/style for the row containing day abbreviations (S, M, T...). |
| `WeekNumbersHeader`          | `string?` | `null`  | CSS class/style for the week number column header (if shown).          |
| `DaysRow`                    | `string?` | `null`  | CSS class/style for each row containing day buttons.                   |
| `WeekNumber`                 | `string?` | `null`  | CSS class/style for the week number cell (if shown).                   |
| `DayButton`                  | `string?` | `null`  | CSS class/style for individual day buttons.                            |
| `TodayDayButton`             | `string?` | `null`  | CSS class/style specifically for the button representing today's date. |
| `SelectedDayButton`          | `string?` | `null`  | CSS class/style specifically for the currently selected day button.    |
| `TimePickerContainer`        | `string?` | `null`  | CSS class/style for the time picker's outer container.                 |
| `TimePickerWrapper`          | `string?` | `null`  | CSS class/style for the time picker's inner wrapper.                   |
| `TimePickerHourInput`        | `string?` | `null`  | CSS class/style for the hour input field.                              |
| `TimePickerHourMinuteSeparator`| `string?` | `null`  | CSS class/style for the separator (:) between hour and minute.       |
| `TimePickerMinuteInput`      | `string?` | `null`  | CSS class/style for the minute input field.                            |
| `Divider`                    | `string?` | `null`  | CSS class/style for the divider line between date and time pickers.    |
| `YearMonthPickerWrapper`     | `string?` | `null`  | CSS class/style for the wrapper containing month/year/decade pickers.  |
| `MonthPickerHeader`          | `string?` | `null`  | CSS class/style for the month picker header.                           |
| `YearPickerToggleButton`     | `string?` | `null`  | CSS class/style for the year toggle button in the month picker header. |
| `MonthPickerNavWrapper`      | `string?` | `null`  | CSS class/style for the navigation button container in month picker.   |
| `PrevYearNavButton`          | `string?` | `null`  | CSS class/style for the previous year button.                          |
| `PrevYearNavIcon`            | `string?` | `null`  | CSS class/style for the previous year icon.                            |
| `NextYearNavButton`          | `string?` | `null`  | CSS class/style for the next year button.                              |
| `NextYearNavIcon`            | `string?` | `null`  | CSS class/style for the next year icon.                                |
| `MonthsRow`                  | `string?` | `null`  | CSS class/style for each row containing month buttons.                 |
| `MonthButton`                | `string?` | `null`  | CSS class/style for individual month buttons.                          |
| `YearPickerHeader`           | `string?` | `null`  | CSS class/style for the year picker header.                            |
| `MonthPickerToggleButton`    | `string?` | `null`  | CSS class/style for the month toggle button in the year picker header. |
| `YearPickerNavWrapper`       | `string?` | `null`  | CSS class/style for the navigation button container in year picker.    |
| `PrevYearRangeNavButton`     | `string?` | `null`  | CSS class/style for the previous year range button.                    |
| `PrevYearRangeNavIcon`       | `string?` | `null`  | CSS class/style for the previous year range icon.                      |
| `NextYearRangeNavButton`     | `string?` | `null`  | CSS class/style for the next year range button.                        |
| `NextYearRangeNavIcon`       | `string?` | `null`  | CSS class/style for the next year range icon.                          |
| `YearsRow`                   | `string?` | `null`  | CSS class/style for each row containing year buttons.                  |
| `YearButton`                 | `string?` | `null`  | CSS class/style for individual year buttons.                           |

**Enums**

*   **BitTimeFormat**: Defines time format options (`TwentyFourHours`, `TwelveHours`).
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Calendar/BitCalendarDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Calendar/BitCalendarDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Calendar/BitCalendar.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Calendar/BitCalendar.razor)

