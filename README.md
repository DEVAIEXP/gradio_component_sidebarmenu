# `gradio-sidebar-menu`
<img alt="Static Badge" src="https://img.shields.io/badge/version%20-%200.0.1%20-%20blue">  
<a href="https://huggingface.co/spaces/elismasilva/gradio_sidebar_menu"><img src="https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Demo-blue"></a>  
<span>💻 <a href='https://github.com/DEVAIEXP/gradio_component_sidebarmenu'>Component GitHub Code</a></span>

Custom sidebar menu component for Gradio apps using `gr.HTML` with Lucide icons, collapsible groups, dynamic routing, and full theme support.

Perfect for dashboards, AI creative tools (like image/model generators), or any Gradio app that needs an elegant, responsive side navigation.

## Features and Key Characteristics

- **Collapsible groups** with persistent state (folders stay open even after navigation)
- **Custom colored icons** via Lucide (colors defined in `menu_data`)
- **Light/dark theme support** (uses Gradio's native `--` CSS variables)
- **Animated toggle button** with smooth rotating arrow (< >)
- **Flexible position** (left/right) with correct borders on both sides
- **Responsive** — auto-closes on mobile when selecting an item
- **Events** — `change` (navigation)
- **No extra dependencies** beyond Gradio + Lucide CDN

## Installation

```bash
pip install gradio-sidebar-menu
```

## Usage
```py
import gradio as gr
from gradio_sidebar_menu import SidebarMenu

menu_data = [
    {"type": "item", "id": "dash", "label": "Dashboard", "icon": "layout-dashboard", "color": "#10b981"},
    {"type": "group", "label": "Train", "icon": "folder", "color": "#f43f5e", "children": [
        {"id": "flux_train", "label": "FLUX Model Trainer", "icon": "dumbbell", "color": "#3b82f6"},
        # ...
    ]},
    # more items...
]

with gr.Blocks() as demo:
    menu = SidebarMenu(
        menu_data=menu_data,
        value="dash",
        open=True,
        position="left",
        width=300
    )
    
    # Your page layout here...
    
demo.launch()
```
Check out the full example in the [Hugging Face demo.](https://huggingface.co/spaces/elismasilva/gradio-sidebar-menu)

| Property | Type | Default | Description |
| :--- | :--- | :--- | :--- |
| `menu_data` | `list[dict]` | **required** | List of menu items. Supports two types: `"type": "item"` and `"type": "group"` with `"children"` array. Each item can have id, label, icon, color. |
| `value` | `str \| None` | `None` | ID of the initially selected/active menu item (highlights with `.active` class). |
| `open` | `bool` | `True` | Whether the sidebar starts open (`True`) or closed (`False`). |
| `position` | `Literal["left", "right"]` | `"left"` | Side of the screen where the sidebar appears. Use `"right"` for right-aligned sidebar. |
| `width` | `int` | `300` | Sidebar width in pixels. |
| `label` | `str \| None` | `None` | Optional label for the component (appears above if set). |
| `visible` | `bool` | `True` | Whether the component is visible. |
| `elem_id` | `str \| None` | `None` | Custom HTML ID for targeting with CSS or JavaScript. |

### Example with all properties

```py
menu = SidebarMenu(
    menu_data=menu_data,
    value="flux_train",                # start with FLUX Trainer selected
    open=False,                        # start closed
    position="right",                  # sidebar on the right side
    width=300,                         # narrower sidebar
    label="Navigation Menu",           # optional title
    visible=True,
    elem_id="custom-sidebar",
    elem_classes=["my-custom-class"]
)
```

### Events

| Event Name | Description |
| :--- | :--- |
| `change` | Triggered when user selects a menu item. Returns the selected item's id. |

```py
menu.change(fn=update_page, inputs=menu, outputs=[page_container])
```

### License
Apache 2.0