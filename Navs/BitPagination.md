<!--
AI Agent Reference File: BitPagination Component

Purpose: This file provides detailed information about the Blazor `BitPagination` component.
Use this reference when generating, analyzing, or modifying code involving BitPagination.
Focus on its core function (page navigation), key parameters (Count, SelectedPage, BoundaryCount, MiddleCount, Variant, Color, Size),
binding patterns (@bind-SelectedPage, OnChange), and customization options (icons, styles, classes).
-->

# BitPagination Component Reference (Blazor)

## Overview

The `BitPagination` component provides a user interface for navigating through a series of pages or sections of content. It displays page numbers and navigation buttons (previous, next, first, last) allowing users to easily jump between pages. This is commonly used with lists, tables, search results, or any content-rich interface split into multiple views.

---

## Usage

The core functionality revolves around the `Count` parameter (total number of pages) and managing the `SelectedPage`.

### Basic Usage

Specify the total number of pages using the `Count` parameter. The component handles rendering the page buttons and basic navigation.

```razor
<BitPagination Count="5" />
```

**Explanation:**

* `Count="5"`: Tells the component there are 5 pages in total. It will render page buttons 1 through 5, plus previous/next buttons (disabled appropriately on the first/last page).

### Variants

The component offers different visual styles through the `Variant` parameter.

```razor
<BitPagination Count="5" Variant="BitVariant.Fill" />
<BitPagination Count="5" Variant="BitVariant.Outline" />
<BitPagination Count="5" Variant="BitVariant.Text" />
```

**Explanation:**

* `Variant="BitVariant.Fill"`: (Default) Buttons have a filled background, especially the selected one.
* `Variant="BitVariant.Outline"`: Buttons have an outline border.
* `Variant="BitVariant.Text"`: Buttons appear primarily as text, with minimal borders/background (often used for a less prominent look).

### Setting the Default Page

Use `DefaultSelectedPage` to specify which page should be initially selected when the component loads. Note that this is only an initial value; subsequent selections are handled internally unless you use binding.

```razor
<BitPagination Count="5" DefaultSelectedPage="3" />
```

**Explanation:**

* `DefaultSelectedPage="3"`: The component will initially render with page 3 highlighted as selected.

### Controlling Displayed Pages (`BoundaryCount`, `MiddleCount`)

When there are many pages, the component uses ellipsis (`•••`) to avoid showing all page numbers. These parameters control how many numbers are shown.

* `BoundaryCount`: Number of page buttons always visible at the *beginning* and *end* of the pagination range.
* `MiddleCount`: Number of page buttons shown *around the currently selected page*.

```razor
@* Show 1 page at start/end, and 3 pages around the current page (6) *@
<BitPagination Count="11" DefaultSelectedPage="6" BoundaryCount="1" MiddleCount="3" />
@* Renders something like: [<<] [<] [1] [...] [5] [6] [7] [...] [11] [>] [>>] *@

@* Default BoundaryCount is 2, Default MiddleCount is 3 *@
<BitPagination Count="11" DefaultSelectedPage="6" />
@* Renders something like: [<<] [<] [1] [2] [...] [5] [6] [7] [...] [10] [11] [>] [>>] *@
```

**Explanation:**

* These parameters help keep the pagination control compact even with a large number of total pages (`Count`).

### Additional Navigation Buttons

You can add buttons to jump directly to the first and last pages.

```razor
<BitPagination Count="24" ShowFirstButton ShowLastButton />
```

**Explanation:**

* `ShowFirstButton`: Adds a "First page" button (often `<<` icon).
* `ShowLastButton`: Adds a "Last page" button (often `>>` icon).
* `ShowPreviousButton` (default: `true`): Shows the "<" button.
* `ShowNextButton` (default: `true`): Shows the ">" button.

### Custom Icons

Customize the icons used for the navigation buttons.

```razor
<BitPagination Count="5"
               NextIcon="@BitIconName.Next"
               PreviousIcon="@BitIconName.Previous"
               FirstIcon="@BitIconName.DoubleChevronLeft" @* Example if ShowFirstButton is true *@
               LastIcon="@BitIconName.DoubleChevronRight" @* Example if ShowLastButton is true *@
               />
```

**Explanation:**

* Provide the desired `BitIconName` string to the respective icon parameters (`FirstIcon`, `PreviousIcon`, `NextIcon`, `LastIcon`).

