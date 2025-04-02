# BitBasicList Component Reference (Blazor UI)

## 1. Overview

**`BitBasicList`** is a foundational Blazor component designed for efficiently rendering lists of items, especially large datasets. It provides the core structure for list rendering but remains agnostic regarding layout specifics, the appearance of individual items (tiles/rows), and selection management. This makes it a flexible base for building various list-based UI experiences.

**Key Purpose:** To display collections of data (`TItem`) in a list format, with built-in support for high-performance virtualization.

## 2. Key Features

*   **Data Binding:** Accepts data through simple `ICollection<TItem>` (`Items` parameter) or dynamically via an `ItemsProvider` delegate for scenarios like async loading or large datasets.
*   **Virtualization:** Built-in support (`EnableVirtualization`) to render only the visible items, significantly improving performance for long lists.
*   **Custom Item Rendering:** Uses a `RowTemplate` (`RenderFragment<TItem>`) to allow complete control over how each item in the list is displayed.
*   **Customization:** Supports standard Blazor component customization via `Class`, `Style`, `Id`, and `HtmlAttributes`.
*   **Accessibility:** Supports `AriaLabel` and configurable `Role` (defaults to "list").
*   **RTL Support:** Built-in support for Right-to-Left layouts using the `Dir` parameter.
*   **Placeholders:** Customizable content for empty lists (`EmptyContent`) and loading states during virtualization (`VirtualizePlaceholder`).
*   **Performance Tuning:** Allows configuration of `ItemSize` and `OverscanCount` for fine-tuning virtualization behavior.

## 3. Core Usage (Basic Example)

The fundamental use involves providing a collection of items and defining a template for how each item should be rendered.

**Component:** `BitBasicList<TItem>`

**Example (`.razor`):**

```cshtml
@* Data source (see C# code below) *@
@using System.Collections.Generic
@using System.Linq

<BitBasicList Items="FewPeople" Style="border: 1px #a19f9d solid; border-radius: 4px;">
    <RowTemplate Context="person">
        <div style="padding: 5px 20px; margin: 10px; background-color: #75737329;">
            Name: <strong>@person.FirstName</strong>
        </div>
    </RowTemplate>
</BitBasicList>

@code {
    private List<Person> FewPeople = Enumerable.Range(0, 100).Select(i => new Person
    {
        Id = i + 1,
        FirstName = $"Person {i + 1}",
        LastName = $"Person Family {i + 1}",
        Job = $"Programmer {i + 1}"
    }).ToList();

    public class Person
    {
        public int Id { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public string Job { get; set; }
    }
}
```

**Explanation:**

1. **`Items="FewPeople"`:** Binds the list to the `FewPeople` C# collection (`List<Person>`). The component will iterate over this collection. `TItem` is inferred as `Person`.
2. **`<RowTemplate Context="person">`:** Defines the Blazor `RenderFragment` that will be used to render *each* item in the `FewPeople` list.
3. **`Context="person"`:** Specifies the variable name (`person`) that represents the current item (`Person` object) within the template's scope.
4. **`@person.FirstName`:** Accesses properties of the current `Person` object being rendered.
5. **`Style`:** Applies basic inline styling to the list container.

---

## 4. Virtualization (Handling Large Lists)

For lists with hundreds or thousands of items, rendering everything at once can be slow. Virtualization solves this by only rendering the items currently visible in the viewport, plus a small buffer (overscan).

**Enable Virtualization:** Set `EnableVirtualization="true"`.

**Required for Virtualization:**

* You **must** provide a unique `@key` for the root element within your `RowTemplate`. This allows Blazor to efficiently track and update items during scrolling.
* Specify `ItemSize` (in pixels) to tell the virtualization mechanism the height of each rendered item. Accurate sizing is crucial for correct scrolling behavior.

**Optional Tuning:**

* `OverscanCount`: Controls how many extra items are rendered above and below the visible area. Increasing this can make scrolling feel smoother at the cost of rendering slightly more items.

**Example (`.razor`):**

