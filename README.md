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

- 🖱️ **Right-click Integration**: Open any link in a Quick Tab via context menu
- 📱 **Floating Windows**: Draggable containers that stay on top
- 🎨 **Dual Themes**: Dark and light theme support
- 📋 **Smart Taskbar**: Collapsible taskbar to manage multiple Quick Tabs
- ⚡ **Animations**: Smooth transitions and hover effects
- 🔧 **Customizable**: Configurable sizes, limits, and behavior
- 🎯 **Keyboard Shortcuts**: Quick access via customizable hotkeys

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
3. Add `preferences.json` to configure settings via Sine or manually
4. Clear Startup Cache and restart browser

## Usage

1. **Opening Quick Tabs**: Right-click any link → "Open Quick Tab"
2. **Managing Windows**: 
   - Drag the header to move
   - Use resize handle (bottom-right) to resize
   - Minimize/Close buttons in header
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
