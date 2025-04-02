# BitSearchBox Blazor Component

**Objective:** This document provides context and reference information about the `BitSearchBox` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's purpose, features, parameters, and usage patterns for generating code or explanations.

**Key Component:** `BitSearchBox`

---

## Overview

`BitSearchBox` is an input component specifically designed for searching content within a site or application. It provides a text field where users can enter search queries to find specific items.

---

## Usage Examples

**1. Basic**

*   **Description**: Standard search box with a placeholder and a disabled version.
*   **Code**:
    ```cshtml
    <BitSearchBox Placeholder="Search" />
    <BitSearchBox Placeholder="Disabled" IsEnabled="false" />
    ```

**2. Underlined**

*   **Description**: Search box styled with only an underline instead of a full border.
*   **Code**:
    ```cshtml
    <BitSearchBox Placeholder="Search" Underlined />
    <BitSearchBox Placeholder="Disabled" IsEnabled="false" Underlined />
    ```

**3. NoBorder**

*   **Description**: Search box rendered without any border.
*   **Code**:
    ```cshtml
    <BitSearchBox Placeholder="Search" NoBorder />
    <BitSearchBox Placeholder="Disabled" IsEnabled="false" NoBorder />
    ```

**4. Accent**

*   **Description**: Demonstrates applying different accent colors (Primary, Secondary, Tertiary, Transparent) to the search box using the `Accent` parameter (of type `BitColorKind`). This example specifically uses the `NoBorder` style as well.
*   **Code**:
    ```cshtml
    <BitSearchBox Placeholder="Primary" Accent="BitColorKind.Primary" NoBorder />
    <BitSearchBox Placeholder="Secondary" Accent="BitColorKind.Secondary" NoBorder />
    <BitSearchBox Placeholder="Tertiary" Accent="BitColorKind.Tertiary" NoBorder />
    <BitSearchBox Placeholder="Transparent" Accent="BitColorKind.Transparent" NoBorder />
    ```

**5. Icon**

