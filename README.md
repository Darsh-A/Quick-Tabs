# Quick Tabs for Zen Browser

A user script that allows you to open links in floating tab containers directly within the Zen browser.



https://github.com/user-attachments/assets/fdbda5ac-aa4b-448e-b1df-56f4f1a79f0b



## Purpose

Quick Tabs provides a unique way to browse multiple websites simultaneously without cluttering your main tab bar. Perfect for:

- **Research & Comparison**: View multiple sources side-by-side
- **Multitasking**: Keep reference materials open while working
- **Content Creation**: Monitor social media, docs, and tools simultaneously
- **Shopping**: Compare products across different sites
- **Development**: Test sites while referencing documentation

## Features

- **Right-Click Menu Integration**:
  - Open links in Quick Tabs directly from the context menu
  - Convert existing tabs to Quick Tabs via right-click options
- **Drag-and-Drop Links**:
  - Drag any link onto the Quick Tabs taskbar to open it in a new Quick Tab. The taskbar dynamically appears when a link is dragged over the window, even if no Quick Tabs are open.
- **Renamable Titles**:
  - Double-click on a Quick Tab's title to customize its name. Renamed titles persist and are not overwritten by page changes.
- **Zen Command Palette Integration**:
  - Access Quick Tabs commands (e.g., close all, minimize all, expand/minimize specific tabs) directly from the [Zen Command Palette](https://github.com/BibekBhusal0/zen-custom-js).
- **Quick Search Integration (Coming Soon)**:
  - Open the Quick Search result in a Quick Tab

## Installation

### Through Sine (Recommended)

1. Navigate to [Sine](https://github.com/CosmoCreeper/Sine) (Extensions Manager)
2. Search for "Quick Tabs" or import this mod via custom JS
3. Click **Install**
4. **Important**: Clear Startup Cache in browser settings for changes to take effect

OR

1. Paste the github repo link into Sine's custom JS section.

### Manual Installation

1. Download `Quick_Tabs.uc.js` (Make sure [Fx-Autoconfig](https://github.com/MrOtherGuy/fx-autoconfig/) is installed)
2. Place in your Zen profile's `chrome/JS/` directory
3. Add preferences from `preferences.json` to your `about:config` manually
4. Clear Startup Cache and restart browser

## Usage

1. **Opening Quick Tabs**:
   - Right-click any link → "Open Quick Tab"
   - **Drag-and-Drop**: Drag a link from any webpage or application onto the Quick Tabs taskbar (bottom-right of the window). The taskbar will appear dynamically when a link is dragged over the browser window.
2. **Managing Windows**: 
   - Drag the header to move
   - Use resize handle (bottom-right) to resize
   - Minimize/Close buttons in header (this can also be done if through URL bar if you have Zen Command Palette)
   - **Renaming Titles**: Double-click on the Quick Tab's title in its header to edit its name. Press Enter to save or Escape to cancel.
3. **Taskbar**: Hover over the taskbar (bottom-right) to see all Quick Tabs
4. **Switching**: Click taskbar items to focus or restore minimized tabs

## Preferences

All settings can be configured through Sine's preferences panel:

### ⚙️ Appearance Settings
- **Theme**: Choose between Dark and Light themes
- **Animations**: Enable/disable smooth transitions and effects

### 🖱️ Behavior Settings  
- **Taskbar Trigger**: Show taskbar on hover or click
- **Access Key**: Customize the keyboard shortcut (default: T)
- **Initial Position**: Set the default screen position for new Quick Tabs.
  - **Values**: `center`, `top-left`, `top-right`, `bottom-left`, `bottom-right`. (Aliases like `left-top` are also supported).
- **Command Palette Dynamic commands**: Generate dynamic commands (like close/minimize/expand x quick tab) for Zen Command Palette.

### 📏 Size & Limits
- **Max Containers**: Maximum number of Quick Tabs allowed (default: 5)
- **Default Width**: Starting width for new containers (default: 400px)
- **Default Height**: Starting height for new containers (default: 500px)
- **Taskbar Min Width**: Minimum width for the taskbar (default: 200px)

## Default Preferences

```js
extensions.quicktabs.theme = "dark"
extensions.quicktabs.taskbar.trigger = "hover" // or "click"
extensions.quicktabs.context_menu.access_key = "T"
extensions.quicktabs.maxContainers = 5
extensions.quicktabs.defaultWidth = 400
extensions.quicktabs.defaultHeight = 500
extensions.quicktabs.taskbar.minWidth = 200
extensions.quicktabs.animations.enabled = true
extensions.quicktabs.initialPosition = "center" // e.g., "top-left", "bottom-right"
extensions.quicktabs.commandpalette.dynamic.enabled = true
```

## API Reference

Quick Tabs exposes a global `window.QuickTabs` API for programmatic access and integration with other scripts.

### Methods

#### `QuickTabs.openQuickTab(url, title?)`
Creates and opens a new Quick Tab container with the specified URL.

**Parameters:**
- `url` (string, required) - The URL to load in the Quick Tab
- `title` (string, optional) - Custom title for the container (defaults to auto-generated from URL)

**Returns:** Container object if successful, `false` if failed

**Example:**
```javascript
// Open a Quick Tab with auto-generated title
QuickTabs.openQuickTab('https://github.com');

// Open with custom title
QuickTabs.openQuickTab('https://github.com', 'GitHub');
```

#### `QuickTabs.openQuickTabFromCurrent()`
Creates a Quick Tab from the currently active browser tab.

**Returns:** Container object if successful, `false` if failed

**Example:**
```javascript
// Clone current tab into a Quick Tab
QuickTabs.openQuickTabFromCurrent();
```

#### `QuickTabs.triggerOpenQuickTab(url, title?)`
Triggers the Quick Tab command through the browser's command system (alternative method).

**Parameters:**
- `url` (string, required) - The URL to load
- `title` (string, optional) - Custom title for the container

**Example:**
```javascript
QuickTabs.triggerOpenQuickTab('https://example.com', 'Example Site');
```

#### `QuickTabs.triggerOpenQuickTabFromCurrent()`
Triggers the "open from current tab" command through the browser's command system.

**Example:**
```javascript
QuickTabs.triggerOpenQuickTabFromCurrent();
```

#### `QuickTabs.getContainerInfo()`
Returns information about all active Quick Tab containers.

**Returns:** Object with container statistics and details
```javascript
{
  count: 3,              // Current number of open containers
  maxContainers: 5,      // Maximum allowed containers
  containers: [          // Array of container details
    {
      id: 1,
      url: "https://github.com",
      title: "GitHub",
      minimized: false
    },
    // ... more containers
  ]
}
```

### Command System

Quick Tabs also exposes browser commands that can be triggered through Zen Browser's command system or other extensions.

#### Available Commands

##### `cmd_zenOpenQuickTab`
Opens a Quick Tab using data from `quickTabCommandData` (set via `triggerOpenQuickTab`).

**Usage:**
```javascript
// Set data first
QuickTabs.triggerOpenQuickTab('https://example.com', 'Example');

// Or trigger directly
const command = document.querySelector('#cmd_zenOpenQuickTab');
if (command) {
    const event = new Event('command', { bubbles: true });
    command.dispatchEvent(event);
}
```

##### `cmd_zenOpenQuickTabFromCurrent`
Opens a Quick Tab from the currently active browser tab.

**Usage:**
```javascript
// Trigger via API (recommended)
QuickTabs.triggerOpenQuickTabFromCurrent();

// Or trigger directly
const command = document.querySelector('#cmd_zenOpenQuickTabFromCurrent');
if (command) {
    const event = new Event('command', { bubbles: true });
    command.dispatchEvent(event);
}
```


## Contributing

Issues and suggestions welcome! This extension is designed for the Zen Browser ecosystem and leverages Firefox's XUL capabilities.

## License

MIT License - Feel free to modify and redistribute. <3