```cshtml
@* Data source (see C# code below) *@
@using System.Collections.Generic
@using System.Linq

<BitBasicList Items="LotsOfPeople"
              EnableVirtualization="true"
              ItemSize="125" @* Approximate height of each rendered row in pixels *@
              OverscanCount="5" @* Render 5 extra items above/below viewport *@
              Style="border: 1px #a19f9d solid; border-radius: 4px; height: 400px; overflow-y: auto;"> @* Ensure list has fixed height and scroll *@
    <RowTemplate Context="person">
        <div @key="person.Id" @* REQUIRED for virtualization *@
             style="border-bottom: 1px #8a8886 solid; padding: 5px 20px; margin: 10px;">
            <img width="100px" height="100px" src="https://picsum.photos/100/100?random=@(person.Id)">
            <div style="margin-left:3%; display: inline-block;">
                <p>Id: <strong>@person.Id</strong></p>
                <p>Full Name: <strong>@person.FirstName @person.LastName</strong></p>
                <p>Job: <strong>@person.Job</strong></p>
            </div>
        </div>
    </RowTemplate>
</BitBasicList>

@code {
    // Using 8000 items to demonstrate virtualization need
    private List<Person> LotsOfPeople = Enumerable.Range(0, 8000).Select(i => new Person
    {
        Id = i + 1,
        FirstName = $"Person {i + 1}",
        LastName = $"Person Family {i + 1}",
        Job = $"Programmer {i + 1}"
    }).ToList();

    // Person class definition remains the same as the basic example
    public class Person { /* ... */ }
}
```

**Explanation:**

1. **`EnableVirtualization="true"`:** Turns on virtualization.
2. **`ItemSize="125"`:** Informs the component that each rendered row is approximately 125 pixels high. **Note:** The actual height in the source HTML example seems closer to ~125-130px including margins. Adjust this value based on your actual `RowTemplate` rendering.
3. **`OverscanCount="5"`:** Renders 5 items before the first visible item and 5 items after the last visible item. Default is 3.
4. **`@key="person.Id"`:** Provides a unique identifier for each rendered item, crucial for virtualization.
5. **`Style` on `BitBasicList`:** A fixed height and `overflow-y: auto` (or `scroll`) are typically required on the list or a parent container for virtualization scrolling to work correctly within a bounded area.

---

## 5. Data Loading with `ItemsProvider`

Instead of providing a static `Items` collection, you can use `ItemsProvider` for more advanced scenarios like:

* Loading data asynchronously (e.g., from an API).
* Implementing server-side paging and filtering.
* Handling extremely large datasets that shouldn't be loaded into memory all at once.

**`ItemsProvider` Signature:**

```csharp
// Delegate type
public delegate ValueTask<BitBasicListItemsProviderResult<TItem>> BitBasicListItemsProvider<TItem>(
    BitBasicListItemsProviderRequest<TItem> request);

// Request object passed to your provider function
public readonly struct BitBasicListItemsProviderRequest<TItem>
{
    public int StartIndex { get; } // The index of the first item required
    public int Count { get; }      // The number of items required
    public CancellationToken CancellationToken { get; } // For cancellation
    // Potentially other context like sorting/filtering info in future versions
}

// Result object your provider function must return
public readonly struct BitBasicListItemsProviderResult<TItem>
{
    public IEnumerable<TItem> Items { get; } // The items requested
    public int TotalItemCount { get; }      // The total number of items available (for scrollbar calculation)
}
```

**Using `ItemsProvider`:**

1. Define a C# method matching the `BitBasicListItemsProvider<TItem>` delegate signature.
2. Assign this method to the `ItemsProvider` parameter.
3. Inside the method, use the `request.StartIndex` and `request.Count` to fetch the specific slice of data needed.
4. Return the fetched items and the *total* number of items available using `BitBasicListItemsProviderResult.From(items, totalCount)`.
5. Use `EnableVirtualization="true"`. `ItemsProvider` typically implies virtualization.
6. Optionally define a `VirtualizePlaceholder` to show while data is loading.

**Example (`.razor`):**

