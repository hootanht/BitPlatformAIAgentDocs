## BitMenuButton

**Overview**

A menu button is a menu item that displays a word or phrase that the user can click to initiate an operation.

**Notes**

* The `BitMenuButton` is a **Multi-API** component.
* It can accept the list of Items in 3 different ways:
    1. Using the `BitMenuButtonItem` class.
    2. Using a Custom Generic class (with `NameSelectors`).
    3. Using the `BitMenuButtonOption` component.

**(Note:** The provided HTML only details the "Item" (`BitMenuButtonItem`) usage.)

---

## Usage Examples (Using `BitMenuButtonItem`)

**1. Basic**

* **Description**: A standard menu button displaying a list of items.
* **Code**:

    ```cshtml
    <BitMenuButton Text="MenuButton" Items="basicItems" />
    ```

    ```csharp
    @code {
        private List<BitMenuButtonItem> basicItems =
        [
            new() { Text = "Item A", Key = "A" },
            new() { Text = "Item B", Key = "B", IsEnabled = false },
            new() { Text = "Item C", Key = "C" }
        ];
    }
    ```

**2. Split**

* **Description**: Demonstrates a split button where the main button area triggers one action (or is the primary item when `Sticky` is used) and the chevron part opens the menu.
* **Code**:

    ```cshtml
    <BitMenuButton Text="Split" Items="basicItems" Split />
    ```

    ```csharp
    // @code section is the same as the Basic example
    ```

**3. Variant**

* **Description**: Shows the three visual variants: `Fill` (default), `Outline`, and `Text`, for both standard and split buttons, in enabled and disabled states.
* **Code**:

    ```cshtml
    <BitMenuButton Text="Fill" Items="basicItems" Variant="BitVariant.Fill" />
    <BitMenuButton Text="Outline" Items="basicItems" Variant="BitVariant.Outline" />
    <BitMenuButton Text="Text" Items="basicItems" Variant="BitVariant.Text" />

    <BitMenuButton Text="Fill" Items="basicItems" Variant="BitVariant.Fill" IsEnabled="false" />
    <BitMenuButton Text="Outline" Items="basicItems" Variant="BitVariant.Outline" IsEnabled="false" />
    <BitMenuButton Text="Text" Items="basicItems" Variant="BitVariant.Text" IsEnabled="false" />

    <BitMenuButton Text="Fill" Items="basicItems" Variant="BitVariant.Fill" Split />
    <BitMenuButton Text="Outline" Items="basicItems" Variant="BitVariant.Outline" Split />
    <BitMenuButton Text="Text" Items="basicItems" Variant="BitVariant.Text" Split />

    <BitMenuButton Text="Fill" Items="basicItems" Variant="BitVariant.Fill" IsEnabled="false" Split />
    <BitMenuButton Text="Outline" Items="basicItems" Variant="BitVariant.Outline" IsEnabled="false" Split />
    <BitMenuButton Text="Text" Items="basicItems" Variant="BitVariant.Text" IsEnabled="false" Split />
    ```

    ```csharp
    // @code section is the same as the Basic example
    ```

**4. Color**

* **Description**: Displays menu buttons using various `BitColor` options (`Primary`, `Secondary`, `Tertiary`, `Info`, `Success`, `Warning`, `SevereWarning`, `Error`, `PrimaryBackground`, `SecondaryBackground`, `TertiaryBackground`, `PrimaryForeground`, `SecondaryForeground`, `TertiaryForeground`, `PrimaryBorder`, `SecondaryBorder`, `TertiaryBorder`) across different variants (`Fill`, `Outline`, `Text`) and modes (standard, split).
* **Code**: (Shows pattern for one color - Primary)

    ```cshtml
    <BitMenuButton Text="Primary" Items="basicItems" Variant="BitVariant.Fill" Color="BitColor.Primary" />
    <BitMenuButton Text="Primary" Items="basicItems" Variant="BitVariant.Outline" Color="BitColor.Primary" />
    <BitMenuButton Text="Primary" Items="basicItems" Variant="BitVariant.Text" Color="BitColor.Primary" />

    <BitMenuButton Text="Primary" Items="basicItems" Variant="BitVariant.Fill" Color="BitColor.Primary" Split />
    <BitMenuButton Text="Primary" Items="basicItems" Variant="BitVariant.Outline" Color="BitColor.Primary" Split />
    <BitMenuButton Text="Primary" Items="basicItems" Variant="BitVariant.Text" Color="BitColor.Primary" Split />

    @* ... other colors follow the same pattern ... *@
    ```

    ```csharp
    // @code section is the same as the Basic example
    ```

