# BitChoiceGroup Blazor Component

**Objective:** This document provides context and reference information about the `BitChoiceGroup` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's features, generate relevant code snippets, and explain its usage.

**Key Component:** `BitChoiceGroup`
**Aliases:** `Radio`, `RadioButton`, `RadioGroup`, `RadioButtonGroup`

---

## Overview

`BitChoiceGroup` allows users to select a single option from a list of two or more choices. It functions similarly to a group of radio buttons.

---

## Notes

*   **Multi-API Component:** The `BitChoiceGroup` can be populated with items in three different ways:
    1.  Using a list of `BitChoiceGroupItem<TValue>` objects passed to the `Items` parameter.
    2.  Using a list of custom generic objects (`TItem`) passed to the `Items` parameter, along with `NameSelectors` to map properties.
    3.  Using `BitChoiceGroupOption` components nested within the `BitChoiceGroup` (`ChildContent`/`Options`).
*   The provided examples focus primarily on the `BitChoiceGroupItem` approach.

---

## Usage Examples (Using `BitChoiceGroupItem`)

**1. Basic**

*   **Description**: Demonstrates the basic setup of a `BitChoiceGroup` using a list of `BitChoiceGroupItem`. Also shows the `NoCircle` option which removes the radio button circle visually.
*   **Code**:
    ```cshtml
    <BitChoiceGroup Label="Basic Items"
                    Items="basicItems"
                    DefaultValue="basicItems[1].Value" />

    <BitChoiceGroup Label="NoCircle"
                    NoCircle
                    Items="basicItems"
                    DefaultValue="basicItems[1].Value" />
    ```
    ```csharp
    @code {
        private readonly List<BitChoiceGroupItem<string>> basicItems =
        [
            new() { Text = "Item A", Value = "A" },
            new() { Text = "Item B", Value = "B" },
            new() { Text = "Item C", Value = "C" },
            new() { Text = "Item D", Value = "D" }
        ];
    }
    ```

**2. Disabled**

*   **Description**: Shows how to disable the entire `BitChoiceGroup` using the `IsEnabled` parameter, and how to disable individual items by setting `IsEnabled = false` on the `BitChoiceGroupItem`.
*   **Code**:
    ```cshtml
    <BitChoiceGroup Label="Disabled ChoiceGroup"
                    IsEnabled="false"
                    Items="basicItems"
                    DefaultValue="@("A")" />

    <BitChoiceGroup Label="ChoiceGroup with Disabled Items"
                    Items="disabledItems"
                    DefaultValue="@("A")" />
    ```
    ```csharp
    @code {
        private readonly List<BitChoiceGroupItem<string>> basicItems =
        [
            new() { Text = "Item A", Value = "A" },
            new() { Text = "Item B", Value = "B" },
            new() { Text = "Item C", Value = "C" },
            new() { Text = "Item D", Value = "D" }
        ];

        private readonly List<BitChoiceGroupItem<string>> disabledItems =
        [
            new() { Text = "Item A", Value = "A" },
            new() { Text = "Item B", Value = "B" },
            new() { Text = "Item C", Value = "C", IsEnabled = false },
            new() { Text = "Item D", Value = "D" }
        ];
    }
    ```

**3. Images and Icons**

