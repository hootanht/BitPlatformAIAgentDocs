# BitPersona Component

**Purpose:** This document provides a structured reference for the `BitPersona` Blazor component (also known as Avatar). Use this information to understand its functionality, properties (like size, text fields, presence, image handling), templating options, styling, and how to implement it effectively in CSHTML (`.razor`) files.

**How to Use:**
1.  **Understand the Goal:** Read the "Overview" to grasp the component's purpose – representing a person visually.
2.  **See Examples:** Refer to the "Usage Examples" section for practical code snippets demonstrating various features (basic usage, sizes, colors, shapes, actions, presence status, initials, templates, styling, RTL). Copy and adapt these examples.
3.  **Check Properties:** Consult the "API" section for a detailed list of available parameters (`@attributes` in Blazor), their types, default values, and descriptions. This is crucial for configuration and customization.
4.  **Render Fragments/Templates:** Note the use of templates like `<PrimaryTextTemplate>`, `<CoinTemplate>`, `<ImageOverlayTemplate>`, etc., for advanced customization (Example 9).
5.  **Styling:** Look at the "Style & Class" example and the `BitPersonaClassStyles` in the API section to understand how to apply custom CSS.
6.  **Enums:** Check the "Enums" subsection in the API for valid values for parameters like `Size`, `Color`, `Variant`, `Shape`, `Presence`, and `Dir`.

---

## Overview

The `BitPersona` component is a visual representation of a person, often used across products. It typically showcases an image (avatar) chosen by the person or their initials on a colored background (coin). It can display the person's name (primary text), role or secondary info (secondary text), status (tertiary text), additional details (optional text), and online presence status. It's a foundational component used in controls like PeoplePicker and Facepile.

*(Related terms: Avatar)*

---

## Usage Examples

This section demonstrates common ways to use the `BitPersona` component.

### 1. Basic Usage

Displays a Persona with initials, an image, or as an "unknown" placeholder.

```cshtml
@* Persona with Initials (default if no ImageUrl) *@
<BitPersona PrimaryText="Saleh Khafan" Size="BitPersonaSize.Size72" />

@* Persona with Image *@
<BitPersona PrimaryText="Annie Lindqvist" @* PrimaryText provides context and initials fallback *@
            Size="BitPersonaSize.Size72"
            ImageUrl="/images/persona/persona-female.png" />

@* Unknown Persona Placeholder *@
<BitPersona PrimaryText="Unknown"
            SecondaryText="Developer"
            Size="BitPersonaSize.Size72"
            Unknown /> @* Sets specific styling and icon for unknown state *@
```

### 2. Size

Control the overall size of the Persona, affecting both the coin (image/initials area) and text. `CoinSize` can override the default coin dimension for a given `Size`.

*Description:* Use the `Size` parameter with `BitPersonaSize` enum values. Use `CoinSize` (in pixels) for custom coin dimensions. `HidePersonaDetails` can hide text fields, showing only the coin.

```cshtml
<BitCheckbox @bind-Value="isDetailsShown" Label="Include BitPersona details" />

@* Various standard sizes *@
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Secondary" Size="BitPersonaSize.Size8"   HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Secondary" Size="BitPersonaSize.Size24"  HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Secondary" Size="BitPersonaSize.Size32"  HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Size="BitPersonaSize.Size40"  HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Size="BitPersonaSize.Size48"  HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Size="BitPersonaSize.Size56"  HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" TertiaryText="In a meeting" Size="BitPersonaSize.Size72"  HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" TertiaryText="Off" OptionalText="Available at 4:00pm" Size="BitPersonaSize.Size100" HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" TertiaryText="In a meeting" OptionalText="Available at 4:00pm" Size="BitPersonaSize.Size120" HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />

@* Custom CoinSize (overrides Size120's default coin dimension) *@
<BitPersona CoinSize="150" PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" TertiaryText="In a meeting" OptionalText="Available at 4:00pm" Size="BitPersonaSize.Size120" HidePersonaDetails="!isDetailsShown" ImageUrl="/images/persona/persona-female.png" />
```

```csharp
@code {
    private bool isDetailsShown = true;
}
```

### 3. Color (Coin Color)

