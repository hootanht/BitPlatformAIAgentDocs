# BitDropdown Blazor Component

**Objective:** This document provides context and reference information about the `BitDropdown` Blazor component, based *solely* on the provided HTML documentation extract. Use this information to understand the component's features, generate relevant code snippets, and explain its usage.

**Key Component:** `BitDropdown`
**Aliases:** `Select`, `MultiSelect`, `ComboBox`

---

## Overview

`BitDropdown` is a component that presents a list where the selected item is always visible, and other items become visible on demand by clicking a button. It's commonly used within forms for selecting options.

---

## Notes

*   **Multi-API Component:** The `BitDropdown` can be populated with items in three different ways:
    1.  Using a list of `BitDropdownItem<TValue>` objects passed to the `Items` parameter.
    2.  Using a list of custom generic objects (`TItem`) passed to the `Items` parameter, along with `NameSelectors` to map properties.
    3.  Using `BitDropdownOption` components nested within the `BitDropdown` (`ChildContent`/`Options`).
*   The provided examples focus primarily on the `BitDropdownItem` approach.

---

## Introduction Video

*(A video demonstrating the component is available in the original source but cannot be embedded here.)*
Music Credit: Music Cocktails by AlexGuz.

---

## Usage Examples (Using `BitDropdownItem`)

**1. Basic**

*   **Description**: Shows basic single-select and multi-select dropdowns, a required dropdown, a dropdown preserving callout width, and a disabled dropdown. Items include headers and dividers.
*   **Code**:
    ```cshtml
    <BitDropdown Label="Single select"
                 Items="GetBasicItems()"
                 Placeholder="Select an item"
                 TItem="BitDropdownItem<string>" TValue="string" />

    <BitDropdown Label="Multi select"
                 MultiSelect
                 DefaultValue="@("")"
                 Items="GetBasicItems()"
                 Placeholder="Select items" />

    <BitDropdown Label="Required" Required
                 Items="GetBasicItems()"
                 DefaultValue="@string.Empty"
                 Placeholder="Select an item" />

    <BitDropdown Label="PreserveCalloutWidth"
                 PreserveCalloutWidth
                 Items="GetBasicItems()"
                 DefaultValue="@string.Empty"
                 Placeholder="Select an item" />

    <BitDropdown Label="Disabled"
                 IsEnabled="false"
                 Items="GetBasicItems()"
                 DefaultValue="@("f-ora")"
                 Placeholder="Select an item" />
    ```
    ```csharp
    @code {
        private List<BitDropdownItem<string>> GetBasicItems() => new()
        {
            new() { ItemType = BitDropdownItemType.Header, Text = "Fruits" },
            new() { Text = "Apple", Value = "f-app" },
            new() { Text = "Banana", Value = "f-ban" },
            new() { Text = "Orange", Value = "f-ora", IsEnabled = false },
            new() { Text = "Grape", Value = "f-gra" },
            new() { ItemType = BitDropdownItemType.Divider },
            new() { ItemType = BitDropdownItemType.Header, Text = "Vegetables" },
            new() { Text = "Broccoli", Value = "v-bro" },
            new() { Text = "Carrot", Value = "v-car" },
            new() { Text = "Lettuce", Value = "v-let" }
        };
    }
    ```

**2. Prefix & Suffix**

*   **Description**: Demonstrates adding text prefixes and suffixes to the dropdown input display.
*   **Code**:
    ```cshtml
    <BitDropdown Label="Prefix"
                 Prefix="Fruits:"
                 Items="GetBasicItems()"
                 Placeholder="Select an item"
                 TItem="BitDropdownItem<string>" TValue="string" />

    <BitDropdown Label="Suffix"
                 Suffix="kg"
                 Items="GetBasicItems()"
                 Placeholder="Select an item"
                 TItem="BitDropdownItem<string>" TValue="string" />

    <BitDropdown Label="Prefix and Suffix"
                 Prefix="Fruits:"
                 Suffix="kg"
                 Items="GetBasicItems()"
                 Placeholder="Select an item"
                 TItem="BitDropdownItem<string>" TValue="string" />

    <BitDropdown Label="Disabled"
                 Prefix="Fruits:" Suffix="kg"
                 Items="GetBasicItems()" Placeholder="Select an item"
                 TItem="BitDropdownItem<string>" TValue="string"
                 IsEnabled="false" />
    ```
    ```csharp
    // @code uses GetBasicItems() from the Basic example
    ```

**3. FitWidth**

*   **Description**: Shows the `FitWidth` parameter, which adjusts the dropdown's width to fit its content.
*   **Code**:
    ```cshtml
    <BitDropdown Label="Single select"
                 FitWidth
                 Items="GetBasicItems()"
                 DefaultValue="@string.Empty"
                 Placeholder="Select an item" />

    <BitDropdown Label="Multi select"
                 FitWidth
                 MultiSelect
                 Items="GetBasicItems()"
                 Placeholder="Select items"
                 DefaultValue="@string.Empty" />
    ```
    ```csharp
    // @code uses GetBasicItems() from the Basic example
    ```

**4. NoBorder**

*   **Description**: Demonstrates the `NoBorder` parameter, which removes the border from the dropdown's root element.
*   **Code**:
    ```cshtml
    <BitDropdown NoBorder
                 Items="GetBasicItems()"
                 DefaultValue="@string.Empty"
                 Placeholder="Select an item" />

    <BitDropdown NoBorder MultiSelect
                 Items="GetBasicItems()"
                 Placeholder="Select items"
                 DefaultValue="@string.Empty" />
    ```
    ```csharp
    // @code uses GetBasicItems() from the Basic example
    ```