**5. Size**

* **Description**: Illustrates the available sizes (`Small`, `Medium`, `Large`) for menu buttons across different variants.
* **Code**:

    ```cshtml
    <BitMenuButton Text="Small" Items="basicItems" Variant="BitVariant.Fill" Size="BitSize.Small" />
    <BitMenuButton Text="Small" Items="basicItems" Variant="BitVariant.Outline" Size="BitSize.Small" />
    <BitMenuButton Text="Small" Items="basicItems" Variant="BitVariant.Text" Size="BitSize.Small" />

    <BitMenuButton Text="Medium" Items="basicItems" Variant="BitVariant.Fill" Size="BitSize.Medium" />
    <BitMenuButton Text="Medium" Items="basicItems" Variant="BitVariant.Outline" Size="BitSize.Medium" />
    <BitMenuButton Text="Medium" Items="basicItems" Variant="BitVariant.Text" Size="BitSize.Medium" />

    <BitMenuButton Text="Large" Items="basicItems" Variant="BitVariant.Fill" Size="BitSize.Large" />
    <BitMenuButton Text="Large" Items="basicItems" Variant="BitVariant.Outline" Size="BitSize.Large" />
    <BitMenuButton Text="Large" Items="basicItems" Variant="BitVariant.Text" Size="BitSize.Large" />
    ```

    ```csharp
    // @code section is the same as the Basic example
    ```

**6. Sticky**

* **Description**: When `Sticky` is true, clicking an item updates the main button's text (and potentially icon) to match the selected item. The callout closes, but the button reflects the choice.
* **Code**:

    ```cshtml
    <BitMenuButton Items="basicItems" Variant="BitVariant.Fill" Sticky />
    <BitMenuButton Items="basicItems" Variant="BitVariant.Fill" Split Sticky />

    <BitMenuButton Items="basicItems" Variant="BitVariant.Outline" Sticky />
    <BitMenuButton Items="basicItems" Variant="BitVariant.Outline" Split Sticky />

    <BitMenuButton Items="basicItems" Variant="BitVariant.Text" Sticky />
    <BitMenuButton Items="basicItems" Variant="BitVariant.Text" Split Sticky />
    ```

    ```csharp
    // @code section is the same as the Basic example
    ```

**7. Icons**

* **Description**: Shows how to add an icon to the main button (`IconName`) and to individual items (`BitMenuButtonItem.IconName`). Also demonstrates customizing the chevron icon (`ChevronDownIcon`).
* **Code**:

    ```cshtml
    <BitMenuButton Text="IconName" Items="basicItemsIcon" IconName="@BitIconName.Edit" />
    <BitMenuButton Text="ChevronDownIcon" Items="basicItemsIcon" ChevronDownIcon="@BitIconName.DoubleChevronDown" Split />
    ```

    ```csharp
    @code {
        private List<BitMenuButtonItem> basicItemsIcon =
        [
            new() { Text = "Item A", Key = "A", IconName = BitIconName.Emoji },
            new() { Text = "Item B", Key = "B", IconName = BitIconName.Emoji, IsEnabled = false },
            new() { Text = "Item C", Key = "C", IconName = BitIconName.Emoji2 }
        ];
    }
    ```

**8. Style & Class**