Set the background color of the coin when initials are displayed (no `ImageUrl` or image failed to load).

*Description:* Use the `CoinColor` parameter with a `BitColor` enum value.

```cshtml
<BitPersona PrimaryText="Primary" CoinColor="BitColor.Primary" />
<BitPersona PrimaryText="Secondary" CoinColor="BitColor.Secondary" />
<BitPersona PrimaryText="Tertiary" CoinColor="BitColor.Tertiary" />
<BitPersona PrimaryText="Info" SecondaryText="(default)" CoinColor="BitColor.Info" />
<BitPersona PrimaryText="Success" CoinColor="BitColor.Success" />
<BitPersona PrimaryText="Warning" CoinColor="BitColor.Warning" />
<BitPersona PrimaryText="SevereWarning" CoinColor="BitColor.SevereWarning" />
<BitPersona PrimaryText="Error" CoinColor="BitColor.Error" />

@* Theme-aware background/foreground/border colors *@
<BitPersona PrimaryText="PrimaryBackground" CoinColor="BitColor.PrimaryBackground" />
<BitPersona PrimaryText="SecondaryBackground" CoinColor="BitColor.SecondaryBackground" />
<BitPersona PrimaryText="TertiaryBackground" CoinColor="BitColor.TertiaryBackground" />
<BitPersona PrimaryText="PrimaryForeground" CoinColor="BitColor.PrimaryForeground" />
<BitPersona PrimaryText="SecondaryForeground" CoinColor="BitColor.SecondaryForeground" />
<BitPersona PrimaryText="TertiaryForeground" CoinColor="BitColor.TertiaryForeground" />
<BitPersona PrimaryText="PrimaryBorder" CoinColor="BitColor.PrimaryBorder" />
<BitPersona PrimaryText="SecondaryBorder" CoinColor="BitColor.SecondaryBorder" />
<BitPersona PrimaryText="TertiaryBorder" CoinColor="BitColor.TertiaryBorder" />
```

### 4. Variant (Coin Variant)

Apply different visual styles to the coin: `Fill` (default), `Outline`, or `Text`.

*Description:* Use the `CoinVariant` parameter with a `BitVariant` enum value.

```cshtml
<BitPersona PrimaryText="Saleh Xafan" SecondaryText="Developer" Size="BitPersonaSize.Size72" CoinVariant="BitVariant.Fill" />
<BitPersona PrimaryText="Saleh Xafan" SecondaryText="Developer" Size="BitPersonaSize.Size72" CoinVariant="BitVariant.Outline" />
<BitPersona PrimaryText="Saleh Xafan" SecondaryText="Developer" Size="BitPersonaSize.Size72" CoinVariant="BitVariant.Text" />
```

### 5. Shape (Coin Shape)

Set the shape of the coin to `Circular` (default) or `Square`.

*Description:* Use the `CoinShape` parameter with a `BitPersonaCoinShape` enum value.

```cshtml
<BitPersona PrimaryText="Saleh Xafan" SecondaryText="Developer" Size="BitPersonaSize.Size72" CoinShape="BitPersonaCoinShape.Circular" ImageUrl="/images/persona/persona-female.png" />
<BitPersona PrimaryText="Saleh Xafan" SecondaryText="Developer" Size="BitPersonaSize.Size72" CoinShape="BitPersonaCoinShape.Square" ImageUrl="/images/persona/persona-female.png" />
```

### 6. Action (Click Handlers)

Handle clicks on the image/coin itself or on a custom action icon that appears on hover.

*Description:* Use `OnImageClick` for clicks on the main coin/image area. Use `OnActionClick` along with `ActionIconName` to add a hover action button.

```cshtml
@* Custom Action Button on Hover *@
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" TertiaryText="In a meeting" OptionalText="Available at 4:00pm"
            Size="BitPersonaSize.Size120" Presence="BitPersonaPresence.None"
            OnActionClick="() => actionClickCount++" ActionIconName="@BitIconName.CloudUpload"
            ImageUrl="/images/persona/persona-female.png" />
<p>Action Click Count: @actionClickCount</p>

@* Clickable Image/Coin *@
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" TertiaryText="In a meeting" OptionalText="Available at 4:00pm"
            Size="BitPersonaSize.Size120" Presence="BitPersonaPresence.Online"
            OnImageClick="() => imageClickCount++"
            ImageUrl="/images/persona/persona-female.png" />
<p>Image Click Count: @imageClickCount</p>
```