**5. Responsive**

*   **Description**: Shows the `Responsive` parameter. When true, the dropdown callout renders as a side panel on smaller screens.
*   **Code**:
    ```cshtml
    <BitDropdown Label="Responsive Dropdown"
                 Responsive
                 Items="GetBasicItems()"
                 DefaultValue="@string.Empty"
                 Placeholder="Select an item" />
    ```
    ```csharp
    // @code uses GetBasicItems() from the Basic example
    ```

**6. Drop direction**

*   **Description**: Uses the `DropDirection` parameter to control the preferred opening direction of the callout (`All`, `TopAndBottom`).
*   **Code**:
    ```cshtml
    <BitDropdown Label="All"
                 Items="dropDirectionItems"
                 DefaultValue="@string.Empty"
                 Placeholder="Select an item"
                 DropDirection="BitDropDirection.All" />

    <BitDropdown Label="TopAndBottom"
                 Items="dropDirectionItems"
                 DefaultValue="@string.Empty"
                 Placeholder="Select an item"
                 DropDirection="BitDropDirection.TopAndBottom" />
    ```
    ```csharp
    @code {
        private ICollection<BitDropdownItem<string>>? dropDirectionItems;

        protected override void OnInitialized()
        {
            dropDirectionItems = Enumerable.Range(1, 15)
                                           .Select(c => new BitDropdownItem<string> { Value = c.ToString(), Text = $"Category {c}" })
                                           .ToArray();
        }
    }
    ```

**7. Clear button**

*   **Description**: Demonstrates the `ShowClearButton` parameter, which adds a button to clear the current selection(s).
*   **Code**:
    ```cshtml
    <BitDropdown @bind-Value="clearValue"
                 ShowClearButton
                 Items="GetBasicItems()"
                 Label="Single select dropdown"
                 Placeholder="Select an option" />
    <div>Value: @clearValue</div>

    <BitDropdown @bind-Values="clearValues"
                 MultiSelect ShowClearButton
                 Items="GetBasicItems()"
                 Placeholder="Select options"
                 Label="Multi select dropdown" />
    <div>Values: @string.Join(',', clearValues)</div>
    ```
    ```csharp
    @code {
        private string? clearValue = "f-app";
        private ICollection<string?> clearValues = new[] { "f-app", "f-ban" };
        // ... GetBasicItems() definition ...
    }
    ```

**8. SearchBox**

*   **Description**: Shows how to enable an inline search box within the dropdown callout using `ShowSearchBox`. `AutoFocusSearchBox` focuses the search input automatically. `SearchBoxPlaceholder` sets the placeholder text. `SearchFunction` allows providing a custom filtering logic.
*   **Code**:
    ```cshtml
    <BitDropdown Label="Single select & auto focus"
                 ShowSearchBox AutoFocusSearchBox
                 Items="GetBasicItems()" DefaultValue="@string.Empty"
                 Placeholder="Select an item" SearchBoxPlaceholder="Search item" />

    <BitDropdown Label="Multi select"
                 MultiSelect ShowSearchBox
                 Items="GetBasicItems()" Placeholder="Select items"
                 DefaultValue="@string.Empty" SearchBoxPlaceholder="Search items" />

    <BitDropdown Label="Single select & auto focus"
                 ShowSearchBox AutoFocusSearchBox
                 Items="GetBasicItems()" DefaultValue="@string.Empty"
                 Placeholder="Select an item" SearchBoxPlaceholder="Search item"
                 SearchFunction="(items, text) => items.Where(i => i.Text?.StartsWith(text, StringComparison.OrdinalIgnoreCase) ?? false).ToArray()" />

    <BitDropdown Label="Multi select"
                 MultiSelect ShowSearchBox
                 Items="GetBasicItems()" Placeholder="Select items"
                 DefaultValue="@string.Empty" SearchBoxPlaceholder="Search items"
                 SearchFunction="(items, text) => items.Where(i => i.Text?.EndsWith(text, StringComparison.OrdinalIgnoreCase) ?? false).ToArray()" />
    ```
    ```csharp
    // @code uses GetBasicItems() from the Basic example
    ```

**9. Validation**

*   **Description**: Demonstrates using `BitDropdown` within an `EditForm` for validation. Examples include making a single selection required (`[Required]`) and enforcing min/max selections in multi-select mode (`[MinLength]`, `[MaxLength]` on the bound collection).
*   **Code**: (Includes CSS for context)
    ```css
    .validation-message { color: #A4262C; font-size: 0.75rem; }
    ```
    ```cshtml
    @using System.ComponentModel.DataAnnotations;

    <EditForm Model="validationModel" OnValidSubmit="HandleValidSubmit" OnInvalidSubmit="HandleInvalidSubmit">
        <DataAnnotationsValidator />

        <BitDropdown @bind-Value="validationModel.Category"
                     Label="Select 1 item"
                     Items="GetBasicItems()"
                     Placeholder="Select an item" />
        <ValidationMessage For="@(() => validationModel.Category)" />

        <BitDropdown @bind-Values="validationModel.Products"
                     MultiSelect Items="GetBasicItems()"
                     Placeholder="Select items"
                     Label="Select min 1 and max 2 items" />
        <ValidationMessage For="@(() => validationModel.Products)" />

        <BitButton ButtonType="BitButtonType.Submit">Submit</BitButton>
    </EditForm>
    ```
    ```csharp
    @code {
        public class FormValidationDropdownModel
        {
            [MaxLength(2, ErrorMessage = "The property {0} have more than {1} elements")]
            [MinLength(1, ErrorMessage = "The property {0} doesn't have at least {1} elements")]
            public ICollection<string?> Products { get; set; } = new List<string?>();

            [Required]
            public string Category { get; set; }
        }

        private FormValidationDropdownModel validationModel = new();

        private async Task HandleValidSubmit() { }
        private void HandleInvalidSubmit() { }
        // ... GetBasicItems() definition ...
    }
    ```