*   **Description**: Demonstrates using images (`ImageSrc`, `SelectedImageSrc`, `ImageSize`, `ImageAlt`) and icons (`IconName`) within choice group items. Also shows the `Inline` parameter for rendering image/icon items horizontally within the label.
*   **Code**:
    ```cshtml
    <BitChoiceGroup Label="Image Items" Items="imageItems" DefaultValue="@("Bar")" />
    <BitChoiceGroup Label="Icon Items" Items="iconItems" DefaultValue="@("Day")" />

    <BitChoiceGroup Label="Image Items" Items="inlineImageItems" DefaultValue="@("Bar")" Inline />
    <BitChoiceGroup Label="Icon Items" Items="iconItems" DefaultValue="@("Day")" Inline />
    ```
    ```csharp
    @code {
        private readonly List<BitChoiceGroupItem<string>> imageItems =
        [
            new() {
                Text = "Bar", Value = "Bar", ImageAlt = "alt for Bar image",
                ImageSize = new BitImageSize(32, 32),
                ImageSrc= "https://static2.sharepointonline.com/files/fabric/office-ui-fabric-react-assets/choicegroup-bar-unselected.png",
                SelectedImageSrc = "https://static2.sharepointonline.com/files/fabric/office-ui-fabric-react-assets/choicegroup-bar-selected.png",
            },
            new() {
                Text = "Pie", Value = "Pie", ImageAlt = "alt for Pie image",
                ImageSize = new BitImageSize(32, 32),
                ImageSrc= "https://static2.sharepointonline.com/files/fabric/office-ui-fabric-react-assets/choicegroup-pie-unselected.png",
                SelectedImageSrc = "https://static2.sharepointonline.com/files/fabric/office-ui-fabric-react-assets/choicegroup-pie-selected.png",
            }
        ];

         private readonly List<BitChoiceGroupItem<string>> inlineImageItems =
        [
             new() { /* ... similar to imageItems but with ImageSize(20, 20) ... */ },
             new() { /* ... similar to imageItems but with ImageSize(20, 20) ... */ }
        ];

        private readonly List<BitChoiceGroupItem<string>> iconItems =
        [
            new() { Text = "Day", Value = "Day", IconName = BitIconName.CalendarDay },
            new() { Text = "Week", Value = "Week", IconName = BitIconName.CalendarWeek },
            new() { Text = "Month", Value = "Month", IconName = BitIconName.Calendar, IsEnabled = false }
        ];
    }
    ```

**4. Horizontal**

*   **Description**: Shows how to render the choice group items horizontally using the `Horizontal` parameter.
*   **Code**:
    ```cshtml
    <BitChoiceGroup Label="Basic" Items="basicItems" DefaultValue="@("A")" Horizontal />
    <BitChoiceGroup Label="Disabled" Items="basicItems" IsEnabled="false" DefaultValue="@("A")" Horizontal />
    <BitChoiceGroup Label="Image" Items="imageItems" DefaultValue="@("Bar")" Horizontal />
    <BitChoiceGroup Label="Icon" Items="iconItems" DefaultValue="@("Day")" Horizontal />
    ```
    ```csharp
    // @code section defines basicItems, imageItems, iconItems as in previous examples
    ```

**5. Style & Class**

*   **Description**: Demonstrates applying custom styling using inline `Style`, root `Class`, item-level `Style`/`Class`, and the `Styles` and `Classes` parameters for fine-grained control over internal elements.
*   **Code**: (Includes CSS for context)
    ```css
    .custom-class { margin-inline: 16px; text-shadow: dodgerblue 0 0 8px; }
    .custom-item { padding: 8px; border-radius: 20px; border: 1px solid gray; }

    /* Styles for the 'Classes' parameter example */
    .custom-root { margin-inline: 16px; }
    .custom-text { font-weight: bold; }
    .custom-label-wrapper::after { /* Custom radio button inner circle */
        width: 8px; height: 8px; border: none; inset-inline-start: 6px; background-color: whitesmoke;
    }
    .custom-checked .custom-label-wrapper::after { background-color: whitesmoke; }
    .custom-label-wrapper::before { /* Custom radio button outer circle */
        background-color: whitesmoke;
    }
    .custom-checked .custom-label-wrapper::before { background-color: dodgerblue; }
    ```
    ```cshtml
    <BitChoiceGroup Label="Styled ChoiceGroup"
                    Items="basicItems" DefaultValue="basicItems[1].Value"
                    Style="margin-inline: 16px; text-shadow: red 0 0 8px;" />

    <BitChoiceGroup Label="Classed ChoiceGroup"
                    Items="basicItems" DefaultValue="basicItems[1].Value"
                    Class="custom-class" />

    <BitChoiceGroup Items="itemStyleClassItems" DefaultValue="itemStyleClassItems[1].Value" />

    <BitChoiceGroup Label="Styles"
                    Items="basicItems" DefaultValue="basicItems[1].Value"
                    Styles="@(new() { Root = "margin-inline: 16px; --item-background: #d3d3d347; --item-border: 1px solid gray;",
                                      ItemLabel = "width: 100%; cursor: pointer;",
                                      ItemChecked = "--item-background: #87cefa24; --item-border: 1px solid dodgerblue;",
                                      ItemContainer = "padding: 8px; border-radius: 2px; background-color: var(--item-background); border: var(--item-border);" })" />

    <BitChoiceGroup Label="Classes"
                    Items="basicItems" DefaultValue="basicItems[1].Value"
                    Classes="@(new() { Root = "custom-root",
                                       ItemText = "custom-text",
                                       ItemChecked = "custom-checked",
                                       ItemLabelWrapper = "custom-label-wrapper" })" />
    ```
    ```csharp
    @code {
        // ... basicItems definition ...

        private readonly List<BitChoiceGroupItem<string>> itemStyleClassItems =
        [
            new() { Text = "Item A", Value = "A", Class = "custom-item" },
            new() { Text = "Item B", Value = "B", Style = "padding: 8px; border-radius: 20px; border: 1px solid gray;" },
            new() { Text = "Item C", Value = "C", Class = "custom-item" },
            new() { Text = "Item D", Value = "D", Class = "custom-item" }
        ];
    }
    ```