```cshtml
@* Inject HttpClient and NavigationManager for API calls *@
@inject HttpClient HttpClient
@inject NavigationManager NavManager
@using System.Text.Json.Serialization

<BitBasicList TItem="ProductDto" @* Explicit TItem often needed with ItemsProvider *@
              ItemSize="83" @* Approximate height of each product row *@
              EnableVirtualization="true"
              ItemsProvider="@ProductsProvider"
              Style="border: 1px #a19f9d solid; border-radius: 4px; height: 400px; overflow-y: auto;">
    <RowTemplate Context="product">
        <div @key="product.Id" style="border-bottom: 1px #8a8886 solid; padding: 5px 20px;">
            <div>Id: <strong>@product.Id</strong></div>
            <div>Name: <strong>@product.Name</strong></div>
            <div>Price: <strong>@product.Price</strong></div>
        </div>
    </RowTemplate>
    <VirtualizePlaceholder>
        <div style="border-bottom: 1px #8a8886 solid; padding: 5px 20px; height: 83px; display: flex; align-items: center;">
             <strong>Loading...</strong>
        </div>
    </VirtualizePlaceholder>
</BitBasicList>

@code {
    private BitBasicListItemsProvider<ProductDto> ProductsProvider;

    protected override void OnInitialized()
    {
        ProductsProvider = async request =>
        {
            try
            {
                // Example: Construct OData-like query parameters
                var query = new Dictionary<string, object>()
                {
                     { "$top", request.Count },
                     { "$skip", request.StartIndex }
                     // Add other params like $filter, $orderby based on component state if needed
                };

                // Replace with your actual API endpoint
                var url = NavManager.GetUriWithQueryParameters("api/Products/GetProducts", query);

                // Assuming your API returns a structure like PagedResult<ProductDto>
                // Need a JsonContext for AOT compilation trimming safety
                var data = await HttpClient.GetFromJsonAsync(url, AppJsonContext.Default.PagedResultProductDto);

                // Return the result in the required format
                return BitBasicListItemsProviderResult.From(data!.Items, (int)data!.TotalCount);
            }
            catch (Exception ex)
            {
                // Handle errors appropriately
                Console.WriteLine($"Error fetching products: {ex.Message}");
                return BitBasicListItemsProviderResult.From(new List<ProductDto>(), 0);
            }
        };

        base.OnInitialized();
    }

    // DTO matching API response item
    public class ProductDto
    {
        public int Id { get; set; }
        public string? Name { get; set; }
        public decimal Price { get; set; }
        public int CategoryId { get; set; }
    }

    // Example structure for paged API response
    public class PagedResult<T>
    {
        public List<T> Items { get; set; } = new();
        public long TotalCount { get; set; }
    }

    // JSON Source Generation context for AOT safety
    [JsonSerializable(typeof(PagedResult<ProductDto>))]
    public partial class AppJsonContext : JsonSerializerContext { }
}
```

---

## 6. Grouped Lists

While `BitBasicList` doesn't have built-in grouping *parameters*, you can achieve grouped displays using `ItemsProvider` and conditional logic within the `RowTemplate`.

1. **Data Structure:** Define a common DTO (`CategoryOrProductDto` in the example) that can represent either a group header (category) or an item (product). Use properties to distinguish between them (e.g., `IsProduct`).
2. **`ItemsProvider` Logic:** Your provider should fetch data in a way that includes both category headers and their corresponding products in the correct order. The `TotalItemCount` should reflect the total number of rows (headers + items).
3. **`RowTemplate` Logic:** Use `@if` statements inside the `RowTemplate` based on the DTO's properties (`catOrProd.IsProduct`) to render different markup for headers and items.
4. **`@key`:** Ensure the `@key` is unique across *all* rendered rows (both headers and items). A common pattern is to use the category ID for headers and a combination of category and product ID for items.

**Example (`.razor`):** (Conceptual - Provider logic is key)

