# High-Performance 2D Card UI System for Unreal Engine 5

A flexible, data-driven system for creating interactive 2D card UIs with advanced, performance-first visual effects. This plugin project serves as a showcase of professional architecture for UMG and material design in Unreal Engine.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## Key Features Showcase

This system is built for stunning visual effects without sacrificing performance. All effects are driven by a single, powerful, and highly-customizable master material.

| Dissolve / Burn Effect | Interactive Hover & Shake | Procedural Glow & Layout |
| :---: | :---: | :---: |
| ![Image](https://github.com/user-attachments/assets/92e62cdc-db2e-421d-925b-33ab9b8f237f) | ![Image](https://github.com/user-attachments/assets/40bc2cc8-439a-430e-b938-e5fd5b2c13c8) | ![Image](https://github.com/user-attachments/assets/92e62cdc-db2e-421d-925b-33ab9b8f237f) |

**[>> Watch Full Video Showcase on YouTube <<](YOUR_YOUTUBE_LINK_HERE)**

---

## Core Concepts & Implemented Techniques

*   **🎨 Advanced Material-Driven VFX:**
    *   **Procedural Dissolve:** A highly customizable "burn" effect with an emissive edge, controlled by a single material parameter.
    *   **Interactive Shake & Glow:** Responds to player interaction with a material-based shake and a soft procedural glow on hover.
    *   **ID Mask ("Clown Mask") Layout:** The entire card layout (frame, icon area, title background) is defined by a single color-coded texture, allowing for radical design changes by just editing one image.
    *   **UV Remapping & Pseudo-Fresnel:** Implements advanced material math to correctly fit textures into masked areas and to generate a border glow compatible with UI and Bloom.

*   **🚀 High-Performance by Design:**
    *   **Tick-Free Animations:** All animations (hover, dissolve, etc.) are driven by timers and interpolation (`FInterp To`), not Event Tick, ensuring updates only happen when needed.
    *   **Optimized Shaders:** The material is built for performance, with complex logic encapsulated in reusable Material Functions for a clean and efficient graph.

*   **⚙️ Data-Driven Architecture:**
    *   **Data Assets are King:** All card data (title, description, cost, icons) is stored in `PrimaryDataAsset`s. Create and balance new cards without ever touching a Blueprint widget.
    *   **Widget Factory (`WBP_Deck`):** This central widget acts as a factory, dynamically spawning and populating card widgets from an array of Data Assets. It uses a `Wrap Box` for a responsive, flexible layout.

---

## Installation & Setup

You have two options to use this system in your own project.

### Option 1: Download Release (Recommended)

This is the easiest way to get started. You get a clean, ready-to-use plugin without any git history.

1.  Go to the [**Releases page**](https://github.com/GetBoros/GBLabProgressionSystem/releases).
2.  Download the `.zip` file from the latest release (e.g., `GBLabProgressionSystem-v1.0.0.zip`).
3.  In your Unreal Engine project's root folder, create a folder named `Plugins` if it doesn't already exist.
4.  **Unzip the downloaded file** into the `Plugins` folder. The final path should look like this: `YourProject/Plugins/GBLabProgressionSystem/`.
5.  Launch your project. Unreal Engine will prompt you to build the plugin; agree and proceed.

### Option 2: Clone as a Plugin (For Developers)

Use this method if you want to contribute or follow the development history.

1.  Navigate to your Unreal Engine project's root folder.
2.  Create a folder named `Plugins` if it doesn't already exist.
3.  Open a terminal or command prompt inside the `Plugins` folder and run the following command:
    ```bash
    git clone https://github.com/GetBoros/GBLabProgressionSystem.git
    ```
4.  Launch your project. Unreal Engine will prompt you to build the plugin; agree and proceed.

### How to Use the Demo

After installing the plugin:
1.  Set your project's `GameMode` to use the `BP_HUD` class provided in the plugin.
2.  Create a `WBP_Deck` widget in your level (or use the provided Demo Map).
3.  Populate the `Cards In Deck` array on the `WBP_Deck` instance with the example `DA_Card_...` assets.
4.  Press Play.

---

## Future Plans

This is an ongoing learning project. Future development plans include:
- **Polishing the 3D Actor System (`BP_Card`):** Integrating the material baking pipeline to create a fully performant 3D version of the cards.
- **Drag-and-Drop Functionality:** Implementing interactive card dragging.
- **Refining Animations with Curves:** Using Curve assets for more nuanced animation easing.