**6. LabelTemplate**

*   **Description**: Shows how to provide a custom `RenderFragment` for the main label of the `BitChoiceGroup`.
*   **Code**: (Includes CSS for context)
    ```css
    .custom-label { color: red; font-size: 18px; font-weight: bold; }
    ```
    ```cshtml
    <BitChoiceGroup Items="basicItems" DefaultValue="@("A")">
        <LabelTemplate>
            <div class="custom-label">
                Custom label <BitIcon IconName="@BitIconName.Filter" />
            </div>
        </LabelTemplate>
    </BitChoiceGroup>
    ```
    ```csharp
    // @code section defines basicItems as in previous examples
    ```

**7. Binding**

*   **Description**: Demonstrates one-way (`Value` parameter) and two-way (`@bind-Value`) data binding with the `BitChoiceGroup`'s selected value.
*   **Code**:
    ```cshtml
    <BitChoiceGroup Label="One-way" Items="basicItems" Value="@oneWayValue" />
    <BitTextField @bind-Value="oneWayValue" />

    <BitChoiceGroup Label="Two-way" Items="basicItems" @bind-Value="@twoWayValue" />
    <BitTextField @bind-Value="twoWayValue" />
    ```
    ```csharp
    @code {
        private string oneWayValue = "A";
        private string twoWayValue = "A";
        // ... basicItems definition ...
    }
    ```

**8. Item Templates**

*   **Description**: Shows different ways to customize the rendering of individual items:
    *   `ItemPrefixTemplate`: Adds content before each item's label.
    *   `ItemLabelTemplate`: Customizes the entire clickable label area (excluding the radio circle).
    *   `ItemTemplate`: Replaces the *entire* item content, including the radio circle, allowing full control.
    *   `Template` property on `BitChoiceGroupItem`: Defines a template specific to *that individual item*.
*   **Code**: (Includes CSS for context)
    ```css
    .custom-container { display: flex; align-items: center; gap: 10px; cursor: pointer; }
    .custom-circle { width: 20px; height: 20px; border: 1px solid; border-radius: 10px; }
    .custom-container:hover .custom-circle { border-top: 5px solid #C66; border-bottom: 5px solid #6C6; border-left: 5px solid #66C; border-right: 5px solid #CC6; }
    .custom-container.selected { color: #C66; }
    .custom-container.selected .custom-circle { border-top: 10px solid #C66; border-bottom: 10px solid #6C6; border-left: 10px solid #66C; border-right: 10px solid #CC6; }
    ```
    ```cshtml
    <BitChoiceGroup Label="ItemPrefixTemplate" Items="basicItems" DefaultValue="@string.Empty">
        <ItemPrefixTemplate Context="item">
            @(item.Index + 1).&nbsp;
        </ItemPrefixTemplate>
    </BitChoiceGroup>

    <BitChoiceGroup Label="ItemLabelTemplate" Items="itemTemplateItems" @bind-Value="itemLabelTemplateValue">
        <ItemLabelTemplate Context="item">
            <div class="custom-container @(itemLabelTemplateValue == item.Value ? "selected" : string.Empty)">
                <BitIcon IconName="@item.IconName" />
                <span>@item.Text</span>
            </div>
        </ItemLabelTemplate>
    </BitChoiceGroup>

    <BitChoiceGroup Label="ItemTemplate" Items="itemTemplateItems" @bind-Value="itemTemplateValue">
        <ItemTemplate Context="item">
            <div class="custom-container @(itemTemplateValue == item.Value ? "selected" : string.Empty)">
                <div class="custom-circle"></div>
                <span>@item.Text</span>
            </div>
        </ItemTemplate>
    </BitChoiceGroup>

    <BitChoiceGroup Label="Item's Template" Items="itemTemplateItems2" @bind-Value="itemTemplateValue2" />
    ```
    ```csharp
    @code {
        private string itemTemplateValue = "Day";
        private string itemTemplateValue2 = "Day";
        private string itemLabelTemplateValue = "Day";
        // ... basicItems definition ...
        // ... itemTemplateItems definition (with IconName) ...

        private List<BitChoiceGroupItem<string>> itemTemplateItems2 = default!;
        protected override void OnInitialized() {
            itemTemplateItems2 = new() {
                new() { Text = "Day", Value = "Day", Template = (item => @<div class="custom-container @(itemTemplateValue2 == item.Value ? "selected" : "")">...</div>) },
                new() { Text = "Week", Value = "Week", Template = (item => @<div class="custom-container @(itemTemplateValue2 == item.Value ? "selected" : "")">...</div>) },
                new() { Text = "Month", Value = "Month", Template = (item => @<div class="custom-container @(itemTemplateValue2 == item.Value ? "selected" : "")">...</div>) }
            };
        }
    }
    ```

