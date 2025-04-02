# BitRating Blazor Component

**Objective:** This document provides context and reference information about the `BitRating` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's purpose, features, parameters, and usage.

**Key Component:** `BitRating`

---

## Overview

`BitRating` shows people's opinions of a product (or item), often represented by stars, helping others make informed decisions. It also allows users to provide their own rating.

---

## Usage Examples

**1. Basic**

*   **Description**: Demonstrates the default rating component, a disabled version with a pre-set value, and a read-only version displaying a specific rating.
*   **Code**:
    ```cshtml
    <BitRating />

    <BitRating IsEnabled="false" DefaultValue="2" />

    <BitRating ReadOnly DefaultValue="3.5" />
    ```

**2. Visibility**

*   **Description**: Shows how to control the visibility of the rating component using the `Visibility` parameter (`Visible`, `Hidden`, `Collapsed`).
*   **Code**:
    ```cshtml
    Visible: [ <BitRating Visibility="BitVisibility.Visible" /> ]
    Hidden: [ <BitRating Visibility="BitVisibility.Hidden" /> ]
    Collapsed: [ <BitRating Visibility="BitVisibility.Collapsed" /> ]
    ```

**3. Style & Class**

*   **Description**: Demonstrates applying custom styling using inline `Style`, root `Class`, and the `Styles` and `Classes` parameters for targeted styling of internal elements (selected/unselected icons).
*   **Code**: (Includes CSS for context)
    ```css
    .custom-class {
        margin-inline: 1rem;
        border-radius: 0.25rem;
        padding-inline: 0.5rem;
        border: 1px solid dodgerblue;
        box-shadow: dodgerblue 0 0 1rem;
    }

    /* Styles for Classes parameter example */
    .custom-selected {
        color: seagreen;
    }
    .custom-unselected {
        color: mediumseagreen;
    }
    .custom-unselected:hover {
        color: lightseagreen;
    }
    ```
    ```cshtml
    <BitRating Style="padding-inline: 0.5rem; margin-inline: 1rem; box-shadow: tomato 0 0 1rem; border-radius: 1rem;" />

    <BitRating Class="custom-class" />

    <BitRating Styles="@(new() { SelectedIcon = "color: blueviolet;", UnselectedIcon = "color: blueviolet;" })" />

    <BitRating Classes="@(new() { SelectedIcon = "custom-selected", UnselectedIcon = "custom-unselected" })" />
    ```

**4. Max value**

*   **Description**: Shows how to change the maximum number of rating items (stars) using the `Max` parameter.
*   **Code**:
    ```cshtml
    <BitRating Max="6" />

    <div style="width: 200px;">
        <BitRating Max="100" />
    </div>
    ```

**5. Icons**

*   **Description**: Demonstrates customizing the icons used for the selected (`SelectedIconName`) and unselected (`UnselectedIconName`) states.
*   **Code**:
    ```cshtml
    <BitRating SelectedIconName="@BitIconName.HeartFill" UnselectedIconName="@BitIconName.Heart" />

    <BitRating SelectedIconName="@BitIconName.CheckboxCompositeReversed" UnselectedIconName="@BitIconName.Checkbox" />

    <BitRating SelectedIconName="@BitIconName.LikeSolid" UnselectedIconName="@BitIconName.Dislike" />
    ```

**6. Size**

*   **Description**: Shows how to change the visual size of the rating icons using the `Size` parameter (`Small`, `Medium` (default), `Large`).
*   **Code**:
    ```cshtml
    <BitRating Size="BitSize.Small" />
    <BitRating Size="BitSize.Medium" />
    <BitRating Size="BitSize.Large" />
    ```

**7. Binding**

*   **Description**: Illustrates one-way (`Value`), two-way (`@bind-Value`), and `OnChange` event handling for the rating value. Also shows `AllowZeroStars="true"` to permit a zero rating.
*   **Code**:
    ```cshtml
    <BitRating AllowZeroStars="true" Value="oneWayBinding" />
    <BitToggleButton @bind-IsChecked="oneWayBindingToggle" OnChange="v => oneWayBinding = v ? 5 : 0" Text="@(oneWayBinding == 5 ? "Unstar All" : "Star All")" /> @* Adjusted example for clarity *@

    <BitRating @bind-Value="twoWayBinding" />
    <BitNumberField @bind-Value="twoWayBinding" />

    <BitRating DefaultValue="2" OnChange="v => onChangeValue = v" />
    <BitLabel>Changed Value: @onChangeValue</BitLabel>
    ```
    ```csharp
    @code {
        private double oneWayBinding = 0;
        // private bool oneWayBindingToggle; // Helper for the toggle button example
        private double twoWayBinding = 3;
        private double onChangeValue;
    }
    ```

**8. Validation**