*   **Description**: Shows options for the search icon: `FixedIcon` (always visible), `DisableAnimation` (icon doesn't animate on focus), customizing the icon with `IconName`, and hiding the icon completely with `HideIcon`.
*   **Code**:
    ```cshtml
    <BitSearchBox Placeholder="FixedIcon" FixedIcon />
    <BitSearchBox Placeholder="DisableAnimation" DisableAnimation />
    <BitSearchBox Placeholder="Custom icon" IconName="@BitIconName.Filter" />
    <BitSearchBox Placeholder="HideIcon" HideIcon />
    ```

**6. Search Button**

*   **Description**: Demonstrates adding an explicit search button next to the input using `ShowSearchButton`. The button's icon can be customized with `SearchButtonIconName`. Works with different styles like `Underlined` and `NoBorder`, and respects the `IsEnabled` state.
*   **Code**:
    ```cshtml
    <BitSearchBox Placeholder="Search" ShowSearchButton />
    <BitSearchBox Placeholder="SearchButtonIconName" ShowSearchButton SearchButtonIconName="PageListFilter" />
    <BitSearchBox Placeholder="Underlined" Underlined ShowSearchButton />
    <BitSearchBox Placeholder="Disabled" IsEnabled="false" ShowSearchButton />
    <BitSearchBox Placeholder="Disabled Underlined" IsEnabled="false" Underlined ShowSearchButton />
    <BitSearchBox Placeholder="NoBorder" NoBorder ShowSearchButton /> @* Added based on visual example *@
    <BitSearchBox Placeholder="Disabled NoBorder" IsEnabled="false" NoBorder ShowSearchButton /> @* Added based on visual example *@
    ```

**7. Binding**

*   **Description**: Shows two-way binding (`@bind-Value`), handling value changes immediately (`Immediate` with `@bind-Value` or `OnChange`), triggering search on Enter (`OnSearch`), and clearing the input (`OnClear`).
*   **Code**:
    ```cshtml
    @* Two-way binding *@
    <BitSearchBox Placeholder="Search" @bind-Value="twoWaySearchValue" />
    <BitTextField Placeholder="Search Value" @bind-Value="twoWaySearchValue" />

    @* Immediate two-way binding *@
    <BitSearchBox Placeholder="Search" Immediate @bind-Value="immediateTwoWaySearchValue" />
    <BitTextField Placeholder="Search Value" Immediate @bind-Value="immediateTwoWaySearchValue" />

    @* OnChange event (immediate) *@
    <BitSearchBox Placeholder="Search" Immediate
                  OnChange="s => onChangeSearchValue = s"
                  OnClear="() => onChangeSearchValue = string.Empty" />
    <div>Search Value: @onChangeSearchValue</div>

    @* OnSearch event (triggered on Enter) *@
    <BitSearchBox Placeholder="Search" Immediate
                  OnSearch="s => onSearchValue = s"
                  OnClear="() => onSearchValue = string.Empty" />
    <div>Search Value: @onSearchValue</div>
    ```
    ```csharp
    @code {
        private string twoWaySearchValue;
        private string immediateTwoWaySearchValue;
        private string onChangeSearchValue;
        private string onSearchValue;
    }
    ```

**8. Suggestion (AutoComplete)**

*   **Description**: Enables suggestions/autocomplete dropdown using `SuggestItems` or `SuggestItemsProvider`. Features demonstrated: basic suggestions, custom filtering (`SuggestFilterFunction`), minimum characters to trigger suggestions (`MinSuggestTriggerChars`), limiting suggestion count (`MaxSuggestCount`), debouncing input (`DebounceTime`), and loading suggestions dynamically (`SuggestItemsProvider`).
*   **Code**:
    ```cshtml
    @* Basic Suggestions *@
    <BitSearchBox @bind-Value="@searchValue" Immediate Placeholder="e.g. Apple"
                  SuggestItems="GetSuggestedItems()" />

    @* Custom Filter Function *@
    <BitSearchBox @bind-Value="@searchValueWithSuggestFilterFunction" Immediate Placeholder="e.g. Apple"
                  SuggestItems="GetSuggestedItems()" SuggestFilterFunction="@SearchFunc" />

    @* Minimum Trigger Characters *@
    <BitSearchBox @bind-Value="@searchValueWithMinSearchLength" Immediate Placeholder="e.g. Apple"
                  MinSuggestTriggerChars="1" SuggestItems="GetSuggestedItems()" />

    @* Maximum Suggestion Count *@
    <BitSearchBox @bind-Value="@searchValueWithMaxSuggestedItems" Immediate Placeholder="e.g. Apple"
                  MaxSuggestCount="2" SuggestItems="GetSuggestedItems()" />

    @* Debounce Time *@
    <BitSearchBox @bind-Value="@searchValueWithSearchDelay" Immediate DebounceTime="2000"
                  Placeholder="e.g. Apple" SuggestItems="GetSuggestedItems()" />

    @* Items Provider (Dynamic Loading) *@
    <BitSearchBox @bind-Value="@searchValueWithItemsProvider" Immediate Placeholder="e.g. Pro"
                  SuggestItemsProvider="LoadItems" />
    <div>SearchValue: @searchValueWithItemsProvider</div>
    ```
    ```csharp
    @code {
        private string searchValue;
        private string searchValueWithSuggestFilterFunction;
        private string searchValueWithSearchDelay;
        private string searchValueWithMinSearchLength;
        private string searchValueWithMaxSuggestedItems;
        private string searchValueWithItemsProvider;

        private List<string> GetSuggestedItems() =>
        [
            "Apple", "Red Apple", "Blue Apple", "Green Apple", "Banana",
            "Orange", "Grape", "Broccoli", "Carrot", "Lettuce"
        ];

        // Custom search logic (example: starts with)
        private Func<string?, string?, bool> SearchFunc = (searchText, itemText) =>
        {
            if (string.IsNullOrEmpty(searchText) || string.IsNullOrEmpty(itemText)) return false;
            return itemText.StartsWith(searchText, StringComparison.OrdinalIgnoreCase);
        };

        // Example provider function (replace with actual data fetching)
        private async ValueTask<IEnumerable<string>> LoadItems(BitSearchBoxSuggestItemsProviderRequest request)
        {
            try
            {
                // Simulate filtering based on request.SearchTerm and request.Take
                await Task.Delay(200); // Simulate network latency
                var query = request.SearchTerm?.ToLowerInvariant() ?? string.Empty;
                return GetSuggestedItems().Where(i => i.ToLowerInvariant().Contains(query)).Take(request.Take > 0 ? request.Take : 5);
            }
            catch
            {
                return [];
            }
        }
    }
    ```

**9. Validation**

*   **Description**: Shows how to use `BitSearchBox` within an `EditForm` and apply validation rules using data annotations (e.g., `[StringLength]`).
*   **Code**: (Includes CSS for context)
    ```css
    .validation-message { color: #A4262C; font-size: 0.75rem; }
    ```
    ```cshtml
    @using System.ComponentModel.DataAnnotations;

    <EditForm Model="validationBoxModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
        <DataAnnotationsValidator />
        <BitSearchBox Placeholder="Search" Immediate
                      DefaultValue="This is default value"
                      @bind-Value="validationBoxModel.Text" />
        <ValidationMessage For="() => validationBoxModel.Text" />
    </EditForm>
    ```
    ```csharp
    @code {
        public class ValidationSearchBoxModel
        {
            [StringLength(6, MinimumLength = 2, ErrorMessage = "Text must be between 2 and 6 chars.")]
            public string Text { get; set; }
        }

        private ValidationSearchBoxModel validationBoxModel = new() { Text = "This is default value" }; // Initialize with default

        private void HandleValidSubmit() { }
        private void HandleInvalidSubmit() { }
    }
    ```

**10. Color**

*   **Description**: Applies different theme colors (`Primary`, `Secondary`, `Tertiary`, `Info`, etc.) to the search box using the `Color` parameter.
*   **Code**: (Example for Primary)
    ```cshtml
    <BitSearchBox Placeholder="Search" Color="BitColor.Primary" /> @* Default color is typically primary *@
    <BitSearchBox Placeholder="Search" Color="BitColor.Secondary" />
    @* ... other colors ... *@
    ```
    *(Note: The provided HTML doesn't explicitly show the `Color` parameter usage in the CSHTML, but demonstrates the visual result for various `BitColor` values.)*

**11. Style & Class**

*   **Description**: Demonstrates applying custom styling via inline `Style`, root `Class`, and the `Styles`/`Classes` parameters for specific internal elements (Root, InputContainer, Focused state, ClearButton, Icon, etc.).
*   **Code**: (Includes CSS for context)
    ```css
    .custom-class { overflow: hidden; margin-inline: 1rem; border-radius: 1rem; border: 2px solid tomato; }
    .custom-class * { border: none; }

    /* Styles for the 'Classes' parameter example */
    .custom-root { margin-inline: 1rem; }
    .custom-input-container { height: 3rem; overflow: hidden; align-items: center; border-radius: 1.5rem; border-color: #13a3a375; background-color: #13a3a375; }
    .custom-focused .custom-input-container { border-width: 1px; border-color: #13a3a375; }
    .custom-clear:hover { background: transparent; }
    .custom-icon { color: darkslategrey; }
    .custom-icon-wrapper { width: 2rem; height: 2rem; border-radius: 1rem; margin-inline: 0.5rem; background-color: whitesmoke; }
    ```
    ```cshtml
    <BitSearchBox Placeholder="Style" Style="box-shadow: dodgerblue 0 0 1rem; margin-inline: 1rem;" />

    <BitSearchBox Placeholder="Class" Class="custom-class" />

    <BitSearchBox Placeholder="Styles"
                  Styles="@(new() { Root = "margin-inline: 1rem;",
                                    Input = "padding: 0.5rem;",
                                    Focused = "--focused-background: #b2b2b25a;",
                                    InputContainer = "background: var(--focused-background);" })" />

    <BitSearchBox FixedIcon Placeholder="Classes"
                  Classes="@(new() { Root = "custom-root",
                                     Icon = "custom-icon",
                                     Focused = "custom-focused",
                                     ClearButton = "custom-clear",
                                     IconWrapper = "custom-icon-wrapper",
                                     InputContainer = "custom-input-container" })" />
    ```

**12. RTL**

*   **Description**: Shows how to render the `BitSearchBox` component in a right-to-left layout using `Dir="BitDir.Rtl"`.
*   **Code**:
    ```cshtml
    <BitSearchBox Placeholder="جستجو" Dir="BitDir.Rtl" />
    ```

---

## API Reference

**BitSearchBox Parameters**

| Name                       | Type                                            | Default             | Description                                                                     |
| :------------------------- | :---------------------------------------------- | :------------------ | :------------------------------------------------------------------------------ |
| `Accent`                   | `BitColorKind?`                                 | `null`              | Accent color kind (Primary, Secondary, Tertiary, Transparent).                  |
| `Classes`                  | `BitSearchBoxClassStyles?`                      | `null`              | Custom CSS classes for different parts.                                         |
| `Color`                    | `BitColor?`                                     | `null`              | General theme color for elements like icons.                                    |
| `DefaultValue`             | `string?`                                       | `null`              | Initial value (uncontrolled).                                                   |
| `DisableAnimation`         | `bool`                                          | `false`             | Disables the focus animation of the search icon.                                |
| `FixedIcon`                | `bool`                                          | `false`             | Keeps the search icon always visible, even when focused.                        |
| `HideIcon`                 | `bool`                                          | `false`             | Hides the search icon entirely.                                                 |
| `HideClearButton`          | `bool`                                          | `false`             | Hides the clear button ('X') when the input has value.                          |
| `IconName`                 | `string`                                        | `Search`            | Custom icon name for the search icon.                                           |
| `InputMode`                | `BitInputMode?`                                 | `null`              | Sets the `inputmode` HTML attribute for virtual keyboard hints.                 |
| `MaxSuggestCount`          | `int`                                           | `5`                 | Maximum number of suggestions to display.                                       |
| `MinSuggestTriggerChars`   | `int`                                           | `3`                 | Minimum characters needed to trigger suggestions.                               |
| `NoBorder`                 | `bool`                                          | `false`             | Removes the default border.                                                     |
| `OnClear`                  | `EventCallback`                                 |                     | Callback when the clear button is clicked or Esc is pressed with value.       |
| `OnEscape`                 | `EventCallback`                                 |                     | Callback when the Escape key is pressed.                                        |
| `OnSearch`                 | `EventCallback<string?>`                        |                     | Callback when the Enter key is pressed or the search button is clicked.         |
| `Placeholder`              | `string?`                                       | `null`              | Placeholder text for the input.                                                 |
| `SearchButtonIconName`     | `string`                                        | `ChromeBackMirrored`| Custom icon name for the search button (if shown).                            |
| `ShowSearchButton`         | `bool`                                          | `false`             | Shows an explicit search button next to the input.                              |
| `Styles`                   | `BitSearchBoxClassStyles?`                      | `null`              | Custom CSS styles for different parts.                                          |
| `SuggestFilterFunction`    | `Func<string?, string?, bool>?`                 | `null`              | Custom function to filter `SuggestItems`.                                       |
| `SuggestItems`             | `ICollection<string>?`                          | `null`              | List of suggestions to display.                                                 |
| `SuggestItemsProvider`     | `BitSearchBoxSuggestItemsProvider?`             | `null`              | Function to provide suggestions dynamically (for virtualization/async).         |
| `SuggestItemTemplate`      | `RenderFragment<string>?`                       | `null`              | Custom template for rendering suggestion items.                                 |
| `Underlined`               | `bool`                                          | `false`             | Renders with an underline style instead of a full border.                       |
| *(Inherited)*              | *(See BitTextInputBase)*                        |                     |                                                                                 |

**BitSearchBox Public Members**

| Name                 | Type               | Description                                             |
| :------------------- | :----------------- | :------------------------------------------------------ |
| `InputElement`       | `ElementReference` | `ElementReference` for the main input element.          |
| `FocusAsync`         | `() => ValueTask`  | Method to programmatically focus the input element.     |
| *(Inherited)*        | *(See BitInputBase)*|                                                         |

**BitTextInputBase Parameters (Inherited)**

| Name           | Type      | Default | Description                                                          |
| :------------- | :-------- | :------ | :------------------------------------------------------------------- |
| `AutoComplete` | `string?` | `null`  | `autocomplete` attribute for the input.                            |
| `AutoFocus`    | `bool`    | `false` | Auto-focuses the input on first render.                              |
| `DebounceTime` | `int`     | `0`     | Debounce time (ms) for value changes before triggering `OnChange`.   |
| `Immediate`    | `bool`    | `false` | Triggers `OnChange` on the `oninput` event instead of `onchange`.    |
| `ThrottleTime` | `int`     | `0`     | Throttle time (ms) for value changes before triggering `OnChange`. |

**BitInputBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitComponentBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitSearchBoxClassStyles Properties**

| Name                       | Type      | Default | Description                                                          |
| :------------------------- | :-------- | :------ | :------------------------------------------------------------------- |
| `Root`                     | `string?` | `null`  | CSS class/style for the root `div`.                                  |
| `InputContainer`           | `string?` | `null`  | CSS class/style for the container `div` holding input and icons.   |
| `Focused`                  | `string?` | `null`  | CSS class/style applied to the root element when focused.            |
| `ClearButton`              | `string?` | `null`  | CSS class/style for the clear button (`<button>`).                   |
| `ClearButtonContainer`     | `string?` | `null`  | CSS class/style for the container `div` of the clear button.       |
| `ClearButtonIcon`          | `string?` | `null`  | CSS class/style for the clear button's icon (`<i>`).                |
| `ClearButtonIconContainer` | `string?` | `null`  | CSS class/style for the container `span` of the clear button icon. |
| `Input`                    | `string?` | `null`  | CSS class/style for the `input` element.                             |
| `SearchIcon`               | `string?` | `null`  | CSS class/style for the search icon (`<i>`).                         |
| `SearchIconContainer`      | `string?` | `null`  | CSS class/style for the container `div` of the search icon.        |

**Enums**

*   **BitColorKind**: Defines accent color options (`Primary`, `Secondary`, `Tertiary`, `Transparent`).
*   **BitColor**: Defines general theme color options (used less directly here, mainly for icons if not overridden by accent).
*   **BitInputMode**: Defines `inputmode` attribute values (`None`, `Text`, `Decimal`, `Numeric`, `Tel`, `Search`, `Email`, `Url`).
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/SearchBox/BitSearchBoxDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/SearchBox/BitSearchBoxDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/SearchBox/BitSearchBox.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/SearchBox/BitSearchBox.razor)