**10. Customization (Templates)**

*   **Description**: Shows various templating options: `HeaderTemplate`, `TextTemplate`, `ItemTemplate`, `PlaceholderTemplate`, `LabelTemplate`. Also demonstrates customizing the caret icon using `CaretDownIconName` and adding header/footer to the callout using `CalloutHeaderTemplate` and `CalloutFooterTemplate`.
*   **Code**: (Includes CSS and C# class for context)
    ```css
    /* CSS for custom templates */
    .custom-drp { gap: 10px; display: flex; align-items: center; flex-flow: row nowrap; justify-content: flex-start; }
    .custom-drp.custom-drp-lbl { color: dodgerblue; }
    .custom-drp.custom-drp-txt { color: goldenrod; }
    .custom-drp.custom-drp-ph { color: orangered; }
    .custom-drp.custom-drp-item { width: 100%; cursor: pointer; }
    .custom-drp.custom-drp-header { width: 100%; padding: 5px 12px; color: #ff4600; font-weight: bold; }
    ```
    ```csharp
    @code {
        public class DropdownItemData { public string? IconName { get; set; } }

        private List<BitDropdownItem<string>> GetDataItems() => new() { /* ... items with Data = new DropdownItemData { IconName = "..." } ... */ };
        // ... GetBasicItems() definition ...
    }
    ```
    ```cshtml
    <BitDropdown Label="Header template" Items="GetDataItems()" Placeholder="Select an item">
        <HeaderTemplate Context="item">
            <div class="custom-drp custom-drp-header">
                <BitIcon IconName="@((item.Data as DropdownItemData)?.IconName)" />
                <div>@item.Text</div>
            </div>
        </HeaderTemplate>
    </BitDropdown>

    <BitDropdown Label="Text & Item templates" Items="GetDataItems()" Placeholder="Select an item">
        <TextTemplate Context="dropdown">
            <div class="custom-drp custom-drp-txt">
                <BitIcon IconName="@((dropdown.SelectedItem?.Data as DropdownItemData)?.IconName)" />
                <div>@dropdown.SelectedItem?.Text</div>
            </div>
        </TextTemplate>
        <ItemTemplate Context="item">
            <div class="custom-drp custom-drp-item">
                <BitIcon IconName="@((item.Data as DropdownItemData)?.IconName)" />
                <div Style="text-decoration:underline">@item.Text</div>
            </div>
        </ItemTemplate>
    </BitDropdown>

    <BitDropdown Label="Placeholder template" Items="GetDataItems()" Placeholder="Select an item">
        <PlaceholderTemplate Context="dropdown">
            <div class="custom-drp custom-drp-ph">
                <BitIcon IconName="@BitIconName.MessageFill" />
                <div>@dropdown.Placeholder</div>
            </div>
        </PlaceholderTemplate>
    </BitDropdown>

    <BitDropdown Label="Label template" Items="GetDataItems()" Placeholder="Select an item">
        <LabelTemplate>
            <div class="custom-drp custom-drp-lbl">
                <div>Custom label</div>
                <BitIcon IconName="@BitIconName.Info" AriaLabel="Info" />
            </div>
        </LabelTemplate>
    </BitDropdown>

    <BitDropdown Label="CaretDownIconName" Items="GetDataItems()" Placeholder="Select an item"
                 CaretDownIconName="@BitIconName.ScrollUpDown" />

    <BitDropdown Label="Callout templates" Items="GetBasicItems()" Placeholder="Select an item">
        <CalloutHeaderTemplate>
             <div Style="padding:0.5rem;border-bottom:1px solid #555">Best in the world</div>
        </CalloutHeaderTemplate>
        <CalloutFooterTemplate>
            <BitActionButton IconName="@BitIconName.Add">New Item</BitActionButton>
        </CalloutFooterTemplate>
    </BitDropdown>
    ```

**11. Binding (Revisited)**

*   **Description**: Provides additional examples of `@bind-Value` (single select), `@bind-Values` (multi-select), `OnChange` (single select value change), `OnValuesChange` (multi-select values change), and `OnSelectItem` (triggered when any item is clicked, providing the full item object).
*   **Code**:
    ```cshtml
    <BitDropdown @bind-Value="controlledValue" Label="Single select" Items="GetBasicItems()" Placeholder="Select an item" />
    <div>Selected Value: @controlledValue</div>

    <BitDropdown @bind-Values="controlledValues" MultiSelect Label="Multi select" Items="GetBasicItems()" Placeholder="Select items" />
    <div>Selected Values: @string.Join(",", controlledValues)</div>

    <BitDropdown Label="Single select" Items="GetBasicItems()" Placeholder="Select an item"
                 TItem="BitDropdownItem<string>" TValue="string"
                 OnChange="(string value) => changedValue = value" />
    <div>Changed Value: @changedValue</div>

    <BitDropdown Label="Multi select" MultiSelect Items="GetBasicItems()" Placeholder="Select items"
                 TItem="BitDropdownItem<string>" TValue="string"
                 OnValuesChange="(IEnumerable<string> values) => changedValues = values" />
    <div>Changed Values: @string.Join(",", changedValues)</div>

    <BitDropdown Label="Single select" Items="GetBasicItems()" Placeholder="Select an item"
                 OnSelectItem="(BitDropdownItem<string> item) => selectedItem1 = item" />
    <div>Selected Value: @selectedItem1?.Value</div>

    <BitDropdown Label="Multi select" MultiSelect Items="GetBasicItems()" Placeholder="Select items"
                 DefaultValue="@string.Empty"
                 OnSelectItem="(BitDropdownItem<string> item) => selectedItem2 = item" />
    <div>Selected Value: @selectedItem2?.Value</div>
    ```
    ```csharp
    @code {
        private string controlledValue = "f-app";
        private IEnumerable<string?> controlledValues = ["f-app", "f-ban"];
        private string? changedValue;
        private IEnumerable<string?> changedValues = [];
        private BitDropdownItem<string>? selectedItem1;
        private BitDropdownItem<string>? selectedItem2;
        // ... GetBasicItems() definition ...
    }
    ```

**12. Virtualization**

*   **Description**: Demonstrates using `Virtualize` with either a large `Items` collection or an `ItemsProvider` delegate (`LoadItems` in the example) to efficiently render large lists. `InitialSelectedItems` can pre-select items when using `ItemsProvider`.
*   **Code**:
    ```cshtml
    <BitDropdown Label="Single select" Virtualize Items="virtualizeItems1" DefaultValue="@string.Empty" Placeholder="Select an item" />
    <BitDropdown Label="Multi select" Virtualize MultiSelect Items="virtualizeItems2" Placeholder="Select items" DefaultValue="@string.Empty" />

    <BitDropdown Label="Single select" Virtualize ItemsProvider="LoadItems" Placeholder="Select an item"
                 TItem="BitDropdownItem<string>" TValue="string" />
    <BitDropdown Label="Multi select" Virtualize MultiSelect ItemsProvider="LoadItems" Placeholder="Select items"
                 TItem="BitDropdownItem<string>" TValue="string" />

    <BitDropdown Label="Single select" Virtualize ItemsProvider="LoadItems" Placeholder="Select an item"
                 InitialSelectedItems="initialSelectedItem" TItem="BitDropdownItem<string>" TValue="string" />
    <BitDropdown Label="Multi select" Virtualize MultiSelect ItemsProvider="LoadItems" Placeholder="Select items"
                 InitialSelectedItems="initialSelectedItems" TItem="BitDropdownItem<string>" TValue="string" />
    ```
    ```csharp
    @code {
        private ICollection<BitDropdownItem<string>>? virtualizeItems1;
        private ICollection<BitDropdownItem<string>>? virtualizeItems2;
        private IEnumerable<BitDropdownItem<string>> initialSelectedItem = [ /* ... single item ... */ ];
        private IEnumerable<BitDropdownItem<string>> initialSelectedItems = [ /* ... multiple items ... */ ];

        protected override void OnInitialized() {
            virtualizeItems1 = Enumerable.Range(1, 10_000).Select(c => new BitDropdownItem<string> { Text = $"Category {c}", Value = c.ToString() }).ToArray();
            virtualizeItems2 = Enumerable.Range(1, 10_000).Select(c => new BitDropdownItem<string> { Text = $"Category {c}", Value = c.ToString() }).ToArray();
        }

        private async ValueTask<BitDropdownItemsProviderResult<BitDropdownItem<string>>> LoadItems(BitDropdownItemsProviderRequest<BitDropdownItem<string>> request) {
            // Example logic to fetch data based on request.StartIndex, request.Count, request.Search
            // Replace with actual data fetching (e.g., HTTP call)
            try {
                // ... (Simulated data fetching logic) ...
                var items = new List<BitDropdownItem<string>>(); // Populate this list based on request
                var totalItemCount = 1000; // Example total count
                return BitDropdownItemsProviderResult.From(items, totalItemCount);
            } catch {
                return BitDropdownItemsProviderResult.From(new List<BitDropdownItem<string>>(), 0);
            }
        }
    }
    ```

**13. ComboBox**

*   **Description**: Enables ComboBox behavior using the `Combo` parameter, allowing users to type directly into the dropdown input to filter or select items. Works with both single and multi-select.
*   **Code**:
    ```cshtml
    <BitDropdown @bind-Value="comboBoxValueSample1"
                 Combo Items="comboBoxItems" Placeholder="Select an option"
                 Label="Single select combo box" />
    <div>Value: @comboBoxValueSample1</div>

    <BitDropdown @bind-Values="comboBoxValues1"
                 Combo MultiSelect Items="comboBoxItems" Placeholder="Select an option"
                 Label="Multi select combo box" />
    <div>Values: @string.Join(',', comboBoxValues1)</div>
    ```
    ```csharp
    @code {
        private string comboBoxValueSample1 = default!;
        private ICollection<string?> comboBoxValues1 = [];
        // ... comboBoxItems definition (same as basicItems) ...
    }
    ```

**14. Chips**

*   **Description**: Used in conjunction with `Combo` (and typically `MultiSelect`), the `Chips` parameter displays selected items as removable "chips" within the dropdown input area.
*   **Code**:
    ```cshtml
    <BitDropdown @bind-Value="comboBoxValueSample2"
                 Combo Chips Items="comboBoxItems" Placeholder="Select an option"
                 Label="Single select combo box & chips" />
    <div>Value: @comboBoxValueSample2</div>

    <BitDropdown @bind-Values="comboBoxValues2"
                 Combo Chips MultiSelect Items="comboBoxItems" Placeholder="Select an option"
                 Label="Multi select combo box & chips" />
    <div>Values: @string.Join(',', comboBoxValues2)</div>
    ```
    ```csharp
    @code {
        private string comboBoxValueSample2 = default!;
        private ICollection<string?> comboBoxValues2 = [];
        // ... comboBoxItems definition (same as basicItems) ...
    }
    ```

**15. Dynamic ComboBox**

*   **Description**: Enables adding new items on-the-fly when using `Combo` mode by setting the `Dynamic` parameter to true. Requires `DynamicValueGenerator` to create the value for the new item and `OnDynamicAdd` to handle the addition logic (e.g., adding to the source list).
*   **Code**:
    ```cshtml
    <BitDropdown @bind-Value="comboBoxValueSample3"
                 Combo Dynamic Items="comboBoxItems" Placeholder="Select an option"
                 Label="Single select combo box & dynamic"
                 DynamicValueGenerator="(BitDropdownItem<string> item) => item.Text"
                 OnDynamicAdd="(BitDropdownItem<string> item) => HandleOnDynamicAdd(item)" />
    <div>Value: @comboBoxValueSample3</div>

    <BitDropdown @bind-Value="comboBoxValueSample4"
                 Responsive Combo Chips Dynamic Items="comboBoxItems" Placeholder="Select an option"
                 Label="Single select combo box, chips & dynamic"
                 DynamicValueGenerator="(BitDropdownItem<string> item) => item.Text"
                 OnDynamicAdd="(BitDropdownItem<string> item) => HandleOnDynamicAdd(item)" />
    <div>Value: @comboBoxValueSample4</div>

    <BitDropdown @bind-Values="comboBoxValues3"
                 Responsive MultiSelect Combo Chips Dynamic Items="comboBoxItems" Placeholder="Select options"
                 Label="Multi select combo box, chips & dynamic"
                 DynamicValueGenerator="(BitDropdownItem<string> item) => item.Text"
                 OnDynamicAdd="(BitDropdownItem<string> item) => HandleOnDynamicAdd(item)" />
    <div>Values: @string.Join(',', comboBoxValues3)</div>
    ```
    ```csharp
    @code {
        private string comboBoxValueSample3 = default!;
        private string comboBoxValueSample4 = default!;
        private ICollection<string?> comboBoxValues3 = [];
        // ... comboBoxItems definition (same as basicItems) ...

        private void HandleOnDynamicAdd(BitDropdownItem<string> item) {
            comboBoxItems.Add(item);
        }
    }
    ```

**16. Style & Class (Revisited)**

*   **Description**: Further examples of applying `Style`, `Class`, `Styles`, and `Classes` for advanced customization, including item-specific classes.
*   **Code**: (Includes CSS for context)
    ```css
    .custom-class { margin-inline: 1rem; box-shadow: dodgerblue 0 0 0.5rem; text-shadow: dodgerblue 0 0 0.5rem; }
    .custom-fruit { background-color: #a5104457; }
    .custom-veg { background-color: #1c73324d; }

    /* Styles for the 'Classes' parameter example */
    .custom-callout { border-radius: 1rem; border-color: lightgray; backdrop-filter: blur(20px); background-color: transparent; box-shadow: darkgray 0 0 0.5rem; }
    .custom-container, .custom-container:after { border-radius: 1rem; } /* Applied to root via Classes */
    .custom-item-button { border-bottom: 1px solid gray; }
    .custom-item-button:hover { background-color: rgba(255, 255, 255, 0.2); }
    .custom-scroll-container div:last-child .custom-item-button { border-bottom: none; }
    ```
    ```cshtml
    <BitDropdown Items="GetBasicItems()" Placeholder="Select an item"
                 Style="margin: 1rem; box-shadow: aqua 0 0 0.5rem; text-shadow: aqua 0 0 0.5rem;" />

    <BitDropdown Class="custom-class" Items="GetBasicItems()" Placeholder="Select an item" />

    <BitDropdown Items="GetStyleClassItems()" Placeholder="Select an item" />

    <BitDropdown Label="Styles" Items="GetBasicItems()" Placeholder="Select an item"
                 Styles="@(new() { Label = "text-shadow: dodgerblue 0 0 0.5rem;",
                                   Container = "box-shadow: dodgerblue 0 0 0.5rem; border-color: lightskyblue; color: lightskyblue;",
                                   ItemHeader = "color: dodgerblue; text-shadow: dodgerblue 0 0 0.5rem;",
                                   ItemButton = "color: lightskyblue",
                                   Callout = "border-radius: 0.25rem; box-shadow: lightskyblue 0 0 0.5rem;" })" />

    <BitDropdown Label="Classes" Items="GetBasicItems()" Placeholder="Select an item"
                 Classes="@(new() { Callout = "custom-callout",
                                    Container = "custom-container",
                                    ItemButton = "custom-item-button",
                                    ScrollContainer = "custom-scroll-container" })" />
    ```
    ```csharp
    @code {
        // ... GetBasicItems() definition ...

        private List<BitDropdownItem<string>> GetStyleClassItems() => new()
        {
            new() { ItemType = BitDropdownItemType.Header, Text = "Fruits", Style = "text-align: center;" },
            new() { Text = "Apple", Value = "f-app", Class = "custom-fruit" },
            new() { Text = "Banana", Value = "f-ban", Class = "custom-fruit" },
            // ... other items with classes ...
        };
    }
    ```

**17. RTL**

*   **Description**: Demonstrates rendering the dropdown component in a right-to-left layout using `Dir="BitDir.Rtl"`.
*   **Code**:
    ```cshtml
    <BitDropdown Label="تک انتخابی" Items="GetRtlItems()" Placeholder="لطفا انتخاب کنید" Dir="BitDir.Rtl" />
    <BitDropdown Label="چند انتخابی" MultiSelect Items="GetRtlItems()" Placeholder="انتخاب چند گزینه ای" Dir="BitDir.Rtl" />
    <BitDropdown Label="تک انتخابی ریسپانسیو" Responsive Items="GetRtlItems()" Placeholder="لطفا انتخاب کنید" Dir="BitDir.Rtl" />
    ```
    ```csharp
    @code {
        private List<BitDropdownItem<string>> GetRtlItems() => new()
        {
            new() { ItemType = BitDropdownItemType.Header, Text = "میوه ها" },
            new() { Text = "سیب", Value = "f-app" },
            // ... other RTL items ...
        };
    }
    ```

---

## API Reference

*(Includes parameters from BitDropdown, BitInputBase, BitComponentBase, and related classes/enums)*

**BitDropdown Parameters**

| Name                         | Type                                                | Default                   | Description                                                                             |
| :--------------------------- | :-------------------------------------------------- | :------------------------ | :-------------------------------------------------------------------------------------- |
| `AutoFocusSearchBox`         | `bool`                                              | `false`                   | Auto-focuses the search box when the callout opens.                                     |
| `CalloutHeaderTemplate`      | `RenderFragment?`                                   | `null`                    | Custom template for the callout header.                                                 |
| `CalloutFooterTemplate`      | `RenderFragment?`                                   | `null`                    | Custom template for the callout footer.                                                 |
| `CaretDownIconName`          | `string?`                                           | `null`                    | Custom icon for the dropdown caret (defaults to `ChevronRight`).                        |
| `CaretDownTemplate`          | `RenderFragment?`                                   | `null`                    | Custom template for the dropdown caret element.                                         |
| `ChildContent`               | `RenderFragment?`                                   | `null`                    | Used for defining items using `BitDropdownOption` components.                         |
| `Chips`                      | `bool`                                              | `false`                   | Displays selected items as chips in Combo mode.                                         |
| `Classes`                    | `BitDropdownClassStyles?`                           | `null`                    | Custom CSS classes for different parts.                                                 |
| `Combo`                      | `bool`                                              | `false`                   | Enables ComboBox behavior (type to filter/select).                                      |
| `DefaultValue`               | `TValue?`                                           | `default`                 | Initial selected value for single-select (uncontrolled).                                |
| `DefaultValues`              | `IEnumerable<TValue?>?`                             | `null`                    | Initial selected values for multi-select (uncontrolled).                                |
| `DropDirection`              | `BitDropDirection`                                  | `TopAndBottom`            | Preferred opening direction(s) for the callout.                                         |
| `Dynamic`                    | `bool`                                              | `false`                   | Allows adding new items dynamically in Combo mode.                                      |
| `DynamicValueGenerator`      | `Func<TItem?, TValue?>?`                            | `null`                    | Generates the `Value` for a dynamically added item.                                     |
| `ExistsSelectedItemFunction` | `Func<ICollection<TItem>, string, bool>?`           |                           | Custom function to check if an item exists in selected items (ComboBox mode).           |
| `FindItemFunction`           | `Func<ICollection<TItem>, string, TItem?>?`         |                           | Custom function to find an item based on text input (ComboBox mode).                    |
| `FitWidth`                   | `bool`                                              | `false`                   | Makes the dropdown width fit its content.                                               |
| `HeaderTemplate`             | `RenderFragment<TItem>?`                            | `null`                    | Custom template for rendering header-type items.                                        |
| `InitialSelectedItems`       | `IEnumerable<TItem>?`                               | `null`                    | Pre-selected items when using `ItemsProvider`.                                          |
| `IsOpen`                     | `bool`                                              | `false`                   | Controls the callout visibility (`@bind-IsOpen`).                                     |
| `Items`                      | `ICollection<TItem>?`                               | `null`                    | The collection of items to display.                                                     |
| `ItemSize`                   | `int`                                               | `35`                      | Height of each item in pixels (for virtualization).                                     |
| `ItemsProvider`              | `BitDropdownItemsProvider<TItem>?`                  | `null`                    | Delegate to load items dynamically (for virtualization).                                |
| `ItemTemplate`               | `RenderFragment<TItem>?`                            | `null`                    | Custom template for rendering normal items.                                             |
| `Label`                      | `string?`                                           | `null`                    | Label displayed above the dropdown.                                                     |
| `LabelTemplate`              | `RenderFragment?`                                   | `null`                    | Custom template for the main label.                                                     |
| `MultiSelect`                | `bool`                                              | `false`                   | Enables selection of multiple items.                                                  |
| `MultiSelectDelimiter`       | `string`                                            | `, `                      | Delimiter used when displaying multiple selected values as text.                      |
| `NameSelectors`              | `BitDropdownNameSelectors<TItem, TValue>?`          | `null`                    | Specifies property names/selectors for custom item types (`TItem`).                     |
| `NoBorder`                   | `bool`                                              | `false`                   | Removes the border from the root element.                                               |
| `OnClick`                    | `EventCallback<MouseEventArgs>`                     |                           | Callback when the dropdown container is clicked.                                        |
| `OnDynamicAdd`               | `EventCallback<TItem>`                              |                           | Callback when a new item is added in Dynamic Combo mode.                                |
| `OnSearch`                   | `EventCallback<string>`                             |                           | Callback when the search box value changes.                                             |
| `OnSelectItem`               | `EventCallback<TItem>`                              |                           | Callback when any item (even if already selected) is clicked.                           |
| `OnValuesChange`             | `EventCallback<IEnumerable<TValue?>>`               |                           | Callback when the collection of selected values changes (multi-select).               |
| `Options`                    | `RenderFragment?`                                   | `null`                    | Alias for `ChildContent`.                                                               |
| `OverscanCount`              | `int`                                               | `3`                       | Number of extra items rendered above/below the visible area in virtualization.        |
| `Placeholder`                | `string?`                                           | `null`                    | Placeholder text displayed when no item is selected.                                    |
| `PlaceholderTemplate`        | `RenderFragment<BitDropdown<TItem, TValue>>?`       | `null`                    | Custom template for the placeholder.                                                    |
| `Prefix`                     | `string?`                                           | `null`                    | Text displayed before the selected value(s).                                            |
| `PrefixTemplate`             | `RenderFragment?`                                   | `null`                    | Custom template for the prefix.                                                         |
| `PreserveCalloutWidth`       | `bool`                                              | `false`                   | Prevents the callout width from adjusting to the dropdown width.                        |
| `Reselectable`               | `bool`                                              | `false`                   | Allows `OnSelectItem` and `OnChange` to fire even if the same item is re-selected.      |
| `Responsive`                 | `bool`                                              | `false`                   | Enables responsive mode (panel display on small screens).                               |
| `SearchBoxPlaceholder`       | `string?`                                           | `null`                    | Placeholder text for the search box.                                                    |
| `SearchFunction`             | `Func<ICollection<TItem>, string, ICollection<TItem>>?`| `null`                    | Custom function for filtering items based on search text.                               |
| `ShowClearButton`            | `bool`                                              | `false`                   | Shows a button to clear the selection(s).                                               |
| `ShowSearchBox`              | `bool`                                              | `false`                   | Shows a search box within the callout.                                                  |
| `Styles`                     | `BitDropdownClassStyles?`                           | `null`                    | Custom CSS styles for different parts.                                                  |
| `Suffix`                     | `string?`                                           | `null`                    | Text displayed after the selected value(s).                                             |
| `SuffixTemplate`             | `RenderFragment?`                                   | `null`                    | Custom template for the suffix.                                                         |
| `TextTemplate`               | `RenderFragment<BitDropdown<TItem, TValue>>?`       | `null`                    | Custom template for displaying the selected value(s) text.                              |
| `Title`                      | `string?`                                           | `null`                    | Tooltip text for the dropdown root element.                                             |
| `Transparent`                | `bool`                                              | `false`                   | Makes the root element background transparent.                                          |
| `Values`                     | `IEnumerable<TValue?>?`                             | `null`                    | The collection of selected values in multi-select (`@bind-Values`).                     |
| `Virtualize`                 | `bool`                                              | `false`                   | Enables item virtualization for performance with large lists.                             |
| `VirtualizePlaceholder`      | `RenderFragment<PlaceholderContext>?`               | `null`                    | Template for items not yet rendered during virtualization.                              |
| *(Inherited)*                | *(See BitInputBase)*                                |                           |                                                                                         |

**BitDropdown Public Members**

| Name                 | Type                 | Description                                                |
| :------------------- | :------------------- | :--------------------------------------------------------- |
| `SelectedItems`      | `IReadOnlyList<TItem>`| Readonly list of selected items (multi-select).            |
| `SelectedItem`       | `TItem?`             | The currently selected item (single-select).             |
| `ComboInputElement`  | `ElementReference`   | `ElementReference` for the combo input element.            |
| `FocusComboInputAsync`| `ValueTask`          | Method to focus the combo input element.                   |
| `SearchInputElement` | `ElementReference`   | `ElementReference` for the search box input element.         |
| `FocusSearchInputAsync`| `ValueTask`          | Method to focus the search box input element.              |
| *(Inherited)*        | *(See BitInputBase)* |                                                            |

**BitInputBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details on `DisplayName`, `InputHtmlAttributes`, `Name`, `NoValidate`, `OnChange`, `ReadOnly`, `Required`, `Value`, `InputElement`, `FocusAsync()`)*