*   **Description**: Shows how to integrate `BitRating` within an `EditForm` for validation, ensuring a value is selected or within a specific range using data annotations (`[Range]`).
*   **Code**: (Includes CSS for context)
    ```css
    .validation-message { color: red; }
    ```
    ```cshtml
    @using System.ComponentModel.DataAnnotations;

    <EditForm Model="ValidationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
        <DataAnnotationsValidator />

        <BitRating AllowZeroStars="true" @bind-Value="ValidationModel.Value" />
        <ValidationMessage For="@(() => ValidationModel.Value)" />

        <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
    </EditForm>
    ```
    ```csharp
    @code {
        public class BitRatingDemoFormModel
        {
            [Range(typeof(double), "1", "5", ErrorMessage = "Your rate must be between {1} and {2}")]
            public double Value { get; set; } // Default is 0, which is invalid based on Range[1,5]
        }

        public BitRatingDemoFormModel ValidationModel = new();

        private void HandleValidSubmit() { }
        private void HandleInvalidSubmit() { }
    }
    ```

**9. RTL**

*   **Description**: Demonstrates rendering the `BitRating` component in a right-to-left layout using `Dir="BitDir.Rtl"`.
*   **Code**:
    ```cshtml
    <BitRating Dir="BitDir.Rtl" />
    ```

---

## API Reference

**BitRating Parameters**

| Name                 | Type                            | Default             | Description                                                                                                   |
| :------------------- | :------------------------------ | :------------------ | :------------------------------------------------------------------------------------------------------------ |
| `AllowZeroStars`     | `bool`                          | `false`             | Allows the initial rating value to be 0. A zero value cannot be selected via UI interaction.                   |
| `AriaLabelFormat`    | `string?`                       | `null`              | Format string for the aria-label of individual rating stars (e.g., "{0} of {1} stars").                           |
| `Classes`            | `BitRatingClassStyles?`         | `null`              | Custom CSS classes for different parts (Root, Button, IconContainer, SelectedIcon, UnselectedIcon).           |
| `DefaultValue`       | `double?`                       | `null`              | Initial rating value (uncontrolled).                                                                          |
| `GetAriaLabel`       | `Func<double, double, string>?` | `null`              | Callback to generate the `aria-label` for the entire control in read-only mode or as a fallback.            |
| `Max`                | `int`                           | `5`                 | Maximum rating value (number of stars).                                                                     |
| `SelectedIconName`   | `string`                        | `FavoriteStarFill`  | Icon name for selected/filled rating elements.                                                                |
| `Size`               | `BitSize?`                      | `null`              | Visual size of the rating icons (`Small`, `Medium`, `Large`).                                                 |
| `Styles`             | `BitRatingClassStyles?`         | `null`              | Custom CSS styles for different parts.                                                                        |
| `UnselectedIconName` | `string`                        | `FavoriteStar`      | Icon name for unselected/empty rating elements.                                                               |
| *(Inherited)*        | *(See BitInputBase)*            |                     |                                                                                                               |

**BitInputBase Parameters (Inherited)**

| Name                | Type                              | Default              | Description                                                                    |
| :------------------ | :-------------------------------- | :------------------- | :----------------------------------------------------------------------------- |
| `DisplayName`       | `string?`                         | `null`               | Display name for validation messages.                                          |
| `InputHtmlAttributes`| `IReadOnlyDictionary<string, object>?`| `null`               | Additional attributes applied to the hidden input element.                     |
| `Name`              | `string?`                         | `null`               | `name` attribute for the hidden input, allowing form association.            |
| `NoValidate`        | `bool`                            | `false`              | Disables validation.                                                           |
| `OnChange`          | `EventCallback<double?>`          |                      | Callback when the bound `Value` changes.                                       |
| `ReadOnly`          | `bool`                            | `false`              | Makes the rating control read-only (visual only, prevents user interaction). |
| `Required`          | `bool`                            | `false`              | Marks the input as required (for form validation).                             |
| `Value`             | `double?`                         | `null`               | The current rating value (use `@bind-Value`).                                  |
| *(Inherited)*       | *(See BitComponentBase)*          |                      |                                                                                |

**BitInputBase Public Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitComponentBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details)*

**BitRatingClassStyles Properties**

| Name            | Type      | Default | Description                                     |
| :-------------- | :-------- | :------ | :---------------------------------------------- |
| `Root`          | `string?` | `null`  | CSS class/style for the root `div` element.   |
| `Button`        | `string?` | `null`  | CSS class/style for each rating icon `button`. |
| `IconContainer` | `string?` | `null`  | CSS class/style for the container `div` inside each button. |
| `SelectedIcon`  | `string?` | `null`  | CSS class/style for the selected/filled icon `i`. |
| `UnselectedIcon`| `string?` | `null`  | CSS class/style for the unselected/empty icon `i`. |

**Enums**

*   **BitSize**: Defines size options (`Small`, `Medium`, `Large`).
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Rating/BitRatingDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Rating/BitRatingDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Rating/BitRating.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Rating/BitRating.razor)

