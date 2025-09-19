Modular Card UI System for Unreal Engine

A plugin project demonstrating a fully modular, data-driven, and visually customizable UI system for card-based games, inspired by titles like Vampire Survivors or Slay the Spire.

This project is currently at Version 0.2. Some features may be incomplete and bugs may be present.

![alt text](https://img.shields.io/badge/License-MIT-yellow.svg)

The core philosophy of this system is the strict separation of data, logic, and visuals. Cards are not hard-coded; they are versatile templates populated with data from Data Assets and styled through a powerful, multi-layered Material system.
Quick Start Guide

This system is designed as a self-contained plugin.

    Create a new, empty Unreal Engine project.

    Create a Plugins folder in the project's root directory.

    Clone this repository into the Plugins folder.

    Launch the project. Unreal Engine will prompt to build the plugin; agree and proceed.

    To set up the demo scene:

        In the Content Drawer, create a new Widget Blueprint and name it WBP_Deck.

        Open it, and in the Graph tab, find the Cards_In_Deck variable.

        Populate this array with the example DA_Card_... assets provided in the plugin's content folder.

        Ensure your Level's GameMode is set to use the BP_HUD class included in the plugin.

    Open the main level and press Play.

Key Concepts & Implemented Techniques

This system is the result of a step-by-step implementation of professional UI development techniques in Unreal Engine.
1. Architecture (Data-Driven Design)

    Data Assets (PrimaryDataAsset): All card information (title, description, cost, icons, materials) is stored in individual DA_Card_Base assets. This allows for easy creation and modification of cards without touching any logic or widgets.

    Clear Hierarchy: Follows the standard UE paradigm: GameMode specifies a HUD Class (BP_HUD), which is responsible for creating the main "Deck" widget (WBP_Deck).

    Widget Factory (WBP_Deck): The WBP_Deck acts as a factory. It reads an array of Data Assets and dynamically spawns the required number of WBP_Card widgets, feeding them the correct data.

    Flexible Layout: Card arrangement is handled by a Wrap Box container, which automatically wraps cards to the next line, ensuring an adaptive layout.

2. The Modular Card Widget (WBP_Card)

    Professional Hierarchy: Utilizes a robust Size Box -> Overlay -> Content structure. This ensures predictable card dimensions and allows for easy layering of content (background, text, icons).

    Dynamic Properties: All key parameters (size, data) are exposed via Expose on Spawn, making the widget highly configurable from the outside.

    Optimized Animations: Smooth hover animations are implemented not via Event Tick, but through a controlled Timer and FInterp To. This provides excellent performance, as updates only occur during the animation itself.

3. Advanced Material System (M_Card_Default)

The core of the visual presentation. The material is fully procedural and multi-layered.

    ID Mask ("Clown Mask"): The entire layout of the card (areas for the frame, title, icon, etc.) is defined by a single color-coded ID Mask texture. This allows for radical design changes by just editing one texture.

    Procedural Mask Generation: Masking out specific ID zones is achieved using the performant Distance -> Step -> OneMinus node combination, which is an industry-standard technique.

    UV Remapping: Implements the math to fit any texture (e.g., an icon) into any rectangular area defined by the ID mask, using the (UV - Start) / Size formula. This allows for non-uniform scaling and positioning of sub-elements within the material itself.

    Procedural Glow (Pseudo-Fresnel): A border glow effect is generated mathematically by analyzing UV coordinates (TexCoord -> Subtract -> Abs -> Max), as the standard Fresnel node is ineffective on flat UI elements.

    Bloom Integration: The glow effect is designed to be "HDR" (color values > 1.0), allowing it to interact with the Post Process Bloom effect for a high-quality emissive look. (Requires enabling the Render Widgets After Post Processing project setting).

4. Refactoring & Reusability (Material Functions)

    Logic Encapsulation: Complex and reusable parts of the material graph (e.g., ID mask generation, UV remapping) are encapsulated into Material Functions (MF_). This results in an exceptionally clean, readable, and easily maintainable main material graph. A key example is the MF_Apply_Texture_By_Mask function, which handles the entire logic of overlaying one texture onto another.

Future Plans & Known Issues

This is an ongoing learning project. Future development plans include:

    Implementing drag-and-drop functionality for cards.

    Adding more procedural material effects, such as a "shake" animation for damage and subtle idle movement.

    Refining animations with Curve assets for perfect easing.

    Bug fixing and further performance optimization.