```csharp
@code {
    private int imageClickCount = 0;
    private int actionClickCount = 0;
}
```

### 7. Initials

Control how initials are displayed when an image isn't available or loading.

*Description:* Initials are generated automatically from `PrimaryText`. Use `ImageInitials` to override. `ShowInitialsUntilImageLoads` displays initials while a valid `ImageUrl` is loading.

```cshtml
@* Show initials because ImageUrl is invalid/not found *@
<BitPersona PrimaryText="Saleh Khafan" Size="BitPersonaSize.Size72" ShowInitialsUntilImageLoads ImageUrl="invalid-src" />

@* Show initials because no ImageUrl is provided *@
<BitPersona Size="BitPersonaSize.Size72" PrimaryText="Saleh Xafan" />

@* Override automatically generated initials with ImageInitials *@
<BitPersona Size="BitPersonaSize.Size72" PrimaryText="Saleh Khafan" ImageInitials="S" />
```

### 8. PersonaPresence

Display the online status of the person.

*Description:* Use the `Presence` parameter with a `BitPersonaPresence` enum value. Customize icons using `PresenceIcons`.

```cshtml
<div>None</div>
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Presence="BitPersonaPresence.None"   PresenceIcons="_icons" Size="BitPersonaSize.Size120" ImageUrl="/images/persona/persona-female.png" />

<div>Offline</div>
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Presence="BitPersonaPresence.Offline" PresenceIcons="_icons" Size="BitPersonaSize.Size120" ImageUrl="/images/persona/persona-female.png" />

<div>Online</div>
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Presence="BitPersonaPresence.Online"  PresenceIcons="_icons" Size="BitPersonaSize.Size120" ImageUrl="/images/persona/persona-female.png" />

<div>Away</div>
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Presence="BitPersonaPresence.Away"    PresenceIcons="_icons" Size="BitPersonaSize.Size120" ImageUrl="/images/persona/persona-female.png" />

<div>Do not Disturb (Dnd)</div>
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Presence="BitPersonaPresence.Dnd"     PresenceIcons="_icons" Size="BitPersonaSize.Size120" ImageUrl="/images/persona/persona-female.png" />

<div>Blocked</div>
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Presence="BitPersonaPresence.Blocked" PresenceIcons="_icons" Size="BitPersonaSize.Size120" ImageUrl="/images/persona/persona-female.png" /> @* Note: _icons dictionary might not include Blocked as per example code *@

<div>Busy</div>
<BitPersona PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Presence="BitPersonaPresence.Busy"    PresenceIcons="_icons" Size="BitPersonaSize.Size120" ImageUrl="/images/persona/persona-female.png" />
```

```csharp
@code {
    private Dictionary<BitPersonaPresence, string> _icons = new()
    {
        { BitPersonaPresence.Offline, BitIconName.UnavailableOffline },
        { BitPersonaPresence.Online, BitIconName.SkypeCheck },
        { BitPersonaPresence.Away, BitIconName.SkypeClock },
        { BitPersonaPresence.Dnd, BitIconName.SkypeMinus },
        { BitPersonaPresence.Blocked, BitIconName.BlockedSolid }, // Example shows default icon if not in dict
        { BitPersonaPresence.Busy, BitIconName.Blocked2Solid }
    };
}
```

### 9. Templates

Provide custom RenderFragments to override default rendering for various parts of the Persona.

*Description:* Use templates like `<PrimaryTextTemplate>`, `<SecondaryTextTemplate>`, `<CoinTemplate>`, `<ImageOverlayTemplate>` etc., to insert custom HTML and components.

```html
<style>
    .custom-ico { font-size: 14px; margin-right: 5px; }
    .custom-coin { display: block; border-radius: 20px; }
</style>
```