### Color Theming

Apply a theme color using the `Color` parameter (works with different `Variant`s).

```razor
<BitPagination Count="5" Color="BitColor.Success" />
<BitPagination Count="5" Color="BitColor.Warning" Variant="BitVariant.Outline" />
<BitPagination Count="5" Color="BitColor.Info" Variant="BitVariant.Text" />
```

**Explanation:**

* `Color="BitColor..."`: Applies the specified theme color (Primary, Secondary, Success, Error, etc.) to the component, primarily affecting the selected item's style.

### Sizing

Control the overall size of the pagination buttons using the `Size` parameter.

```razor
<BitPagination Count="5" Size="BitSize.Small" />
<BitPagination Count="5" Size="BitSize.Medium" /> @* Default Size *@
<BitPagination Count="5" Size="BitSize.Large" />
```

**Explanation:**

* `Size="BitSize..."`: Adjusts the padding and font size of the pagination buttons (Small, Medium, Large).

### Binding and Events

Manage the selected page programmatically.

* **One-Way Binding (`SelectedPage`)**: Set the current page from your code. The component reflects this value but doesn't update your variable when the user clicks.
* **Two-Way Binding (`@bind-SelectedPage`)**: Keeps your C# variable synchronized with the component's selected page. User clicks update the variable, and changes to the variable update the component.
* **Event Handling (`OnChange`)**: Executes a callback method whenever the selected page changes, passing the new page number (`int`) as an argument.

```razor
@* One-Way Binding *@
<BitPagination Count="5" SelectedPage="oneWayPage" />
<BitNumberField @bind-Value="oneWayPage" Min="1" Max="5" />

@* Two-Way Binding *@
<BitPagination Count="5" @bind-SelectedPage="twoWayPage" />
<BitNumberField @bind-Value="twoWayPage" Min="1" Max="5" />

@* OnChange Event *@
<BitPagination Count="5" OnChange="HandlePageChange" />
<div>Changed page: <b>@changedPage</b></div>

@code {
    private int oneWayPage = 1;
    private int twoWayPage = 2;
    private int changedPage = 1; // Store the last changed value

    private void HandlePageChange(int newPage)
    {
        changedPage = newPage;
        // You might fetch data for the new page here
        Console.WriteLine($"Page changed to: {newPage}");
    }
}
```

### Styling (`Style`, `Class`, `Styles`, `Classes`)

Customize appearance using standard HTML attributes or specific style/class objects.

* **`Style` / `Class`:** Apply to the root `div` element of the pagination component.
* **`Styles` / `Classes` Parameters:** Provide `BitPaginationClassStyles` objects to target internal elements like `Root`, `Button`, `SelectedButton`, `Ellipsis`, `FirstButton`, `PreviousButton`, `NextButton`, `LastButton`, and their icons.

```razor
@* Direct Style/Class on root *@
<BitPagination Count="5" Style="background-color: lightblue; padding: 10px; border-radius: 8px;" />
<BitPagination Count="5" Class="my-pagination-container" />

@* Granular styling via Styles *@
<BitPagination Count="5" Styles="@(new BitPaginationClassStyles {
                                       Root = "gap: 2px;",
                                       Button = "border-radius: 50%; border: 1px solid grey;",
                                       SelectedButton = "background-color: navy; color: white; border-color: navy;",
                                       Ellipsis = "color: grey; align-self: end;"
                                   })" />

@* Granular styling via Classes (assuming CSS definitions exist) *@
<BitPagination Count="5" Classes="@(new BitPaginationClassStyles {
                                      Root = "custom-pagination-root",
                                      Button = "custom-page-button",
                                      SelectedButton = "custom-selected-page",
                                      PreviousButton = "custom-nav-button"
                                   })" />
```

### Right-to-Left (RTL) Support

Render the component layout for RTL languages using the `Dir` parameter.

```razor
<div dir="rtl"> @* Container div recommended for proper layout *@
    <BitPagination Count="5" Dir="BitDir.Rtl" />
</div>
```

**Explanation:**

* `Dir="BitDir.Rtl"` reverses the order of buttons and adjusts icon mirroring for RTL context.

---

## Key Parameters (`BitPagination`)

<!-- AI: Focus on these common parameters when generating BitPagination code. -->