**BitComponentBase Parameters & Members (Inherited)**

*(Refer to the `BitCheckbox` reference file for details on `AriaLabel`, `Class`, `Dir`, `HtmlAttributes`, `Id`, `IsEnabled`, `Style`, `Visibility`, `UniqueId`, `RootElement`)*

**BitDropdownItem Properties**

| Name               | Type                    | Default           | Description                                                         |
| :----------------- | :---------------------- | :---------------- | :------------------------------------------------------------------ |
| `AriaLabel`        | `string?`               | `null`            | AriaLabel for the item.                                           |
| `Class`            | `string?`               | `null`            | Custom CSS class.                                                 |
| `Id`               | `string?`               | `null`            | Custom ID.                                                        |
| `Data`             | `object?`               | `null`            | Custom data associated with the item (for templates).             |
| `IsEnabled`        | `bool`                  | `true`            | Whether the item can be selected.                                 |
| `IsHidden`         | `bool`                  | `false`           | Whether the item is rendered in the list.                         |
| `ItemType`         | `BitDropdownItemType`   | `Normal`          | Type of item (`Normal`, `Header`, `Divider`).                     |
| `Style`            | `string?`               | `null`            | Custom inline style.                                              |
| `Text`             | `string`                | `string.Empty`    | Text displayed for the item.                                      |
| `Title`            | `string?`               | `null`            | Tooltip for the item.                                             |
| `Value`            | `TValue?`               | `default`         | The value associated with the item.                               |
| `IsSelected`       | `bool`                  | `false`           | *(Readonly)* Indicates if the item is currently selected.           |