```cshtml
@* Text Field Templates and Image Overlay Template *@
<BitPersona Size="BitPersonaSize.Size100" ImageUrl="/images/persona/persona-female.png" OnImageClick="() => {}">
    <PrimaryTextTemplate>
        <BitIcon IconName="@BitIconName.Contact" Class="custom-ico" /> Annie Lindqvist
    </PrimaryTextTemplate>
    <SecondaryTextTemplate>
        <BitIcon IconName="@BitIconName.Suitcase" Class="custom-ico" /> Software Engineer
    </SecondaryTextTemplate>
    <TertiaryTextTemplate>
        <BitIcon IconName="@BitIconName.JoinOnlineMeeting" Class="custom-ico" /> In a meeting
    </TertiaryTextTemplate>
    <OptionalTextTemplate>
        <BitIcon IconName="@BitIconName.Clock" Class="custom-ico" /> Available at 7:00pm
    </OptionalTextTemplate>
    <ImageOverlayTemplate>
        <BitIcon IconName="@BitIconName.Edit" Class="custom-ico" /> Edit image
    </ImageOverlayTemplate>
</BitPersona>

@* Coin Template (completely overrides default coin rendering) *@
<BitPersona Size="BitPersonaSize.Size100" PrimaryText="Annie Lindqvist" SecondaryText="Software Engineer" Presence="BitPersonaPresence.Online" CoinVariant="BitVariant.Text">
    <CoinTemplate>
        <img src="/images/persona/persona-female.png" width="100px" height="100px" class="custom-coin" />
    </CoinTemplate>
</BitPersona>
```

### 10. Style & Class Customization

Apply custom CSS styles and classes to the Persona and its internal elements.

*Description:* Use standard `Style` and `Class` attributes for the root element. Use the `Styles` and `Classes` parameters (which accept a `BitPersonaClassStyles` object) to target specific internal parts like the image container (`ImageContainer`), text fields (`PrimaryTextContainer`, etc.).

```html
<style>
    .custom-class { /* Applied via Class attribute */
        padding: 1rem;
        box-shadow: #3d3226 0 0 1rem;
        border-radius: 1rem;
    }

    /* Applied via Classes parameter */
    .custom-img-container {
        color: #ff6a00;
        background-color: #f2cd01;
    }
    .custom-primary-text {
        color: #b6ff00;
        font-weight: bold;
        font-style: italic;
    }
</style>
```

```cshtml
@* Using Style attribute on root *@
<BitPersona PrimaryText="Saleh Khafan" Size="BitPersonaSize.Size72" Style="padding: 1rem; background: gray; border-radius: 1rem;" />

@* Using Class attribute on root *@
<BitPersona PrimaryText="Saleh Khafan" Size="BitPersonaSize.Size72" Class="custom-class" />

@* Using Styles parameter for internal elements *@
<BitPersona PrimaryText="Saleh Khafan" Size="BitPersonaSize.Size72"
            Styles="@(new() { ImageContainer = "color: #b6ff00; background-color: #00ff90;",
                              PrimaryTextContainer = "color: #ea1919; font-weight: bold; font-style: italic;" })" />

@* Using Classes parameter for internal elements *@
<BitPersona PrimaryText="Saleh Khafan" Size="BitPersonaSize.Size72"
            Classes="@(new() { ImageContainer = "custom-img-container",
                               PrimaryTextContainer = "custom-primary-text" })" />
```

### 11. RTL (Right-to-Left)

Render the Persona correctly for right-to-left languages.

*Description:* Set the `Dir` parameter to `BitDir.Rtl`.

```cshtml
<div dir="rtl"> @* Parent div sets context for example layout *@
    <BitPersona Dir="BitDir.Rtl"
                PrimaryText="صالح یوسف نژاد"
                SecondaryText="مهندس نرم افزار"
                Size="@BitPersonaSize.Size56" />
</div>
```

---

## API

This section details the parameters (properties) available for the `BitPersona` component.

### Parameters (BitPersona)