* **Description**: Demonstrates applying custom `Style` and `Class` attributes to the root component, individual items (`BitMenuButtonItem.Style`, `BitMenuButtonItem.Class`), and specific internal elements using the `Styles` and `Classes` parameters.
* **Code**: (Includes CSS for context)

    ```css
    .custom-class { margin-inline: 1rem; border-radius: 1rem; border-color: tomato; border-width: 0.25rem; }
    .custom-class > button { color: tomato; border-color: tomato; background: transparent; }
    .custom-class > button:hover { background-color: #ff63473b; }
    .custom-item { color: peachpuff; background-color: tomato; }
    .custom-button { color: deepskyblue; background: transparent; }
    .custom-opened .custom-button { color: cornflowerblue; }
    .custom-callout { border-radius: 1rem; border-color: lightgray; backdrop-filter: blur(20px); background-color: transparent; box-shadow: darkgray 0 0 0.5rem; }
    .custom-item-button { border-bottom: 1px solid gray; }
    .custom-item-button:hover { background-color: rgba(255, 255, 255, 0.2); }
    .custom-callout li:last-child .custom-item-button { border-bottom: none; }
    ```

    ```cshtml
    <BitMenuButton Text="Styled Button" Items="basicItems" Style="border-radius: 1rem; margin: 1rem; box-shadow: aqua 0 0 1rem; overflow: hidden;" />
    <BitMenuButton Text="Classed Button" Items="basicItems" Class="custom-class" Variant="BitVariant.Outline" />

    <BitMenuButton Text="Item Styled & Classed Button" Items="itemStyleClassItems" Variant="BitVariant.Text" />

    <BitMenuButton Text="Classes" Items="basicItems" IconName="@BitIconName.FormatPainter" Variant="BitVariant.Text"
                   Classes="@(new() { OperatorButton = "custom-button", Opened = "custom-opened", Callout = "custom-callout", ItemButton = "custom-item-button" })" />

    <BitMenuButton Text="Styles" Items="basicItems" IconName="@BitIconName.Brush"
                   Styles="@(new() { Root = "--button-background: tomato; background: var(--button-background); border-color: var(--button-background); border-radius: 0.25rem;",
                                     Opened = "--button-background: orangered;",
                                     OperatorButton = "background: var(--button-background);",
                                     ItemButton = "background: lightcoral;",
                                     Callout = "border-radius: 0.25rem; box-shadow: lightgray 0 0 0.5rem;" })" />
    ```

    ```csharp
    @code {
        // ... basicItems definition ...

        private static List<BitMenuButtonItem> itemStyleClassItems =
        [
            new() { Text = "Item A (Default)", Key = "A", IconName = BitIconName.Emoji },
            new() { Text = "Item C (Styled)", Key = "B", IconName = BitIconName.Emoji, Style = "color: tomato; border-color: brown; background-color: peachpuff;" },
            new() { Text = "Item B (Classed)", Key = "C", IconName = BitIconName.Emoji2, Class = "custom-item" }
        ];
    }
    ```

**9. Templates**

* **Description**: Shows how to customize the button's header (`HeaderTemplate`), the rendering of all items (`ItemTemplate`), or individual items (`BitMenuButtonItem.Template`). `HeaderTemplate` and `Text` are ignored if `Sticky` is true.
* **Code**:

    ```cshtml
    <BitMenuButton Items="basicItems">
        <HeaderTemplate>
            <div style="font-weight: bold; color: #d13438;">Custom Header!</div>
        </HeaderTemplate>
    </BitMenuButton>

    <BitMenuButton Text="Items" Items="itemTemplateItems" Split>
        <ItemTemplate Context="item">
            <div class="item-template-box">
                <span style="color:brown">@item.Text (@item.Key)</span>
            </div>
        </ItemTemplate>
    </BitMenuButton>

    <BitMenuButton Text="Items" Items="itemTemplateItems2" />
    ```

    ```csharp
    @code {
        // ... basicItems definition ...

        private List<BitMenuButtonItem> itemTemplateItems = [ /* ... items ... */ ];

        private List<BitMenuButtonItem> itemTemplateItems2 =
        [
            new() { /* ..., */ Template = (item => @<div class="item-template-box" style="color:green">@item.Text (@item.Key)</div>) },
            new() { /* ..., */ Template = (item => @<div class="item-template-box" style="color:yellow">@item.Text (@item.Key)</div>) },
            new() { /* ..., */ Template = (item => @<div class="item-template-box" style="color:red">@item.Text (@item.Key)</div>) }
        ];
    }
    ```

**10. Events**