**9. RTL**

*   **Description**: Demonstrates rendering the `BitChoiceGroup` in a right-to-left layout using `Dir="BitDir.Rtl"`.
*   **Code**:
    ```cshtml
    <BitChoiceGroup Label="ساده" Items="rtlItems" DefaultValue="@("A")" Dir="BitDir.Rtl" />
    <BitChoiceGroup Label="غیرفعال" Items="rtlItems" IsEnabled="false" DefaultValue="@("A")" Dir="BitDir.Rtl" />
    ```
    ```csharp
    @code {
        private readonly List<BitChoiceGroupItem<string>> rtlItems = new()
        {
            new() { Text = "بخش آ", Value = "A" },
            new() { Text = "بخش ب", Value = "B" },
            new() { Text = "بخش پ", Value = "C" },
            new() { Text = "بخش ت", Value = "D" }
        };
    }
    ```

**10. Validation**

*   **Description**: Shows using `BitChoiceGroup` within an `EditForm` and validating the selection using data annotations (`[Required]`).
*   **Code**:
    ```cshtml
    <style> .validation-message { color: red; } </style>

    <EditForm Model="@validationModel" OnValidSubmit="@HandleValidSubmit" OnInvalidSubmit="@HandleInvalidSubmit">
        <DataAnnotationsValidator />

        <BitChoiceGroup Items="basicItems" @bind-Value="validationModel.Value" />
        <ValidationMessage For="@(() => validationModel.Value)" />

        <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
    </EditForm>
    ```
    ```csharp
    @code {
        public class ChoiceGroupValidationModel
        {
            [Required(ErrorMessage = "Pick one")]
            public string Value { get; set; }
        }

        public ChoiceGroupValidationModel validationModel = new();

        private void HandleValidSubmit() { }
        private void HandleInvalidSubmit() { }
        // ... basicItems definition ...
    }
    ```

---

## API Reference

**BitChoiceGroup Parameters**