| Name                      | Type                            | Default Value         | Description                                                                                                                               |
| ------------------------- | ------------------------------- | --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| `ActionButtonTitle`     | `string`                        | `"Edit image"`        | The title (tooltip) for the action button shown on hover (if `ActionIconName` or `ActionTemplate` is used).                               |
| `ActionIconName`        | `string?`                       | `null`                | Icon name (from `BitIconName`) for the custom action button. Providing this enables the action button feature.                              |
| `ActionTemplate`        | `RenderFragment?`               | `null`                | Optional custom template (`RenderFragment`) for the action button element. Overrides `ActionIconName` if provided.                        |
| `Classes`                 | `BitPersonaClassStyles?`        | `null`                | Custom CSS classes for different internal parts. See `BitPersonaClassStyles` below.                                                       |
| `CoinColor`               | `BitColor?`                     | `null`                | Background color for the coin when initials are displayed. See `BitColor` enum below.                                                       |
| `CoinShape`               | `BitPersonaCoinShape?`          | `null`                | Shape of the coin (Circular or Square). See `BitPersonaCoinShape` enum below. Default: `Circular`.                                        |
| `CoinSize`                | `int?`                          | `null`                | Custom size for the coin in pixels. Overrides the default coin size associated with the `Size` parameter.                                 |
| `CoinTemplate`            | `RenderFragment?`               | `null`                | Custom template (`RenderFragment`) for the entire coin area. Overrides default image/initials rendering.                                  |
| `CoinVariant`             | `BitVariant?`                   | `null`                | Visual variant for the coin (Fill, Outline, Text). See `BitVariant` enum below. Default: `Fill`.                                          |
| `HidePersonaDetails`      | `bool`                          | `false`               | If true, only the coin (image/initials) is rendered, hiding all text details.                                                             |
| `ImageAlt`                | `string?`                       | `null`                | Alt text for the persona image.                                                                                                           |
| `ImageInitials`           | `string?`                       | `null`                | Initials to display in the coin if no `ImageUrl` is provided or image fails to load. Overrides automatically generated initials.          |
| `ImageOverlayTemplate`    | `RenderFragment?`               | `null`                | Custom template (`RenderFragment`) for the overlay shown on hover when `OnImageClick` is provided.                                        |
| `ImageOverlayText`        | `string?`                       | `"Edit image"`        | Text for the default image overlay shown on hover when `OnImageClick` is provided (if `ImageOverlayTemplate` is not used).              |
| `ImageUrl`                | `string?`                       | `null`                | URL of the persona image. If not provided or invalid, initials will be shown.                                                             |
| `OnActionClick`           | `EventCallback<MouseEventArgs>` | (none)                | Callback invoked when the custom action button is clicked.                                                                                |
| `OnImageClick`            | `EventCallback<MouseEventArgs>` | (none)                | Callback invoked when the main coin/image area is clicked. Enables the image overlay on hover.                                            |
| `OptionalText`            | `string?`                       | `null`                | Optional text (e.g., availability). Only visible for `Size100` and `Size120`.                                                             |
| `OptionalTextTemplate`    | `RenderFragment?`               | `null`                | Custom template (`RenderFragment`) for the optional text area.                                                                            |
| `Presence`                | `BitPersonaPresence`            | `BitPersonaPresence.None` | Presence status to display (Online, Offline, Away, etc.). See `BitPersonaPresence` enum below.                                          |
| `PresenceIcons`           | `Dictionary<BitPersonaPresence, string>?` | `null`       | Dictionary mapping presence statuses to custom icon names (from `BitIconName`).                                                            |
| `PresenceTitle`           | `string?`                       | `null`                | Title (tooltip) for the presence indicator.                                                                                               |
| `PrimaryText`             | `string?`                       | `null`                | Main text, usually the person's name. Used to generate initials if `ImageInitials` is not set.                                            |
| `PrimaryTextTemplate`     | `RenderFragment?`               | `null`                | Custom template (`RenderFragment`) for the primary text area.                                                                             |
| `SecondaryText`           | `string?`                       | `null`                | Secondary text, usually the person's role or title.                                                                                       |
| `SecondaryTextTemplate`   | `RenderFragment?`               | `null`                | Custom template (`RenderFragment`) for the secondary text area.                                                                           |
| `ShowInitialsUntilImageLoads` | `bool`                    | `false`               | If true and `ImageUrl` is provided, initials are shown while the image is loading.                                                          |
| `Size`                    | `string?`                       | `null`                | Overall size of the Persona control. Use `BitPersonaSize` constants. Default: `Size48`.                                                     |
| `Styles`                  | `BitPersonaClassStyles?`        | `null`                | Custom CSS styles for different internal parts. See `BitPersonaClassStyles` below.                                                        |
| `TertiaryText`            | `string?`                       | `null`                | Tertiary text, usually status message. Only visible for `Size72`, `Size100`, and `Size120`.                                              |
| `TertiaryTextTemplate`    | `RenderFragment?`               | `null`                | Custom template (`RenderFragment`) for the tertiary text area.                                                                            |
| `Unknown`                 | `bool`                          | `false`               | If true, renders a special 'unknown' state with a '?' icon and fixed colors, ignoring `ImageUrl` and `ImageInitials`.                     |