```cshtml
@* Assumes ItemsProvider "CategoriesAndProductsProvider" is implemented *@
@* Assumes DTO "CategoryOrProductDto" exists *@
@inject HttpClient HttpClient
@inject NavigationManager NavManager
@using System.Text.Json.Serialization

<BitBasicList TItem="CategoryOrProductDto"
              ItemSize="50" @* Adjust based on average row height (can be tricky with variable heights) *@
              EnableVirtualization="true"
              ItemsProvider="@CategoriesAndProductsProvider"
              Style="border: 1px #a19f9d solid; border-radius: 4px; height: 400px; overflow-y: auto;">
    <RowTemplate Context="catOrProd">
        @if (catOrProd.IsProduct)
        {
            @* Render Product Row *@
            <div @key="@($"prod-{catOrProd.ProductId}")" @* Unique key for product *@
                 style="border-bottom: 1px #8a8886 solid; padding: 5px 20px; margin-left: 20px;"> @* Indent product *@
                <div>Name: <strong>@catOrProd.Name</strong></div>
                <div>Price: <strong>@catOrProd.Price</strong></div>
            </div>
        }
        else
        {
            @* Render Category Header Row *@
            <div @key="@($"cat-{catOrProd.CategoryId}")" @* Unique key for category *@
                 style="border-bottom: 1px #8a8886 solid; padding: 10px 10px; background-color: #e0e0e0; font-weight: bold;">
                @catOrProd.Name
            </div>
        }
    </RowTemplate>
    <VirtualizePlaceholder>
        <div style="padding: 15px 20px; height: 50px;">Loading group...</div>
    </VirtualizePlaceholder>
</BitBasicList>

@code {
    private BitBasicListItemsProvider<CategoryOrProductDto> CategoriesAndProductsProvider;

    protected override void OnInitialized()
    {
        // Implementation fetches categories and their products, interleaving them
        CategoriesAndProductsProvider = async request => {
             // ... Fetch logic that returns a list containing both category headers
             // ... and product items in sequence, plus the total count of rows.
             // ... Example: Fetch page N might return [Cat3Header, Prod3.1, Prod3.2, Cat4Header, Prod4.1, ...]
             try
             {
                 var query = new Dictionary<string, object>() { { "$top", request.Count }, { "$skip", request.StartIndex } };
                 var url = NavManager.GetUriWithQueryParameters("api/Products/GetCategoriesAndProducts", query); // Example endpoint
                 var data = await HttpClient.GetFromJsonAsync(url, AppJsonContext.Default.PagedResultCategoryOrProductDto);
                 return BitBasicListItemsProviderResult.From(data!.Items, (int)data!.TotalCount);
             }
             catch(Exception ex)
             {
                 Console.WriteLine($"Error fetching grouped data: {ex.Message}");
                 return BitBasicListItemsProviderResult.From(new List<CategoryOrProductDto>(), 0);
             }
        };
        base.OnInitialized();
    }

    // Combined DTO for either a Category or a Product
    public class CategoryOrProductDto
    {
        // Nullable IDs help differentiate
        public int? ProductId { get; set; }
        public int? CategoryId { get; set; }

        // Helper to check type
        public bool IsProduct => ProductId.HasValue;

        // Common properties
        public string? Name { get; set; } // Category Name or Product Name
        public decimal? Price { get; set; } // Only for products
    }

     // Example structure for paged API response
    public class PagedResult<T>
    {
        public List<T> Items { get; set; } = new();
        public long TotalCount { get; set; }
    }

    // Updated JSON Context
    [JsonSerializable(typeof(PagedResult<CategoryOrProductDto>))]
    public partial class AppJsonContext : JsonSerializerContext { }
}
```

**Note on Grouping & Virtualization:** Virtualization with variable row heights (like headers vs items) can sometimes be less precise. Setting `ItemSize` to an average or the most common row height is often the best approach.

---

## 7. Custom Styling

Apply custom CSS using the standard `Class` and `Style` parameters.

**Example (`.razor`):**

```cshtml
<style>
    .custom-basic-list-container {
        border: 2px dashed blue;
        border-radius: 8px;
        background-color: #f0f8ff; /* AliceBlue */
        height: 300px;
        overflow-y: auto;
    }

    .custom-basic-list-container .list-item { /* Target items within the specific list */
        gap: 0.5rem;
        color: white;
        display: flex;
        padding: 1rem;
        margin: 0.5rem;
        flex-wrap: wrap;
        border-radius: 0.25rem;
        background-color: tomato;
        font-family: 'Comic Sans MS', cursive, sans-serif; /* For fun */
    }
</style>

<BitBasicList Items="LotsOfPeople"
              Class="custom-basic-list-container" @* Apply custom class *@
              EnableVirtualization="true"
              ItemSize="60" @* Adjusted for new padding/margin *@
              Style="box-shadow: 3px 3px 5px grey;"> @* Apply inline style *@
    <RowTemplate Context="person">
        <div @key="person.Id" class="list-item"> @* Apply class to item *@
            <span>Id: <strong>@person.Id</strong></span>
            <span>Full Name: <strong>@person.FirstName</strong></span>
            <span>Job: <strong>@person.Job</strong></span>
        </div>
    </RowTemplate>
</BitBasicList>

@code {
    // LotsOfPeople and Person class definition remain the same
    private List<Person> LotsOfPeople = Enumerable.Range(0, 100).Select(i => new Person { Id = i + 1, FirstName = $"Person {i + 1}", LastName = $"LN{i+1}", Job = $"Job{i+1}" }).ToList();
    public class Person { public int Id { get; set; } public string FirstName { get; set; } public string LastName { get; set; } public string Job { get; set; } }
}
```