* **Description**: Demonstrates handling `OnClick` (triggered when an item is clicked, or the main button in Split mode) and `OnChange` (triggered when the selected item changes, primarily used with `Sticky` mode). Shows usage with both standard and split buttons, sticky and non-sticky.
* **Code**:

    ```cshtml
    <BitMenuButton Text="Items" Items="basicItems"
                   OnChange="(BitMenuButtonItem item) => eventsChangedItem = item?.Key"
                   OnClick="(BitMenuButtonItem item) => eventsClickedItem = item?.Key" />

    <BitMenuButton Split Text="Items" Items="basicItemsOnClick"
                   OnChange="(BitMenuButtonItem item) => eventsChangedItem = item?.Key"
                   OnClick="@((BitMenuButtonItem item) => eventsClickedItem = "Main button clicked")" />

    <BitMenuButton Sticky Items="basicItems"
                   OnChange="(BitMenuButtonItem item) => eventsChangedItem = item?.Key"
                   OnClick="(BitMenuButtonItem item) => eventsClickedItem = item?.Key" />

    <BitMenuButton Sticky Split Items="basicItemsOnClick"
                   OnChange="(BitMenuButtonItem item) => eventsChangedItem = item?.Key"
                   OnClick="(BitMenuButtonItem item) => eventsClickedItem = item?.Key" />

    <div>Clicked item: @eventsClickedItem</div>
    <div>Changed item: @eventsChangedItem</div>
    ```

    ```csharp
    @code {
        private string? eventsClickedItem;
        private string? eventsChangedItem;
        // ... basicItems definition ...
        private List<BitMenuButtonItem> basicItemsOnClick = [ /* ... items ... */ ];

        protected override void OnInitialized() { /* ... attaches item.OnClick handler ... */ }
    }
    ```

**11. Binding**

* **Description**: Shows various binding scenarios:
  * `DefaultSelectedItem`: Sets the initial item displayed in `Sticky` mode.
  * `@bind-SelectedItem`: Two-way binding for the selected item in `Sticky` mode.
  * `IsSelected` (on item): Pre-selects an item in `Sticky` mode.
  * `IsOpen`: One-way binding to control the callout visibility.
  * `@bind-IsOpen`: Two-way binding to control and monitor the callout visibility.
* **Code**:

    ```cshtml
    <BitMenuButton Split Sticky Items="basicItems" DefaultSelectedItem="basicItems[1]" />

    <BitMenuButton Sticky Items="basicItems" @bind-SelectedItem="twoWaySelectedItem" />
    <BitChoiceGroup Horizontal Items="@choiceGroupItems" @bind-Value="@twoWaySelectedItem" />

    <BitMenuButton Sticky Items="isSelectedItems" />

    <BitMenuButton Sticky Items="basicItems" IsOpen="oneWayIsOpen" />
    <BitCheckbox Label="One-way IsOpen" @bind-Value="oneWayIsOpen" OnChange="async _ => { await Task.Delay(2000); oneWayIsOpen = false; }" />

    <BitMenuButton Sticky Items="basicItems" @bind-IsOpen="twoWayIsOpen" />
    <BitCheckbox Label="Two-way IsOpen" @bind-Value="twoWayIsOpen" />
    ```

    ```csharp
    @code {
        private BitMenuButtonItem twoWaySelectedItem = default!;
        private bool oneWayIsOpen;
        private bool twoWayIsOpen;
        // ... basicItems definition ...
        // ... choiceGroupItems definition (derived from basicItems) ...
        private List<BitMenuButtonItem> isSelectedItems = [ /* ... items with one IsSelected = true ... */ ];

        protected override void OnInitialized() { twoWaySelectedItem = basicItems[2]; }
    }
    ```

**12. RTL**

* **Description**: Demonstrates using the `Dir="BitDir.Rtl"` attribute to render the component and its items in a right-to-left layout.
* **Code**:

    ```cshtml
    <BitMenuButton Text="گزینه ها" Dir="BitDir.Rtl" Items="rtlItemsIcon" IconName="@BitIconName.Edit" />
    <BitMenuButton Text="گزینه ها" Dir="BitDir.Rtl" Items="rtlItemsIcon" ChevronDownIcon="@BitIconName.DoubleChevronDown" Split />
    ```

    ```csharp
    @code {
        private static List<BitMenuButtonItem> rtlItemsIcon =
        [
            new() { Text = "گزینه الف", Key = "A", IconName = BitIconName.Emoji },
            new() { Text = "گزینه ب", Key = "B", IconName = BitIconName.Emoji },
            new() { Text = "گزینه ج", Key = "C", IconName = BitIconName.Emoji2 }
        ];
    }
    ```

---

## API Reference

**BitMenuButton Parameters**