| Name                | Type                                          | Default                    | Description                                                                    |
| :------------------ | :-------------------------------------------- | :------------------------- | :----------------------------------------------------------------------------- |
| `AriaLabelledBy`    | `string?`                                     | `null`                     | ID of an element that labels the ChoiceGroup for accessibility.              |
| `ChildContent`      | `RenderFragment?`                             | `null`                     | Content consisting of `BitChoiceGroupOption` components.                       |
| `Classes`           | `BitChoiceGroupClassStyles?`                  | `null`                     | Custom CSS classes for different parts.                                        |
| `DefaultValue`      | `TValue?`                                     | `default`                  | Default selected value (uncontrolled).                                         |
| `Inline`            | `bool`                                        | `false`                    | Renders item image/icon on the same line as the item text.                     |
| `Horizontal`        | `bool`                                        | `false`                    | Renders items horizontally instead of vertically.                              |
| `Items`             | `IEnumerable<TItem>`                          | `new List<TItem>()`        | Data source for items (`BitChoiceGroupItem` or custom type).                 |
| `ItemLabelTemplate` | `RenderFragment<TItem>?`                      |                            | Custom template for the item's label content (excludes the radio button).      |
| `ItemPrefixTemplate`| `RenderFragment<TItem>?`                      |                            | Custom template rendered before each item's content.                         |
| `ItemTemplate`      | `RenderFragment<TItem>?`                      | `null`                     | Custom template for rendering the entire item content (replaces default).      |
| `Label`             | `string?`                                     | `null`                     | Descriptive label for the ChoiceGroup.                                         |
| `LabelTemplate`     | `RenderFragment?`                             | `null`                     | Custom template for the ChoiceGroup's main label.                              |
| `Name`              | `string`                                      | `Guid.NewGuid().ToString()`| HTML `name` attribute used to group radio buttons.                             |
| `NameSelectors`     | `BitChoiceGroupNameSelectors<TItem, TValue>?` | `null`                     | Specifies property names/selectors when using a custom item type (`TItem`).    |
| `NoCircle`          | `bool`                                        | `false`                    | If true, hides the visual radio button circle.                                 |
| `OnClick`           | `EventCallback<MouseEventArgs>`               |                            | Callback for when an option is clicked.                                      |
| `Options`           | `RenderFragment?`                             | `null`                     | Alias for `ChildContent`.                                                      |
| `Styles`            | `BitChoiceGroupClassStyles?`                  | `null`                     | Custom CSS styles for different parts.                                         |
| *(Inherited)*       | *(See BitInputBase)*                          |                            |                                                                                |

**BitInputBase Parameters (Inherited)**

| Name                | Type                              | Default              | Description                                                                    |
| :------------------ | :-------------------------------- | :------------------- | :----------------------------------------------------------------------------- |
| `DisplayName`       | `string?`                         | `null`               | Display name for validation messages.                                          |
| `InputHtmlAttributes`| `IReadOnlyDictionary<string, object>?`| `null`               | Additional attributes applied to internal input elements (where applicable). |
| `Name`              | `string?`                         | `null`               | Logical name used for form association (overridden by `BitChoiceGroup.Name`).|
| `NoValidate`        | `bool`                            | `false`              | Disables validation.                                                           |
| `OnChange`          | `EventCallback<TValue?>`          |                      | Callback when the bound `Value` changes.                                       |
| `ReadOnly`          | `bool`                            | `false`              | Makes the input read-only (visual effect).                                     |
| `Required`          | `bool`                            | `false`              | Marks the input as required (visual cue, use validation attributes).         |
| `Value`             | `TValue?`                         | `default`            | The currently selected value (use `@bind-Value`).                            |
| *(Inherited)*       | *(See BitComponentBase)*          |                      |                                                                                |

**BitComponentBase Parameters (Inherited)**

| Name           | Type                         | Default                   | Description                                                           |
| :------------- | :--------------------------- | :------------------------ | :-------------------------------------------------------------------- |
| `AriaLabel`    | `string?`                    | `null`                    | Aria-label for accessibility (applied to the group).                  |
| `Class`        | `string?`                    | `null`                    | Custom CSS class for the root element.                                |
| `Dir`          | `BitDir?`                    | `null`                    | Component direction (`Ltr`, `Rtl`, `Auto`).                           |
| `HtmlAttributes`| `Dictionary<string, object>` | `new Dictionary<>()`      | Additional HTML attributes for the root element.                        |
| `Id`           | `string?`                    | `null`                    | Custom ID for the root element (defaults to `UniqueId`).              |
| `IsEnabled`    | `bool`                       | `true`                    | Whether the entire component is enabled.                              |
| `Style`        | `string?`                    | `null`                    | Custom CSS style for the root element.                                |
| `Visibility`   | `BitVisibility`              | `BitVisibility.Visible`   | Component visibility (`Visible`, `Hidden`, `Collapsed`).              |

**BitComponentBase Public Members (Inherited)**

| Name        | Type               | Default          | Description                                       |
| :---------- | :----------------- | :--------------- | :------------------------------------------------ |
| `UniqueId`  | `Guid`             | `Guid.NewGuid()` | Readonly unique ID assigned at construction.      |
| `RootElement` | `ElementReference` |                  | `ElementReference` for the root DOM element.    |