| Parameter             | Type                     | Default             | Description                                                        |
| :-------------------- | :----------------------- | :------------------ | :----------------------------------------------------------------- |
| `Count`               | `int`                    | `1`                 | **Required.** Total number of pages.                               |
| `SelectedPage`        | `int`                    | `0`                 | The currently selected page number (1-based). Use for binding.     |
| `DefaultSelectedPage` | `int`                    | `0`                 | The initially selected page number (1-based). Only sets initial state. |
| `OnChange`            | `EventCallback<int>`     | -                   | Callback function invoked when the selected page changes.          |
| `BoundaryCount`       | `int`                    | `2`                 | Number of pages displayed at the start and end.                    |
| `MiddleCount`         | `int`                    | `3`                 | Number of pages displayed around the current page.                 |
| `Variant`             | `BitVariant?`            | `BitVariant.Fill`   | Visual style: Fill, Outline, Text.                                 |
| `Color`               | `BitColor?`              | `BitColor.Primary`  | Theme color applied to the component.                              |
| `Size`                | `BitSize?`               | `BitSize.Medium`    | Size of the pagination buttons (Small, Medium, Large).             |
| `ShowFirstButton`     | `bool`                   | `false`             | Whether to display the "First page" button.                        |
| `ShowLastButton`      | `bool`                   | `false`             | Whether to display the "Last page" button.                         |
| `ShowPreviousButton`  | `bool`                   | `true`              | Whether to display the "Previous page" button.                     |
| `ShowNextButton`      | `bool`                   | `true`              | Whether to display the "Next page" button.                         |
| `IsEnabled`           | `bool`                   | `true`              | Enables/disables the entire pagination control.                    |
| `FirstIcon`           | `string?`                | `ChevronRightEnd6`  | Icon for the "First page" button.                                  |
| `PreviousIcon`        | `string?`                | `ChevronRight`      | Icon for the "Previous page" button.                               |
| `NextIcon`            | `string?`                | `ChevronRight`      | Icon for the "Next page" button.                                   |
| `LastIcon`            | `string?`                | `ChevronRightEnd6`  | Icon for the "Last page" button.                                   |
| `Dir`                 | `BitDir?`                | `null`              | Sets the text direction (Ltr, Rtl, Auto).                          |
| `Styles`              | `BitPaginationClassStyles?`| `null`              | Custom inline styles for internal elements.                        |
| `Classes`             | `BitPaginationClassStyles?`| `null`              | Custom CSS classes for internal elements.                          |
| `Style`               | `string?`                | `null`              | Custom inline style for the root element.                          |
| `Class`               | `string?`                | `null`              | Custom CSS class for the root element.                             |

---

## API Parameter Tables (Detailed)

*(These tables are based on the provided HTML API section)*

### `BitPagination` Parameters

*(See Key Parameters table above for the most common ones)*

| Name                  | Type                        | Default             | Description                                                      |
| :-------------------- | :-------------------------- | :------------------ | :--------------------------------------------------------------- |
| `BoundaryCount`       | `int`                       | `2`                 | Number of items at the start and end.                            |
| `Classes`             | `BitPaginationClassStyles?` | `null`              | Custom CSS classes for different parts.                          |
| `Color`               | `BitColor?`                 | `null` (`Primary`)  | General color of the pagination.                                 |
| `Count`               | `int`                       | `1`                 | Total number of pages.                                           |
| `DefaultSelectedPage` | `int`                       | `0`                 | Default selected page number (1-based).                          |
| `FirstIcon`           | `string?`                   | `null` (`ChevronRightEnd6`) | Icon name of the first button.                             |
| `LastIcon`            | `string?`                   | `null` (`ChevronRightEnd6`) | Icon name of the last button.                              |
| `MiddleCount`         | `int`                       | `3`                 | Number of items in the middle.                                   |
| `NextIcon`            | `string?`                   | `null` (`ChevronRight`)     | Icon name of the next button.                              |
| `OnChange`            | `EventCallback<int>`        | `null`              | Event callback for when selected page changes.                   |
| `PreviousIcon`        | `string?`                   | `null` (`ChevronRight`)     | Icon name of the previous button.                          |
| `SelectedPage`        | `int`                       | `0`                 | Selected page number (1-based). Use `@bind-SelectedPage` for 2-way. |
| `ShowFirstButton`     | `bool`                      | `false`             | Whether to show the first button.                                |
| `ShowLastButton`      | `bool`                      | `false`             | Whether to show the last button.                                 |
| `ShowNextButton`      | `bool`                      | `true`              | Whether to show the next button.                                 |
| `ShowPreviousButton`  | `bool`                      | `true`              | Whether to show the previous button.                             |
| `Size`                | `BitSize?`                  | `null` (`Medium`)   | Size of the buttons.                                             |
| `Styles`              | `BitPaginationClassStyles?` | `null`              | Custom CSS styles for different parts.                           |
| `Variant`             | `BitVariant?`               | `null` (`Fill`)     | Visual variant of the pagination.                                |
| ... (Inherited from `BitComponentBase`: `AriaLabel`, `Class`, `Dir`, `HtmlAttributes`, `Id`, `IsEnabled`, `Style`, `Visibility`) ... |                             |                     |                                                                  |