| Name                  | Type                                   | Default             | Description                                                                     |
| :-------------------- | :------------------------------------- | :------------------ | :------------------------------------------------------------------------------ |
| `AriaDescription`     | `string?`                              | `null`              | Detailed description for screen readers.                                        |
| `AriaHidden`          | `bool`                                 | `false`             | If true, hides the button from screen readers.                                  |
| `ButtonType`          | `BitButtonType?`                       | `null`              | The `type` attribute of the button (`Button`, `Submit`, `Reset`).               |
| `ChevronDownIcon`     | `string?`                              | `null`              | Custom icon for the chevron down part.                                          |
| `ChildContent`        | `RenderFragment?`                      | `null`              | Content for `BitMenuButtonOption` components.                                   |
| `Classes`             | `BitMenuButtonClassStyles?`            | `null`              | Custom CSS classes for different parts.                                         |
| `Color`               | `BitColor?`                            | `null`              | General color of the button.                                                    |
| `DefaultSelectedItem` | `TItem?`                               | `null`              | Default selected item (used with `Sticky`).                                     |
| `HeaderTemplate`      | `RenderFragment?`                      | `null`              | Custom template for the button's header (ignored if `Sticky` is true).          |
| `IconName`            | `string?`                              | `null`              | Icon shown inside the button's header.                                          |
| `IsOpen`              | `bool`                                 | `false`             | Controls the visibility of the callout (use `@bind-IsOpen` for two-way).        |
| `Items`               | `IEnumerable<TItem>`                   | `new List<TItem>()` | List of items (`BitMenuButtonItem` or custom type) to display.                |
| `ItemTemplate`        | `RenderFragment<TItem>?`               | `null`              | Custom template for rendering each item.                                        |
| `NameSelectors`       | `BitMenuButtonNameSelectors<TItem>?` | `null`              | Specifies property names/selectors when using a custom item type (`TItem`).     |
| `OnClick`             | `EventCallback<MouseEventArgs>`        |                     | Callback when the button header is clicked (or item if not `Split`/`Sticky`).   |
| `OnChange`            | `EventCallback<TItem>`                 |                     | Callback when the selected item changes (used with `Sticky` or `@bind-Value`). |
| `Options`             | `RenderFragment?`                      | `null`              | Alias for `ChildContent`.                                                       |
| `SelectedItem`        | `TItem?`                               | `null`              | The currently selected item (use `@bind-SelectedItem` for two-way).             |
| `Size`                | `BitSize?`                             | `null`              | Size of the button (`Small`, `Medium`, `Large`).                                |
| `Split`               | `bool`                                 | `false`             | Renders as a split button if true.                                              |
| `Sticky`              | `bool`                                 | `false`             | If true, the header updates to show the selected item.                          |
| `Styles`              | `BitMenuButtonClassStyles?`            | `null`              | Custom CSS styles for different parts.                                          |
| `Text`                | `string?`                              | `null`              | Text shown inside the button's header (ignored if `Sticky` is true).            |
| `Variant`             | `BitVariant?`                          | `null`              | Visual variant (`Fill`, `Outline`, `Text`).                                     |
| *(Inherited)*        | *(See BitComponentBase)*               |                     |                                                                                 |

**BitComponentBase Parameters (Inherited)**

| Name           | Type                         | Default                   | Description                                                           |
| :------------- | :--------------------------- | :------------------------ | :-------------------------------------------------------------------- |
| `AriaLabel`    | `string?`                    | `null`                    | Aria-label for accessibility.                                         |
| `Class`        | `string?`                    | `null`                    | Custom CSS class for the root element.                                |
| `Dir`          | `BitDir?`                    | `null`                    | Component direction (`Ltr`, `Rtl`, `Auto`).                           |
| `HtmlAttributes`| `Dictionary<string, object>` | `new Dictionary<>()`      | Additional HTML attributes to render.                                 |
| `Id`           | `string?`                    | `null`                    | Custom ID for the root element (defaults to `UniqueId`).              |
| `IsEnabled`    | `bool`                       | `true`                    | Whether the component is enabled.                                     |
| `Style`        | `string?`                    | `null`                    | Custom CSS style for the root element.                                |
| `Visibility`   | `BitVisibility`              | `BitVisibility.Visible`   | Component visibility (`Visible`, `Hidden`, `Collapsed`).              |

**BitComponentBase Public Members (Inherited)**

| Name        | Type               | Default          | Description                                       |
| :---------- | :----------------- | :--------------- | :------------------------------------------------ |
| `UniqueId`  | `Guid`             | `Guid.NewGuid()` | Readonly unique ID assigned at construction.      |
| `RootElement` | `ElementReference` |                  | `ElementReference` for the root DOM element.    |

**BitMenuButtonItem Properties (for `Items` parameter)**