**BitChoiceGroupItem Properties (for `Items` parameter)**

| Name               | Type                                        | Default | Description                                                         |
| :----------------- | :------------------------------------------ | :------ | :------------------------------------------------------------------ |
| `AriaLabel`        | `string?`                                   | `null`  | AriaLabel for the item's input.                                   |
| `Class`            | `string?`                                   | `null`  | Custom CSS class for the item container.                            |
| `Id`               | `string?`                                   | `null`  | Custom ID for the item's input element.                           |
| `IsEnabled`        | `bool`                                      | `true`  | Whether the individual item is enabled.                             |
| `IconName`         | `string?`                                   | `null`  | Icon name to display next to the item text.                       |
| `ImageSrc`         | `string?`                                   | `null`  | URL of the image to display for the item.                         |
| `ImageAlt`         | `string?`                                   | `null`  | `alt` text for the item's image.                                  |
| `ImageSize`        | `BitImageSize?`                             | `null`  | Specifies width and height for the item's image.                  |
| `Prefix`           | `string?`                                   | `null`  | Text to render before the item label.                             |
| `SelectedImageSrc` | `string?`                                   | `null`  | URL of the image to display when the item is selected.            |
| `Style`            | `string?`                                   | `null`  | Custom inline style for the item container.                         |
| `Template`         | `RenderFragment<BitChoiceGroupItem<TValue>>?` | `null`  | Custom template to render the entire content of this specific item. |
| `Text`             | `string?`                                   | `null`  | Text displayed for the item.                                      |
| `Value`            | `TValue?`                                   | `default` | The value associated with this item.                              |
| `Index`            | `int`                                       |         | *(Readonly)* Index assigned by the component during rendering.    |
| `IsSelected`       | `bool`                                      | `false` | *(Readonly)* Indicates if the item is currently selected.           |

**BitChoiceGroupOption Properties (for `ChildContent`/`Options`)**

*(Functionally similar to `BitChoiceGroupItem` but defined declaratively as components)*

| Name               | Type                                  | Default | Description                                                       |
| :----------------- | :------------------------------------ | :------ | :---------------------------------------------------------------- |
| `AriaLabel`        | `string?`                             | `null`  | AriaLabel for the option's input.                               |
| `Class`            | `string?`                             | `null`  | Custom CSS class for the option container.                        |
| `Id`               | `string?`                             | `null`  | Custom ID for the option's input element.                         |
| `IsEnabled`        | `bool`                                | `true`  | Whether the individual option is enabled.                         |
| `IconName`         | `string?`                             | `null`  | Icon name to display next to the option text.                     |
| `ImageSrc`         | `string?`                             | `null`  | URL of the image to display for the option.                       |
| `ImageAlt`         | `string?`                             | `null`  | `alt` text for the option's image.                              |
| `ImageSize`        | `BitImageSize?`                       | `null`  | Specifies width and height for the option's image.                |
| `Prefix`           | `string?`                             | `null`  | Text to render before the option label.                           |
| `SelectedImageSrc` | `string?`                             | `null`  | URL of the image to display when the option is selected.          |
| `Style`            | `string?`                             | `null`  | Custom inline style for the option container.                     |
| `Template`         | `RenderFragment<BitChoiceGroupOption>?` | `null`  | Custom template to render the entire content of this specific option. |
| `Text`             | `string?`                             | `null`  | Text displayed for the option.                                    |
| `Value`            | `TValue?`                             | `default` | The value associated with this option.                            |
| `Index`            | `int`                                 |         | *(Readonly)* Index assigned by the component during rendering.    |
| `IsSelected`       | `bool`                                | `false` | *(Readonly)* Indicates if the option is currently selected.       |

**BitChoiceGroupNameSelectors Properties (for `NameSelectors` parameter)**