### `BitPaginationClassStyles` Properties

| Name               | Type      | Description                                                      |
| :----------------- | :-------- | :--------------------------------------------------------------- |
| `Root`             | `string?` | Custom CSS classes/styles for the root element.                  |
| `Button`           | `string?` | Custom CSS classes/styles for the page number buttons.           |
| `Ellipsis`         | `string?` | Custom CSS classes/styles for the ellipsis (`•••`).              |
| `SelectedButton`   | `string?` | Custom CSS classes/styles for the *selected* page number button. |
| `FirstButton`      | `string?` | Custom CSS classes/styles for the first button.                  |
| `FirstButtonIcon`  | `string?` | Custom CSS classes/styles for the first button's icon.           |
| `PreviousButton`   | `string?` | Custom CSS classes/styles for the previous button.               |
| `PreviousButtonIcon`| `string?` | Custom CSS classes/styles for the previous button's icon.        |
| `NextButton`       | `string?` | Custom CSS classes/styles for the next button.                   |
| `NextButtonIcon`   | `string?` | Custom CSS classes/styles for the next button's icon.            |
| `LastButton`       | `string?` | Custom CSS classes/styles for the last button.                   |
| `LastButtonIcon`   | `string?` | Custom CSS classes/styles for the last button's icon.            |

### Relevant Enums

* **`BitVariant`**: `Fill`, `Outline`, `Text` (Note: `Standard` is listed in API, seems equivalent to `Outline`)
* **`BitColor`**: `Primary`, `Secondary`, `Tertiary`, `Info`, `Success`, `Warning`, `SevereWarning`, `Error`
* **`BitSize`**: `Small`, `Medium`, `Large`
* **`BitDir`**: `Ltr`, `Rtl`, `Auto`
* **`BitVisibility`**: `Visible`, `Hidden`, `Collapsed`

---

## AI Agent Guidance Summary

* Use `<BitPagination>` for navigating between pages of content.
* **Core Parameter:** `Count` (int) is required to set the total number of pages.
* **Selection:**
  * Use `DefaultSelectedPage` (int, 1-based) for initial selection.
  * Use `SelectedPage` (int, 1-based) for one-way binding.
  * Use `@bind-SelectedPage` (int, 1-based) for two-way binding.
  * Use `OnChange` (EventCallback<int>) to react to page changes.
* **Display Control:**
  * Use `BoundaryCount` (int) to set pages shown at ends.
  * Use `MiddleCount` (int) to set pages shown around the current one.
* **Appearance:**
  * Use `Variant` (`BitVariant.Fill`, `Outline`, `Text`) for button style.
  * Use `Color` (`BitColor`) for theme color.
  * Use `Size` (`BitSize`) for button size.
* **Navigation Buttons:**
  * Use `ShowFirstButton`, `ShowLastButton`, `ShowPreviousButton`, `ShowNextButton` (bool) to toggle visibility.
  * Use `FirstIcon`, `PreviousIcon`, `NextIcon`, `LastIcon` (string, `BitIconName`) to customize icons.
* **Customization:** Apply `Style`/`Class` to the root, or use `Styles`/`Classes` (`BitPaginationClassStyles`) for granular control over internal elements (buttons, selected state, ellipsis, nav icons).
* **RTL:** Use `Dir="BitDir.Rtl"` for right-to-left layout.
* **State:** Use `IsEnabled` (bool) to disable the control.