| Name       | Type                            | Default | Description                                           |
| :--------- | :------------------------------ | :------ | :---------------------------------------------------- |
| `Class`    | `string?`                       | `null`  | Custom CSS class for the item.                      |
| `IconName` | `string?`                       | `null`  | Icon to render next to the text.                    |
| `IsEnabled`| `bool`                          | `true`  | Whether the item is enabled.                        |
| `IsSelected`| `bool`                          | `false` | Selection state (used with `Sticky` binding).       |
| `Key`      | `string?`                       | `null`  | Unique key for the item.                            |
| `OnClick`  | `EventCallback`                 |         | Click event handler specifically for this item.       |
| `Style`    | `string?`                       | `null`  | Custom inline style for the item.                   |
| `Template` | `RenderFragment<BitMenuButtonItem>?` | `null`  | Custom template to render this specific item.       |
| `Text`     | `string?`                       | `null`  | Text to display for the item.                       |

**BitMenuButtonOption Properties (for `ChildContent`/`Options`)**

*(Similar to `BitMenuButtonItem`, represents items declared as components)*

| Name       | Type                                | Default | Description                                         |
| :--------- | :---------------------------------- | :------ | :-------------------------------------------------- |
| `Class`    | `string?`                           | `null`  | Custom CSS class for the option.                    |
| `IconName` | `string?`                           | `null`  | Icon to render next to the text.                  |
| `IsEnabled`| `bool`                              | `true`  | Whether the option is enabled.                      |
| `IsSelected`| `bool`                              | `false` | Selection state (used with `Sticky` binding).     |
| `Key`      | `string?`                           | `null`  | Unique key for the option.                        |
| `OnClick`  | `EventCallback`                     |         | Click event handler specifically for this option.   |
| `Style`    | `string?`                           | `null`  | Custom inline style for the option.                 |
| `Template` | `RenderFragment<BitMenuButtonOption>?` | `null`  | Custom template to render this specific option.   |
| `Text`     | `string?`                           | `null`  | Text to display for the option.                   |

**BitMenuButtonClassStyles Properties (for `Classes`/`Styles`)**

| Name                 | Type      | Default | Description                                                   |
| :------------------- | :-------- | :------ | :------------------------------------------------------------ |
| `Root`               | `string?` | `null`  | Style/Class for the root element.                             |
| `Opened`             | `string?` | `null`  | Style/Class applied when the callout is open.                 |
| `OperatorButton`     | `string?` | `null`  | Style/Class for the main operator button part.                |
| `OperatorButtonIcon` | `string?` | `null`  | Style/Class for the icon within the operator button.          |
| `OperatorButtonText` | `string?` | `null`  | Style/Class for the text within the operator button.          |
| `Callout`            | `string?` | `null`  | Style/Class for the callout popup element.                    |
| `CalloutContainer`   | `string?` | `null`  | Style/Class for the container within the callout.             |
| `ChevronDownButton`  | `string?` | `null`  | Style/Class for the chevron down button (in `Split` mode).    |
| `ChevronDown`        | `string?` | `null`  | Style/Class for the chevron icon itself.                      |
| `Separator`          | `string?` | `null`  | Style/Class for the separator line (in `Split` mode).         |
| `Icon`               | `string?` | `null`  | Style/Class for the main button's icon (`IconName` parameter).|
| `ItemWrapper`        | `string?` | `null`  | Style/Class for the `<li>` wrapper around each item button.   |
| `ItemButton`         | `string?` | `null`  | Style/Class for the `<button>` element of each item.          |
| `ItemIcon`           | `string?` | `null`  | Style/Class for the icon within each item.                    |
| `ItemText`           | `string?` | `null`  | Style/Class for the text within each item.                    |
| `Overlay`            | `string?` | `null`  | Style/Class for the overlay shown when the callout is open.   |
| `Text`               | `string?` | `null`  | Style/Class for the main button's text (`Text` parameter).    |

**(Note:** Other classes like `BitMenuButtonNameSelectors`, `BitNameSelectorPair` and Enums like `BitButtonType`, `BitColor`, `BitSize`, `BitVariant`, `BitVisibility`, `BitDir` are also documented in the API section with their properties/values and descriptions.)

---

## Feedback

* Provide feedback via the **GitHub repo**: [File an Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or [Start a Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
* Review/Edit this demo page: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/MenuButton/BitMenuButtonDemo.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Buttons/MenuButton/BitMenuButtonDemo.razor)
* Review/Edit the component source: [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Buttons/MenuButton/BitMenuButton.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Buttons/MenuButton/BitMenuButton.razor)