---

## 8. Right-to-Left (RTL) Support

Set the `Dir` parameter to `BitDir.Rtl` for languages written right-to-left.

**Example (`.razor`):**

```cshtml
<BitBasicList Dir="BitDir.Rtl" @* Enable RTL *@
              Items="FewPeopleRtl"
              Style="border: 1px #a19f9d solid; border-radius: 4px;">
    <RowTemplate Context="person">
        <div style="padding: 5px 20px; margin: 10px; background-color: #75737329; text-align: right;"> @* Ensure text aligns right *@
            <p>شناسه: <strong>@person.Id</strong></p>
            <p>نام کامل: <strong>@person.FirstName @person.LastName</strong></p>
            <p>شغل: <strong>@person.Job</strong></p>
        </div>
    </RowTemplate>
</BitBasicList>

@code {
    private List<Person> FewPeopleRtl = Enumerable.Range(0, 100).Select(i => new Person
    {
        Id = i + 1,
        FirstName = $"شخص {i + 1}",
        LastName = $"نام خانواگی شخص {i + 1}",
        Job = $"برنامه نویس {i + 1}"
    }).ToList();

    // Person class definition remains the same
    public class Person { public int Id { get; set; } public string FirstName { get; set; } public string LastName { get; set; } public string Job { get; set; } }
}
```

---

## 9. API Reference

### `BitBasicList<TItem>` Parameters

| Name                  | Type                                     | Default Value              | Description                                                                                                   |
| :-------------------- | :--------------------------------------- | :------------------------- | :------------------------------------------------------------------------------------------------------------ |
| `Items`               | `ICollection<TItem>`                     | `new Array.Empty<TItem>()` | Gets or sets the list of items to render. Use this **or** `ItemsProvider`.                                  |
| `ItemsProvider`       | `BitBasicListItemsProvider<TItem>?`      | `null`                     | A callback that supplies data dynamically. Use this **or** `Items`.                                           |
| `RowTemplate`         | `RenderFragment<TItem>?`                 | `null`                     | **Required**. Defines the Blazor template used to render each item in the list.                               |
| `EnableVirtualization`| `bool`                                   | `false`                    | Enables virtualization for rendering only visible items, improving performance for large lists.             |
| `ItemSize`            | `float`                                  | `50`                       | **Required for Virtualization**. The height (in pixels) of each item. Affects virtualization calculations. |
| `OverscanCount`       | `int`                                    | `3`                        | Used with Virtualization. How many extra items to render above/below the visible area.                        |
| `VirtualizePlaceholder`| `RenderFragment<PlaceholderContext>?`   | `null`                     | Optional template shown for items while they are loading when using `ItemsProvider` with virtualization.      |
| `EmptyContent`        | `RenderFragment?`                        | `null`                     | Optional template shown when the `Items` collection is empty or `ItemsProvider` returns no data.            |
| `Role`                | `string`                                 | `"list"`                   | The `role` attribute applied to the root HTML element of the list (e.g., `<div>` or `<ul>`).                |
| `Class`               | `string?`                                | `null`                     | Custom CSS class for the root element. Inherited from `BitComponentBase`.                                   |
| `Style`               | `string?`                                | `null`                     | Custom inline CSS style for the root element. Inherited from `BitComponentBase`.                              |
| `Id`                  | `string?`                                | `null`                     | Custom `id` attribute for the root element. Inherited from `BitComponentBase`.                              |
| `AriaLabel`           | `string?`                                | `null`                     | The `aria-label` attribute for accessibility. Inherited from `BitComponentBase`.                            |
| `Dir`                 | `BitDir?`                                | `null`                     | Sets the component direction (Ltr, Rtl, Auto). Inherited from `BitComponentBase`.                           |
| `IsEnabled`           | `bool`                                   | `true`                     | Whether the component is enabled (affects styling/behavior). Inherited from `BitComponentBase`.             |
| `Visibility`          | `BitVisibility`                          | `BitVisibility.Visible`    | Controls component visibility (Visible, Hidden, Collapsed). Inherited from `BitComponentBase`.              |
| `HtmlAttributes`      | `Dictionary<string, object>`             | `new(...)`                 | Allows passing additional HTML attributes to the root element. Inherited from `BitComponentBase`.           |