### Parameters (Inherited from BitComponentBase)

| Name             | Type                            | Default Value                      | Description                                                                                     |
| ---------------- | ------------------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                       | `null`                             | The aria-label of the control for screen readers.                                               |
| `Class`          | `string?`                       | `null`                             | Custom CSS class for the root element of the component.                                         |
| `Dir`            | `BitDir?`                       | `null`                             | Determines the component direction (Ltr, Rtl, Auto).                                            |
| `HtmlAttributes` | `Dictionary<string, object>`    | `new Dictionary<string, object>()` | Capture and render additional HTML attributes on the root element.                              |
| `Id`             | `string?`                       | `null`                             | Custom id attribute for the root element. If null, a unique ID (`UniqueId`) will be used.       |
| `IsEnabled`      | `bool`                          | `true`                             | Whether or not the component is enabled (affects click handlers).                             |
| `Style`          | `string?`                       | `null`                             | Custom CSS style for the root element of the component.                                         |
| `Visibility`     | `BitVisibility`                 | `BitVisibility.Visible`            | Whether the component is `Visible`, `Hidden` (takes space), or `Collapsed` (takes no space). |

### Class Styles (BitPersonaClassStyles)

Used with the `Classes` and `Styles` parameters to target specific elements within the component.

| Name                   | Type      | Description                                                              |
| ---------------------- | --------- | ------------------------------------------------------------------------ |
| `Root`                 | `string?` | Custom CSS classes/styles for the root `<div>` element.                  |
| `CoinContainer`        | `string?` | Custom CSS classes/styles for the `<div>` containing the coin elements.    |
| `PresentationIcon`     | `string?` | Custom CSS classes/styles for the `<i>` icon in the coin container.        |
| `Presentation`         | `string?` | Custom CSS classes/styles for the role=presentation `<div>`.              |
| `ImageContainer`       | `string?` | Custom CSS classes/styles for the `<div>` holding the image/initials.     |
| `UnknownIcon`          | `string?` | Custom CSS classes/styles for the '?' icon in `Unknown` mode.            |
| `ImageOverlay`         | `string?` | Custom CSS classes/styles for the overlay `<div>` shown on image hover.   |
| `ImageOverlayText`     | `string?` | Custom CSS classes/styles for the `<span>` within the image overlay.      |
| `Initials`             | `string?` | Custom CSS classes/styles for the initials `<span>`.                      |
| `Image`                | `string?` | Custom CSS classes/styles for the `<img>` element.                       |
| `ActionButton`         | `string?` | Custom CSS classes/styles for the action `<button>` element.              |
| `ActionButtonIcon`     | `string?` | Custom CSS classes/styles for the action button's icon `<i>`.            |
| `Presence`             | `string?` | Custom CSS classes/styles for the presence indicator `<div>`.            |
| `DetailsContainer`     | `string?` | Custom CSS classes/styles for the `<div>` containing all text details.    |
| `PrimaryTextContainer` | `string?` | Custom CSS classes/styles for the primary text `<div>`.                  |
| `SecondaryTextContainer`| `string?`| Custom CSS classes/styles for the secondary text `<div>`.                |
| `TertiaryTextContainer`| `string?` | Custom CSS classes/styles for the tertiary text `<div>`.                 |
| `OptionalTextContainer`| `string?` | Custom CSS classes/styles for the optional text `<div>`.                 |

### Enums

#### `BitPersonaPresence`

Defines the presence status indicators.