**BitDropdownOption Properties**

*(Similar to `BitDropdownItem` but defined declaratively as components)*

**BitDropdownNameSelectors Properties**

*(Refer to the `BitMenuButton` reference file for details on this class and its properties like `AriaLabel`, `Class`, `Id`, `Data`, `IsEnabled`, `IsHidden`, `ItemType`, `Style`, `Text`, `Title`, `Value`, etc.)*
*   **Additional properties for Dropdown:** `TextSetter`, `ValueSetter` (used for Dynamic ComboBox mode).

**BitDropdownClassStyles Properties**

| Name                          | Type      | Default | Description                                                              |
| :---------------------------- | :-------- | :------ | :----------------------------------------------------------------------- |
| `Root`                        | `string?` | `null`  | CSS class/style for the root `div`.                                      |
| `Label`                       | `string?` | `null`  | CSS class/style for the label.                                           |
| `Container`                   | `string?` | `null`  | CSS class/style for the main container `div` wrapping the input area.    |
| `TextContainer`               | `string?` | `null`  | CSS class/style for the `span` displaying selected text/placeholder/chips. |
| `ClearButton`                 | `string?` | `null`  | CSS class/style for the clear button.                                    |
| `CaretDownIcon`               | `string?` | `null`  | CSS class/style for the caret down icon.                                 |
| `Overlay`                     | `string?` | `null`  | CSS class/style for the overlay shown when the callout is open.          |
| `Callout`                     | `string?` | `null`  | CSS class/style for the callout (popup).                                 |
| `ResponsiveLabelContainer`    | `string?` | `null`  | CSS class/style for the responsive panel's label container.              |
| `ResponsiveLabel`             | `string?` | `null`  | CSS class/style for the responsive panel's label.                        |
| `ResponsiveCloseButton`       | `string?` | `null`  | CSS class/style for the responsive panel's close button.                 |
| `ResponsiveCloseIcon`         | `string?` | `null`  | CSS class/style for the responsive panel's close icon.                   |
| `SearchBoxContainer`          | `string?` | `null`  | CSS class/style for the search box container.                            |
| `SearchBoxIconContainer`      | `string?` | `null`  | CSS class/style for the search icon container.                           |
| `SearchBoxIcon`               | `string?` | `null`  | CSS class/style for the search icon.                                     |
| `SearchBoxInput`              | `string?` | `null`  | CSS class/style for the search input element.                            |
| `SearchBoxClearButtonContainer`| `string?` | `null`  | CSS class/style for the search clear button container.                   |
| `SearchBoxClearButton`        | `string?` | `null`  | CSS class/style for the search clear button.                             |
| `SearchBoxClearIcon`          | `string?` | `null`  | CSS class/style for the search clear icon.                               |
| `ScrollContainer`             | `string?` | `null`  | CSS class/style for the scrollable container within the callout.         |
| `ItemHeader`                  | `string?` | `null`  | CSS class/style for header items (`ItemType = Header`).                  |
| `ItemWrapper`                 | `string?` | `null`  | CSS class/style for the wrapper `div` around multi-select items.         |
| `ItemButton`                  | `string?` | `null`  | CSS class/style for the item `button` element.                           |
| `ItemCheckBox`                | `string?` | `null`  | CSS class/style for the checkbox `div` in multi-select items.            |
| `ItemCheckIcon`               | `string?` | `null`  | CSS class/style for the checkmark icon `i` in multi-select items.        |
| `ItemText`                    | `string?` | `null`  | CSS class/style for the item text `span`.                              |
| `ItemDivider`                 | `string?` | `null`  | CSS class/style for divider items (`ItemType = Divider`).                |

**Enums**

*   **BitDropdownItemType**: Defines item types (`Normal`, `Header`, `Divider`).
*   **BitVisibility**: Defines visibility states (`Visible`, `Hidden`, `Collapsed`).
*   **BitDir**: Defines text direction (`Ltr`, `Rtl`, `Auto`).
*   **BitDropDirection**: Defines preferred callout opening directions (`Auto`, `TopAndBottom`).

---

## Feedback

*   Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
*   Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Dropdown/BitDropdownDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Inputs/Dropdown/BitDropdownDemo.razor)
*   Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Dropdown/BitDropdown.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Inputs/Dropdown/BitDropdown.razor)

