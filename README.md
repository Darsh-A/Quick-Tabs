# Quick Tabs for Zen Browser

A user script that allows you to open links in floating tab containers directly within the Zen browser.

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
extensions.quicktabs.taskbar.trigger = "hover"
extensions.quicktabs.context_menu.access_key = "T"
extensions.quicktabs.maxContainers = 5
extensions.quicktabs.defaultWidth = 400
extensions.quicktabs.defaultHeight = 500
extensions.quicktabs.taskbar.minWidth = 200
extensions.quicktabs.animations.enabled = true
```

## Contributing

Issues and suggestions welcome! This extension is designed for the Zen Browser ecosystem and leverages Firefox's XUL capabilities.

## License

MIT License - Feel free to modify and redistribute. <3