| Name      | Value | Description                |
| --------- | ----- | -------------------------- |
| `None`    | 0     | No presence indicator.     |
| `Offline` | 1     | Offline status.            |
| `Online`  | 2     | Online status.             |
| `Away`    | 3     | Away status.               |
| `Dnd`     | 4     | Do Not Disturb status.     |
| `Blocked` | 5     | Blocked status (no icon).  |
| `Busy`    | 6     | Busy status.               |

#### `BitPersonaSize`

Defines standard sizes for the Persona component. Values are strings matching CSS classes (e.g., "Size48").

| Name      | Value    | Description                  |
| --------- | -------- | ---------------------------- |
| `Size8`   | `"Size8"`  | Renders an 8px coin.         |
| `Size24`  | `"Size24"` | Renders a 24px coin.         |
| `Size32`  | `"Size32"` | Renders a 32px coin.         |
| `Size40`  | `"Size40"` | Renders a 40px coin.         |
| `Size48`  | `"Size48"` | Renders a 48px coin (Default)|
| `Size56`  | `"Size56"` | Renders a 56px coin.         |
| `Size72`  | `"Size72"` | Renders a 72px coin.         |
| `Size100` | `"Size100"`| Renders a 100px coin.        |
| `Size120` | `"Size120"`| Renders a 120px coin.        |

#### `BitPersonaCoinShape`

Defines the shape of the coin.

| Name       | Value      | Description                |
| ---------- | ---------- | -------------------------- |
| `Circular` | `"Circle"` | Round coin shape (Default).|
| `Square`   | `"Square"` | Square coin shape.         |

#### `BitColor`

Defines standard color options, used here for `CoinColor`.

| Name                | Value | Description                  |
| ------------------- | ----- | ---------------------------- |
| `Primary`           | 0     | Primary theme color.         |
| `Secondary`         | 1     | Secondary theme color.       |
| `Tertiary`          | 2     | Tertiary theme color.        |
| `Info`              | 3     | Informational theme color.   |
| `Success`           | 4     | Success theme color.         |
| `Warning`           | 5     | Warning theme color.         |
| `SevereWarning`     | 6     | Severe Warning theme color.  |
| `Error`             | 7     | Error/Danger theme color.    |
| `PrimaryBackground` | 8     | Primary background color.    |
| `SecondaryBackground`| 9     | Secondary background color.  |
| `TertiaryBackground`| 10    | Tertiary background color.   |
| `PrimaryForeground` | 11    | Primary foreground color.    |
| `SecondaryForeground`| 12    | Secondary foreground color.  |
| `TertiaryForeground`| 13    | Tertiary foreground color.   |
| `PrimaryBorder`     | 14    | Primary border color.        |
| `SecondaryBorder`   | 15    | Secondary border color.      |
| `TertiaryBorder`    | 16    | Tertiary border color.       |

#### `BitVariant`

Defines visual styles, used here for `CoinVariant`.

| Name      | Value | Description               |
| --------- | ----- | ------------------------- |
| `Fill`    | 0     | Fill styled variant.      |
| `Outline` | 1     | Outline styled variant.   |
| `Text`    | 2     | Text styled variant.      |

#### `BitVisibility` (from BitComponentBase)

Controls the rendering and visibility of the component.

| Name        | Value | Description                                                                                       |
| ----------- | ----- | ------------------------------------------------------------------------------------------------- |
| `Visible`   | 0     | The component is visible.                                                                         |
| `Hidden`    | 1     | The component is hidden (`visibility: hidden`), but still occupies space in the layout.           |
| `Collapsed` | 2     | The component is hidden (`display: none`) and does not occupy any space in the layout.            |

#### `BitDir` (from BitComponentBase)

Specifies the text directionality.

| Name   | Value | Description                                                                                                |
| ------ | ----- | ---------------------------------------------------------------------------------------------------------- |
| `Ltr`  | 0     | Left-to-right direction.                                                                                   |
| `Rtl`  | 1     | Right-to-left direction.                                                                                   |
| `Auto` | 2     | Lets the browser decide the direction based on the content.                                                |

---

## Feedback

* **GitHub Repo:** [bitfoundation/bitplatform](https://github.com/bitfoundation/bitplatform)
* **File an Issue:** [New Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Start a Discussion:** [New Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose)
* **Component Source Code:** [BitPersona.razor](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Notifications/Persona/BitPersona.razor)