| Name               | Type                                          | Default                                              | Description                                                         |
| :----------------- | :-------------------------------------------- | :--------------------------------------------------- | :------------------------------------------------------------------ |
| `AriaLabel`        | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.AriaLabel))`    | Selector for the `AriaLabel` property of the custom item type.      |
| `Class`            | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.Class))`        | Selector for the `Class` property of the custom item type.          |
| `Id`               | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.Id))`           | Selector for the `Id` property of the custom item type.             |
| `IsEnabled`        | `BitNameSelectorPair<TItem, bool>`            | `new(nameof(BitChoiceGroupItem<TValue>.IsEnabled))`    | Selector for the `IsEnabled` property of the custom item type.      |
| `IconName`         | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.IconName))`     | Selector for the `IconName` property of the custom item type.       |
| `ImageSrc`         | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.ImageSrc))`     | Selector for the `ImageSrc` property of the custom item type.       |
| `ImageAlt`         | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.ImageAlt))`     | Selector for the `ImageAlt` property of the custom item type.       |
| `ImageSize`        | `BitNameSelectorPair<TItem, BitImageSize?>`   | `new(nameof(BitChoiceGroupItem<TValue>.ImageSize))`    | Selector for the `ImageSize` property of the custom item type.      |
| `SelectedImageSrc` | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.SelectedImageSrc))`| Selector for the `SelectedImageSrc` property of the custom item type.|
| `Style`            | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.Style))`        | Selector for the `Style` property of the custom item type.          |
| `Template`         | `BitNameSelectorPair<TItem, RenderFragment<TItem>?>`| `new(nameof(BitChoiceGroupItem<TValue>.Template))`   | Selector for the `Template` property of the custom item type.       |
| `Text`             | `BitNameSelectorPair<TItem, string?>`         | `new(nameof(BitChoiceGroupItem<TValue>.Text))`         | Selector for the `Text` property of the custom item type.           |
| `Value`            | `BitNameSelectorPair<TItem, TValue?>`         | `new(nameof(BitChoiceGroupItem<TValue>.Value))`        | Selector for the `Value` property of the custom item type.          |
| `Index`            | `string`                                      | `nameof(BitChoiceGroupItem<TValue>.Index)`             | Name of the `Index` property (for reflection, value set by component).|
| `IsSelected`       | `string`                                      | `nameof(BitChoiceGroupItem<TValue>.IsSelected)`        | Name of the `IsSelected` property (for reflection, value set by component).|

**BitChoiceGroupClassStyles Properties (for `Classes`/`Styles`)**

| Name               | Type      | Default | Description                                                            |
| :----------------- | :-------- | :------ | :--------------------------------------------------------------------- |
| `Root`             | `string?` | `null`  | CSS class/style for the root `div` element.                            |
| `LabelContainer`   | `string?` | `null`  | CSS class/style for the container holding the main label.              |
| `Label`            | `string?` | `null`  | CSS class/style for the main label element.                            |
| `Container`        | `string?` | `null`  | CSS class/style for the container holding all the choice items.        |
| `ItemChecked`      | `string?` | `null`  | CSS class/style applied to the container of the *checked* item.        |
| `ItemContainer`    | `string?` | `null`  | CSS class/style for the container (`div`) of *each* individual item.   |
| `ItemLabel`        | `string?` | `null`  | CSS class/style for the `label` element of each item.                  |
| `ItemLabelWrapper` | `string?` | `null`  | CSS class/style for the inner wrapper `div` inside the item's label. |
| `ItemImageContainer`| `string?` | `null`  | CSS class/style for the container holding the item's image/icon.       |
| `ItemImageWrapper` | `string?` | `null`  | CSS class/style for the wrapper around the item's image/icon.        |
| `ItemImageDiv`     | `string?` | `null`  | CSS class/style for the `div` containing the item's image.             |
| `ItemImage`        | `string?` | `null`  | CSS class/style for the `img` element of the item.                     |
| `ItemIconContainer`| `string?` | `null`  | CSS class/style for the container holding the item's icon.             |
| `ItemIconWrapper`  | `string?` | `null`  | CSS class/style for the wrapper around the item's icon.                |
| `ItemIcon`         | `string?` | `null`  | CSS class/style for the `i` (icon) element of the item.                |
| `ItemPrefix`       | `string?` | `null`  | CSS class/style for the prefix element of the item.                    |
| `ItemTextWrapper`  | `string?` | `null`  | CSS class/style for the wrapper around the item's text.                |
| `ItemText`         | `string?` | `null`  | CSS class/style for the `span` containing the item's text.             |

**Enums**

*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/ChoiceGroup/BitChoiceGroupDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/ChoiceGroup/BitChoiceGroupDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/ChoiceGroup/BitChoiceGroup.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/ChoiceGroup/BitChoiceGroup.razor)