*(Inherited parameters are from `BitComponentBase`)*

### Public Members (from `BitComponentBase`)

| Name          | Type                | Default Value    | Description                                                                              |
| :------------ | :------------------ | :--------------- | :--------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`              | `Guid.NewGuid()` | **Readonly**. A unique ID generated for the component instance.                            |
| `RootElement` | `ElementReference`  | *(N/A)*          | A Blazor `ElementReference` to the root HTML element rendered by the component.        |

### Enums

**`BitVisibility`**

| Name        | Value | Description                                                                     |
| :---------- | :---- | :------------------------------------------------------------------------------ |
| `Visible`   | `0`   | The component is visible.                                                       |
| `Hidden`    | `1`   | The component is hidden (`visibility: hidden`), but still occupies space.       |
| `Collapsed` | `2`   | The component is hidden (`display: none`) and does not occupy space.            |

**`BitDir`**

| Name   | Value | Description                                                                       |
| :----- | :---- | :-------------------------------------------------------------------------------- |
| `Ltr`  | `0`   | Left-to-right direction.                                                          |
| `Rtl`  | `1`   | Right-to-left direction.                                                          |
| `Auto` | `2`   | Direction is determined by the browser based on the content.                      |

---

## 10. Best Practices & Considerations

* **`@key` is Crucial:** Always use a unique `@key` on the root element inside your `RowTemplate` when `EnableVirtualization` is `true` or when the list content can change dynamically.
* **Accurate `ItemSize`:** For virtualization, provide the most accurate `ItemSize` possible (including padding/margins). Inaccurate values lead to jumpy scrolling or incorrect scrollbar size.
* **Fixed Height Container:** When using virtualization, the `BitBasicList` or one of its parent elements usually needs a defined height and `overflow: auto` or `overflow: scroll` style for the scrolling mechanism to work correctly within a bounded area.
* **`Items` vs. `ItemsProvider`:**
  * Use `Items` for simple, small-to-medium sized lists already available in memory.
  * Use `ItemsProvider` for large datasets, asynchronous loading, server-side operations (paging, sorting, filtering), or when you need fine-grained control over data fetching.
* **Performance:** Virtualization significantly helps with rendering performance for large lists. Avoid complex calculations or nested components within the `RowTemplate` if possible, especially for very long lists, as the template is rendered frequently during scrolling.
* **Grouping Height:** Virtualization with grouped items (variable row heights) can be less precise. Consider using an average `ItemSize` or testing thoroughly.

---

## 11. Further Information (Source Links)

* **Component Source Code:** [BitBasicList.razor on GitHub](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Lists/BasicList/BitBasicList.razor)
* **Demo Page Source Code:** [BitBasicListDemo.razor on GitHub](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Lists/BasicList/BitBasicListDemo.razor)
* **Project Issues:** [File an Issue on GitHub](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Project Discussions:** [Start a Discussion on GitHub](https://github.com/bitfoundation/bitplatform/discussions/new/choose)

This Markdown file provides:

1.  **Clear Structure:** Uses headings and subheadings (`#`, `##`, `###`) for easy navigation.
2.  **Concise Overview:** Explains the component's purpose upfront.
3.  **Feature Highlights:** Lists key capabilities.
4.  **Code Examples:** Includes well-formatted `cshtml` and `csharp` code blocks for common use cases (Basic, Virtualization, ItemsProvider, Grouping, Styling, RTL).
5.  **Explanations:** Describes *why* and *how* to use features like virtualization and `ItemsProvider`.
6.  **API Documentation:** Presents parameters and enums in clear Markdown tables.
7.  **Best Practices:** Offers tips for effective use.
8.  **Links:** Provides direct links to relevant source code and feedback channels.

An AI agent using this file should be able to understand the `BitBasicList` component's capabilities, parameters, and common usage patterns, enabling it to provide relevant code suggestions and explanations.
