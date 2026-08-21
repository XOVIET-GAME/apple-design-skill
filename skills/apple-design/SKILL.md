---
name: apple-design
description: Complete Apple Human Interface Guidelines (HIG) and Apple Design System standard. Use when designing, building, or auditing UI/UX for iOS, iPadOS, macOS, watchOS, visionOS, or Apple-styled web and mobile applications.
version: 1.1.0
license: MIT
author: apple-design-skill
tags:
  - design-system
  - apple
  - hig
  - swiftui
  - ios
  - macos
  - visionos
  - web-design
  - ui-ux
  - audit
---

# Apple Design System & Human Interface Guidelines (HIG)

This skill equips AI coding agents with the exact principles, visual specifications, component architectures, typography metrics, color tokens, motion curves, and automated compliance auditing defined by **Apple's Human Interface Guidelines (HIG)** across iOS, iPadOS, macOS, watchOS, visionOS, and modern Apple-grade Web UI.

---

## 🎯 Operational Modes

### Mode 1 — Design & Build from Scratch
When tasked with creating new screens, apps, or web interfaces in Apple style:
1. Choose the platform-native navigation paradigm (e.g. Bottom Tab Bar for iOS, Sidebar for macOS/iPad, Ornaments for visionOS).
2. Establish the 8pt spatial grid and continuous squircle curvature (`G2 continuity`).
3. Apply the SF Pro / New York typography scale with optical tracking rules.
4. Implement semantic Dynamic Colors (Light & OLED Dark mode) and Liquid Frosted Glass materials.
5. Apply Apple spring physics (`cubic-bezier(0.25, 1, 0.5, 1)`) and tactile active feedback (`scale(0.97)`).

### Mode 2 — Apple HIG Compliance Audit & Scoring
When reviewing an existing codebase, mockup, or component:
1. Run the audit tool `node skills/apple-design/scripts/audit-apple-design.mjs` to perform automated static scanning with a **0–100 Scoring Rubric**.
2. Perform exact mathematical WCAG contrast checks and 44×44pt touch-target validations.
3. Fill out the **[Apple HIG Audit Scorecard](templates/apple-hig-audit-scorecard.md)** across the 5 core pillars.
4. Deliver prioritized findings with **Confidence Tagging**:
   - 🟢 **Tool-verified**: Statistically measured via CLI tool (e.g., contrast ratio, button dimension, static CSS rules).
   - 🟡 **Needs device test**: Requires hardware interaction (e.g., Dynamic Type at 300%, Reduce Transparency toggle, VoiceOver speech hierarchy).
   - 🔴 **Assumed**: Contextual design trade-off or subjective aesthetic evaluation.

---

## 🛠️ The Apple HIG Compliance CLI Engine

The built-in audit engine (`skills/apple-design/scripts/audit-apple-design.mjs`) provides four subcommands:

```bash
# 1. Full Codebase Static Scan with 0-100 Scorecard (Default)
npm run audit
# or: node skills/apple-design/scripts/audit-apple-design.mjs [path]

# 2. WCAG Relative Luminance Contrast Ratio Check
node skills/apple-design/scripts/audit-apple-design.mjs contrast "#8E8E93" "#FFFFFF"
# -> Contrast Ratio: 3.26:1 [🔴 FAILED - Needs >= 4.5:1]

# 3. Tap Target Sizing Validation (44x44 pt minimum)
node skills/apple-design/scripts/audit-apple-design.mjs target 32 32
# -> Tap Target: 32x32 pt [🔴 FAILED - Minimum 44x44 pt]

# 4. Batch JSON Automated Verification
node skills/apple-design/scripts/audit-apple-design.mjs batch audit.json
```

### Audit Scoring Rubric:
- Base score: **100 points**.
- Point deduction: **-10 points per violation**.
- Scorecard Classification:
  - 🟢 **90 – 100 pts**: **Ship (Sẵn sàng phát hành)** — Đạt chuẩn xuất sắc.
  - 🟡 **70 – 89 pts**: **Cần sửa trước khi release (Fix before release)** — Cần khắc phục trước khi đưa lên App Store / production.
  - 🔴 **< 70 pts**: **Cần thiết kế lại (Systematic redesign required)** — Vi phạm nghiêm trọng kiến trúc hoặc khả năng tiếp cận.

---

## 1. Core Design Philosophy

Apple interfaces are built upon three primary pillars:

1. **Clarity**:
   - Text is legible at every size; icons are precise, distinct, and universally understood.
   - Adornments are subtle and purposeful. Content always takes visual priority over decorative Chrome.
   - Negative space (whitespace) provides breathing room and clarifies visual hierarchy.

2. **Deference**:
   - Fluid motion, translucent materials, and crisp typography elevate content without competing with it.
   - Backgrounds defer to content; chrome recedes when the user is engaged in primary tasks.

3. **Depth**:
   - Distinct visual layers, realistic lighting, specular highlights, and physical spring physics convey spatial hierarchy and tactile realism.
   - Elevations and materials communicate interactive affordances without harsh dropped shadows or abrasive outlines.

---

## 2. Universal Apple Design Tenets & Critical Rules

### 🚫 Forbidden Anti-Patterns (Never Do These)
- **NO Purple/Violet On Dark Themes**: Never use purple fonts or violet accent buttons on dark backgrounds. Use Apple System Blue (`#0A84FF`) or semantic system tints.
- **NO Harsh Drop Shadows**: Never use dense black un-diffused box shadows (`box-shadow: 0 4px 10px rgba(0,0,0,0.5)`). Use multi-layered ambient diffusion (`box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08), 0 1px 2px rgba(0, 0, 0, 0.04)`).
- **NO Sharp / Geometric Corners**: Never leave interactive controls, cards, or inputs with 0px radius or arbitrary non-continuous corners.
- **NO Untracked Large Typography**: Never render large headings (>24px) without tight letter-spacing (-0.02em to -0.03em / -0.5px to -1.2px).
- **NO Non-Standard Touch Targets**: Never create clickable elements smaller than 44×44 pt (iOS standard) or 28×28 pt (macOS compact pointer).
- **NO Plain Static CSS Transitions**: Never use `ease-in-out` for physical UI interactions; always use fluid spring physics or Apple easing curves.

---

## 3. Visual Foundations

### A. Typography System (San Francisco & New York)
- **Primary Interface Font**: SF Pro (`-apple-system, BlinkMacSystemFont, "SF Pro Display", "SF Pro Text", "Helvetica Neue", sans-serif`)
- **Monospace Font**: SF Mono (`ui-monospace, "SF Mono", Menlo, Monaco, Consolas, monospace`)
- **Serif Font**: New York (`"New York", ui-serif, Georgia, Cambria, serif`)

#### Typographic Scale & Optical Sizing Rules:
| Style | Size (pt/px) | Weight | Line Height | Tracking / Letter Spacing |
| :--- | :--- | :--- | :--- | :--- |
| **Large Title** | 34px | Bold (700) | 41px | `-0.022em (-0.75px)` |
| **Title 1** | 28px | Bold / SemiBold | 34px | `-0.020em (-0.56px)` |
| **Title 2** | 22px | Bold / SemiBold | 28px | `-0.018em (-0.40px)` |
| **Title 3** | 20px | SemiBold (600) | 25px | `-0.015em (-0.30px)` |
| **Headline** | 17px | SemiBold (600) | 22px | `-0.012em (-0.20px)` |
| **Body** | 17px | Regular (400) | 22px | `-0.010em (-0.17px)` |
| **Callout** | 16px | Regular (400) | 21px | `-0.008em (-0.13px)` |
| **Subheadline** | 15px | Regular (400) | 20px | `-0.005em (-0.08px)` |
| **Footnote** | 13px | Regular (400) | 18px | `0.000em (0.00px)` |
| **Caption 1** | 12px | Regular (400) | 16px | `0.005em (+0.06px)` |
| **Caption 2** | 11px | Regular / Medium | 13px | `0.010em (+0.11px)` |

---

## 4. Materials, Translucency & Specular Glass

Apple materials blur underlying content to create visual grounding while maintaining vibrancy:

```css
/* Authentic Apple Ultra-Thin Frosted Glass Material */
.apple-material-ultrathin {
  background: rgba(255, 255, 255, 0.72);
  backdrop-filter: blur(20px) saturate(190%);
  -webkit-backdrop-filter: blur(20px) saturate(190%);
  border: 1px solid rgba(255, 255, 255, 0.45);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.04), 0 1px 2px rgba(0, 0, 0, 0.02);
}

@media (prefers-color-scheme: dark), [data-theme="dark"] {
  .apple-material-ultrathin {
    background: rgba(28, 28, 30, 0.75);
    backdrop-filter: blur(25px) saturate(190%);
    -webkit-backdrop-filter: blur(25px) saturate(190%);
    border: 1px solid rgba(255, 255, 255, 0.12);
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.35), 0 1px 3px rgba(255, 255, 255, 0.05) inset;
  }
}
```

---

## 5. Animation Physics (Apple Spring Curves)

Never use linear or standard ease curves for interactive UI. Use authentic Apple spring physics:

### Spring Parameters Reference:
- **Interactive / Tap feedback**: `mass: 1, stiffness: 350, damping: 35` (CSS approx: `cubic-bezier(0.25, 1, 0.5, 1)`)
- **Sheet Presentation / Modal Slide**: `mass: 1.2, stiffness: 280, damping: 28` (CSS approx: `cubic-bezier(0.32, 0.72, 0, 1)`)
- **Snappy Switch / Toggle**: `mass: 0.8, stiffness: 450, damping: 30`

```css
/* Apple Native Motion Classes */
.apple-spring-interactive {
  transition: transform 0.35s cubic-bezier(0.25, 1, 0.5, 1),
              opacity 0.25s ease;
}

.apple-spring-interactive:active {
  transform: scale(0.965);
}
```

---

## 6. Bundled Resources & Full Apple HIG Library

- **[Apple HIG Audit Scorecard Template](templates/apple-hig-audit-scorecard.md)**: Standard 5-pillar evaluation scorecard.
- **Assets & Presets**:
  - `assets/apple-tokens.css`: Complete CSS variable design token stylesheet.
  - `assets/apple-components.css`: Ready-to-use CSS components (Buttons, Glass cards, Segmented, Sheets).
  - `assets/tailwind.preset.apple.js`: Tailwind configuration preset.
  - `assets/swiftui-cheat-sheet.md`: Idiomatic SwiftUI patterns.
- **CLI Automation Tools**:
  - `npm run audit`: Scans codebases for Apple HIG violations and generates a 0–100 score.
  - `npm run fetch-hig`: Fetches/updates the entire Apple HIG documentation and illustrations from Apple CDN.

---

## 7. Apple Human Interface Guidelines (HIG) Index

Complete collection of **179** official Apple Human Interface Guidelines documentation pages with downloaded local illustrations.

| Guideline Topic | Markdown File | Overview |
| :--- | :--- | :--- |
| **Accessibility** | [accessibility.md](./references/accessibility.md) | Accessible user interfaces empower everyone to have a great experience with your app or game. |
| **Action button** | [action-button.md](./references/action-button.md) | The Action button gives people quick access to their favorite features on supported iPhone and Apple... |
| **Action sheets** | [action-sheets.md](./references/action-sheets.md) | An action sheet is a modal view that presents choices related to an action people initiate. |
| **Activity rings** | [activity-rings.md](./references/activity-rings.md) | Activity rings show an individual's daily progress toward Move, Exercise, and Stand goals. |
| **Activity views** | [activity-views.md](./references/activity-views.md) | An activity view — often called a *share sheet* — presents a range of tasks that people can perform ... |
| **AirPlay** | [airplay.md](./references/airplay.md) | AirPlay lets people stream media content wirelessly from iOS, iPadOS, macOS, and tvOS devices to App... |
| **Alerts** | [alerts.md](./references/alerts.md) | An alert gives people critical information they need right away. |
| **Always On** | [always-on.md](./references/always-on.md) | On devices that include the Always On display, the system can continue to display an app's interface... |
| **App Clips** | [app-clips.md](./references/app-clips.md) | An App Clip is a lightweight version of your app or game that provides an on-the-go or demo experien... |
| **App icons** | [app-icons.md](./references/app-icons.md) | A unique, memorable icon expresses your app's or game's purpose and personality and helps people rec... |
| **App Shortcuts** | [app-shortcuts.md](./references/app-shortcuts.md) | An App Shortcut gives people access to your app's key functions or content throughout the system. |
| **Apple Accessibility (a11y) & Haptics Guidelines** | [accessibility-and-haptics.md](./references/accessibility-and-haptics.md) |  |
| **Apple Color Palette & Translucent Materials** | [color-palette-materials.md](./references/color-palette-materials.md) |  |
| **Apple Components & Layout Architecture** | [components-and-layouts.md](./references/components-and-layouts.md) |  |
| **Apple Human Interface Guidelines (HIG) Principles** | [hig-principles.md](./references/hig-principles.md) |  |
| **Apple Motion & Spring Physics Guide** | [animations-and-springs.md](./references/animations-and-springs.md) |  |
| **Apple Pay** | [apple-pay.md](./references/apple-pay.md) | Apple Pay is a secure, easy way to make payments for physical goods and services, donations, and sub... |
| **Apple Pencil and Scribble** | [apple-pencil-and-scribble.md](./references/apple-pencil-and-scribble.md) | Apple Pencil helps make drawing, handwriting, and marking effortless and natural, in addition to per... |
| **Apple Spatial Computing & visionOS Design Guidelines** | [spatial-visionos.md](./references/spatial-visionos.md) |  |
| **Apple Typography System (San Francisco & New York)** | [typography-system.md](./references/typography-system.md) |  |
| **Augmented reality** | [augmented-reality.md](./references/augmented-reality.md) | Augmented reality (or AR) lets you deliver immersive, engaging experiences that seamlessly blend vir... |
| **Boxes** | [boxes.md](./references/boxes.md) | A box creates a visually distinct group of logically related information and components. |
| **Branding** | [branding.md](./references/branding.md) | Apps and games express their unique brand identity in ways that make them instantly recognizable whi... |
| **Buttons** | [buttons.md](./references/buttons.md) | A button initiates an instantaneous action. |
| **Camera Control** | [camera-control.md](./references/camera-control.md) | The Camera Control provides direct access to your app's camera experience. |
| **CareKit** | [carekit.md](./references/carekit.md) | People can use CareKit apps to manage care plans related to a chronic illness like diabetes, recover... |
| **CarPlay** | [carplay.md](./references/carplay.md) | CarPlay lets people get directions, make calls, send and receive messages, listen to music, and more... |
| **Charting data** | [charting-data.md](./references/charting-data.md) | Presenting data in a chart can help you communicate information with clarity and appeal. |
| **Charts** | [charts.md](./references/charts.md) | Organize data in a chart to communicate information with clarity and visual appeal. |
| **Collaboration and sharing** | [collaboration-and-sharing.md](./references/collaboration-and-sharing.md) | Great collaboration and sharing experiences are simple and responsive, letting people engage with th... |
| **Collections** | [collections.md](./references/collections.md) | A collection manages an ordered set of content and presents it in a customizable and highly visual l... |
| **Color** | [color.md](./references/color.md) | Judicious use of color can enhance communication, evoke your brand, provide visual continuity, commu... |
| **Color wells** | [color-wells.md](./references/color-wells.md) | A color well lets people adjust the color of text, shapes, guides, and other onscreen elements. |
| **Column views** | [column-views.md](./references/column-views.md) | A column view — also called a *browser* — lets people view and navigate a data hierarchy using a ser... |
| **Combo boxes** | [combo-boxes.md](./references/combo-boxes.md) | A combo box combines a text field with a pull-down button in a single control. |
| **Complications** | [complications.md](./references/complications.md) | A complication displays timely, relevant information on the watch face, where people can view it eac... |
| **Components** | [components.md](./references/components.md) | Learn how to use and customize system-defined components to give people a familiar and consistent ex... |
| **Content** | [content.md](./references/content.md) |  |
| **Context menus** | [context-menus.md](./references/context-menus.md) | A context menu provides access to functionality that's directly related to an item, without clutteri... |
| **Controls** | [controls.md](./references/controls.md) | A control provides quick access to a feature of your app from Control Center, the Lock Screen, or th... |
| **Dark Mode** | [dark-mode.md](./references/dark-mode.md) | Dark Mode is a systemwide appearance setting that uses a dark color palette to provide a comfortable... |
| **Design principles** | [design-principles.md](./references/design-principles.md) | Explore fundamental principles that guide design across Apple platforms. |
| **Designing for games** | [designing-for-games.md](./references/designing-for-games.md) | When people play your game on an Apple device, they dive into the world you designed while relying o... |
| **Designing for iOS** | [designing-for-ios.md](./references/designing-for-ios.md) | People depend on their iPhone to help them stay connected, play games, view media, accomplish tasks,... |
| **Designing for iPadOS** | [designing-for-ipados.md](./references/designing-for-ipados.md) | People value the power, mobility, and flexibility of iPad as they enjoy media, play games, perform d... |
| **Designing for macOS** | [designing-for-macos.md](./references/designing-for-macos.md) | People rely on the power, spaciousness, and flexibility of a Mac as they perform in-depth productivi... |
| **Designing for tvOS** | [designing-for-tvos.md](./references/designing-for-tvos.md) | People enjoy the vibrant content, immersive experiences, and streamlined interactions that tvOS deli... |
| **Designing for visionOS** | [designing-for-visionos.md](./references/designing-for-visionos.md) | When people wear Apple Vision Pro, they enter an infinite 3D space where they can engage with your a... |
| **Designing for watchOS** | [designing-for-watchos.md](./references/designing-for-watchos.md) | When people glance at their Apple Watch, they know they can access essential information and perform... |
| **Digit entry views** | [digit-entry-views.md](./references/digit-entry-views.md) | A digit entry view fills the entire screen and prompts people to enter a series of digits, like a PI... |
| **Digital Crown** | [digital-crown.md](./references/digital-crown.md) | The Digital Crown is an important hardware input for Apple Vision Pro and Apple Watch. |
| **Disclosure controls** | [disclosure-controls.md](./references/disclosure-controls.md) | Disclosure controls reveal and hide information and functionality related to specific controls or vi... |
| **Dock menus** | [dock-menus.md](./references/dock-menus.md) | On a Mac, people can secondary click an app's or game's icon in the Dock to reveal a Dock menu, whic... |
| **Drag and drop** | [drag-and-drop.md](./references/drag-and-drop.md) | Using drag and drop, people can move or duplicate selected photos, text, and other content by draggi... |
| **Edit menus** | [edit-menus.md](./references/edit-menus.md) | An edit menu lets people make changes to selected content in the current view, in addition to offeri... |
| **Entering data** | [entering-data.md](./references/entering-data.md) | When you need information from people, design ways that make it easy for them to provide it without ... |
| **Eyes** | [eyes.md](./references/eyes.md) | In visionOS, people look at a virtual object to identify it as a target they can interact with. |
| **Feedback** | [feedback.md](./references/feedback.md) | Feedback helps people know what's happening, discover what they can do next, understand the results ... |
| **File management** | [file-management.md](./references/file-management.md) | Some apps can support documents and files that people expect to manage throughout the system. |
| **Focus and selection** | [focus-and-selection.md](./references/focus-and-selection.md) | Focus helps people visually confirm the object that their interaction targets. |
| **Foundations** | [foundations.md](./references/foundations.md) | Understand how fundamental design elements help you create rich experiences. |
| **Game Center** | [game-center.md](./references/game-center.md) | Game Center is Apple's social gaming network, which lets players track their progress and connect wi... |
| **Game controls** | [game-controls.md](./references/game-controls.md) | Precise, intuitive game controls enhance gameplay and can increase a player's immersion in the game. |
| **Gauges** | [gauges.md](./references/gauges.md) | A gauge displays a specific numerical value within a range of values. |
| **Generative AI** | [generative-ai.md](./references/generative-ai.md) | Generative AI empowers you to enhance your app or game with dynamic content and offer intelligent fe... |
| **Gestures** | [gestures.md](./references/gestures.md) | A gesture is a physical motion that a person uses to directly affect an object in an app or game on ... |
| **Getting started** | [getting-started.md](./references/getting-started.md) | Create an app or game that feels at home on every platform you support. |
| **Going full screen** | [going-full-screen.md](./references/going-full-screen.md) | iPhone, iPad, and Mac offer full-screen modes that let people expand a window to fill the screen, hi... |
| **Gyroscope and accelerometer** | [gyro-and-accelerometer.md](./references/gyro-and-accelerometer.md) | On-device gyroscopes and accelerometers can supply data about a device's movement in the physical wo... |
| **HealthKit** | [healthkit.md](./references/healthkit.md) | HealthKit is the central repository for health and fitness data in iOS, iPadOS, and watchOS. |
| **Home Screen quick actions** | [home-screen-quick-actions.md](./references/home-screen-quick-actions.md) | Home Screen quick actions give people a way to perform app-specific actions from the Home Screen. |
| **HomeKit** | [homekit.md](./references/homekit.md) | HomeKit lets people securely control connected accessories in their homes using Siri or the Home app... |
| **Human Interface Guidelines** | [human-interface-guidelines.md](./references/human-interface-guidelines.md) | The HIG contains guidance and best practices that can help you design a great experience for any App... |
| **iCloud** | [icloud.md](./references/icloud.md) | iCloud is a service that lets people seamlessly access the content they care about — photos, videos,... |
| **Icons** | [icons.md](./references/icons.md) | An effective icon is a graphic asset that expresses a single concept in ways people instantly unders... |
| **ID Verifier** | [id-verifier.md](./references/id-verifier.md) | ID Verifier lets your iPhone app read mobile IDs in person without requiring external hardware. |
| **Image views** | [image-views.md](./references/image-views.md) | An image view displays a single image — or in some cases, an animated sequence of images — on a tran... |
| **Image wells** | [image-wells.md](./references/image-wells.md) | An image well is an editable version of an image view. |
| **Images** | [images.md](./references/images.md) | To make sure your artwork looks great on all devices you support, learn how the system displays cont... |
| **iMessage apps and stickers** | [imessage-apps-and-stickers.md](./references/imessage-apps-and-stickers.md) | An iMessage app can help people share content, collaborate, and even play games with others in a con... |
| **Immersive experiences** | [immersive-experiences.md](./references/immersive-experiences.md) | In visionOS, you can design apps and games that extend beyond windows and volumes, immersing people ... |
| **In-app purchase** | [in-app-purchase.md](./references/in-app-purchase.md) | People can use in-app purchase to pay for virtual goods — like premium content, digital goods, and s... |
| **Inclusion** | [inclusion.md](./references/inclusion.md) | Inclusive apps and games put people first by prioritizing respectful communication and presenting co... |
| **Inputs** | [inputs.md](./references/inputs.md) | Learn about the various methods people use to control your app or game and enter data. |
| **Keyboards** | [keyboards.md](./references/keyboards.md) | A physical keyboard can be an essential input device for entering text, playing games, controlling a... |
| **Labels** | [labels.md](./references/labels.md) | A label is a static piece of text that people can read and often copy, but not edit. |
| **Launching** | [launching.md](./references/launching.md) | A streamlined launch experience helps people start using your app or game immediately. |
| **Layout** | [layout.md](./references/layout.md) | A consistent layout that adapts to various contexts makes your experience more approachable and help... |
| **Layout and organization** | [layout-and-organization.md](./references/layout-and-organization.md) |  |
| **Lists and tables** | [lists-and-tables.md](./references/lists-and-tables.md) | Lists and tables present data in one or more columns of rows. |
| **Live Activities** | [live-activities.md](./references/live-activities.md) | A Live Activity lets people track the progress of an activity, event, or task at a glance. |
| **Live Photos** | [live-photos.md](./references/live-photos.md) | Live Photos lets people capture favorite memories in a sound- and motion-rich interactive experience... |
| **Live-viewing apps** | [live-viewing-apps.md](./references/live-viewing-apps.md) | As you design a live-viewing app, prioritize the content and create fun, fluid interactions that enc... |
| **Loading** | [loading.md](./references/loading.md) | The best content-loading experience finishes before people become aware of it. |
| **Lockups** | [lockups.md](./references/lockups.md) | Lockups combine multiple separate views into a single, interactive unit. |
| **Mac Catalyst** | [mac-catalyst.md](./references/mac-catalyst.md) | When you use Mac Catalyst to create a Mac version of your iPad app, you give people the opportunity ... |
| **Machine learning** | [machine-learning.md](./references/machine-learning.md) | Machine learning enables apps and games to learn from data and usage patterns, letting you improve e... |
| **Managing accounts** | [managing-accounts.md](./references/managing-accounts.md) | When it doesn't create an unnecessary barrier to your experience, an account can be a convenient way... |
| **Managing notifications** | [managing-notifications.md](./references/managing-notifications.md) | Notifications can give people timely and important information, whether the device is locked or in u... |
| **Maps** | [maps.md](./references/maps.md) | A map displays outdoor or indoor geographical data in your app or on your website. |
| **Materials** | [materials.md](./references/materials.md) | A material is a visual effect that creates a sense of depth, layering, and hierarchy between foregro... |
| **Menus** | [menus.md](./references/menus.md) | A menu reveals its options when people interact with it, making it a space-efficient way to present ... |
| **Menus and actions** | [menus-and-actions.md](./references/menus-and-actions.md) |  |
| **Modality** | [modality.md](./references/modality.md) | Modality is a design technique that presents content in a separate, dedicated mode that prevents int... |
| **Motion** | [motion.md](./references/motion.md) | Beautiful, fluid motions bring the interface to life, conveying status, providing feedback and instr... |
| **Multitasking** | [multitasking.md](./references/multitasking.md) | Multitasking lets people switch quickly from one app to another, performing tasks in each. |
| **Navigation and search** | [navigation-and-search.md](./references/navigation-and-search.md) |  |
| **Nearby interactions** | [nearby-interactions.md](./references/nearby-interactions.md) | Nearby interactions support on-device experiences that integrate the presence of people and objects ... |
| **NFC** | [nfc.md](./references/nfc.md) | Near-field communication (NFC) allows devices within a few centimeters of each other to exchange inf... |
| **Notifications** | [notifications.md](./references/notifications.md) | A notification gives people timely, high-value information they can understand at a glance. |
| **Offering help** | [offering-help.md](./references/offering-help.md) | Although the most effective experiences are approachable and intuitive, you can provide contextual h... |
| **Onboarding** | [onboarding.md](./references/onboarding.md) | Onboarding can help people get a quick start using your app or game. |
| **Ornaments** | [ornaments.md](./references/ornaments.md) | In visionOS, an ornament presents controls and information related to a window, without crowding or ... |
| **Outline views** | [outline-views.md](./references/outline-views.md) | An outline view presents hierarchical data in a scrolling list of cells that are organized into colu... |
| **Page controls** | [page-controls.md](./references/page-controls.md) | A page control displays a row of indicator images, each of which represents a page in a flat list. |
| **Panels** | [panels.md](./references/panels.md) | In a macOS app, a panel typically floats above other open windows providing supplementary controls, ... |
| **Path controls** | [path-controls.md](./references/path-controls.md) | A path control shows the file system path of a selected file or folder. |
| **Patterns** | [patterns.md](./references/patterns.md) | Get design guidance for supporting common user actions, tasks, and experiences. |
| **Photo editing** | [photo-editing.md](./references/photo-editing.md) | Photo-editing extensions let people modify photos and videos within the Photos app by applying filte... |
| **Pickers** | [pickers.md](./references/pickers.md) | A picker displays one or more scrollable lists of distinct values that people can choose from. |
| **Playing audio** | [playing-audio.md](./references/playing-audio.md) | People expect rich audio experiences that automatically adjust when the context changes on the devic... |
| **Playing haptics** | [playing-haptics.md](./references/playing-haptics.md) | Playing haptics can engage people's sense of touch and bring their familiarity with the physical wor... |
| **Playing video** | [playing-video.md](./references/playing-video.md) | People expect to enjoy rich video experiences on their devices, regardless of the app or game they'r... |
| **Pointing devices** | [pointing-devices.md](./references/pointing-devices.md) | People can use a pointing device like a trackpad or mouse to navigate the interface and initiate act... |
| **Pop-up buttons** | [pop-up-buttons.md](./references/pop-up-buttons.md) | A pop-up button displays a menu of mutually exclusive options. |
| **Popovers** | [popovers.md](./references/popovers.md) | A popover is a transient view that appears above other content when people click or tap a control or... |
| **Presentation** | [presentation.md](./references/presentation.md) |  |
| **Printing** | [printing.md](./references/printing.md) | An iOS, iPadOS, macOS, or visionOS app can integrate system-provided print functionality when it mak... |
| **Privacy** | [privacy.md](./references/privacy.md) | Privacy is paramount: it's critical to be transparent about the privacy-related data and resources y... |
| **Progress indicators** | [progress-indicators.md](./references/progress-indicators.md) | Progress indicators let people know that your app isn't stalled while it loads content or performs l... |
| **Pull-down buttons** | [pull-down-buttons.md](./references/pull-down-buttons.md) | A pull-down button displays a menu of items or actions that directly relate to the button's purpose. |
| **Rating indicators** | [rating-indicators.md](./references/rating-indicators.md) | A rating indicator uses a series of horizontally arranged graphical symbols — by default, stars — to... |
| **Ratings and reviews** | [ratings-and-reviews.md](./references/ratings-and-reviews.md) | People often view the ratings and reviews for an app or game before they download it. |
| **Remotes** | [remotes.md](./references/remotes.md) | The Siri Remote is the primary input method for Apple TV, helping people feel connected to onscreen ... |
| **ResearchKit** | [researchkit.md](./references/researchkit.md) | A research app lets people everywhere participate in important medical research studies. |
| **Right to left** | [right-to-left.md](./references/right-to-left.md) | Support right-to-left languages like Arabic and Hebrew by reversing your interface as needed to matc... |
| **Scroll views** | [scroll-views.md](./references/scroll-views.md) | A scroll view lets people view content that's larger than the view's boundaries by moving the conten... |
| **Search fields** | [search-fields.md](./references/search-fields.md) | A search field lets people search a collection of content for specific terms they enter. |
| **Searching** | [searching.md](./references/searching.md) | People use various search techniques to find content on their device, within an app, and within a do... |
| **Segmented controls** | [segmented-controls.md](./references/segmented-controls.md) | A segmented control is a linear set of two or more segments, each of which functions as a button. |
| **Selection and input** | [selection-and-input.md](./references/selection-and-input.md) |  |
| **Settings** | [settings.md](./references/settings.md) | People expect apps and games to just work, but they also appreciate having ways to customize the exp... |
| **SF Symbols** | [sf-symbols.md](./references/sf-symbols.md) | SF Symbols provides thousands of consistent, highly configurable symbols that integrate seamlessly w... |
| **SharePlay** | [shareplay.md](./references/shareplay.md) | SharePlay helps multiple people share activities — like viewing a movie, listening to music, playing... |
| **ShazamKit** | [shazamkit.md](./references/shazamkit.md) | ShazamKit supports audio recognition by matching an audio sample against the ShazamKit catalog or a ... |
| **Sheets** | [sheets.md](./references/sheets.md) | A sheet helps people perform a scoped task that's closely related to their current context. |
| **Sidebars** | [sidebars.md](./references/sidebars.md) | A sidebar appears on the leading side of a view and lets people navigate between areas of your app o... |
| **Sign in with Apple** | [sign-in-with-apple.md](./references/sign-in-with-apple.md) | Sign in with Apple provides a fast, private way to sign into apps and websites, giving people a cons... |
| **Siri** | [siri.md](./references/siri.md) | People use Siri to help them with the things they need to find, know, or do every day. |
| **Sliders** | [sliders.md](./references/sliders.md) | A slider is a horizontal track with a control, called a thumb, that people can adjust between a mini... |
| **Snippets** | [snippets.md](./references/snippets.md) | When someone performs a task with Siri or an App Shortcut, a snippet shows the result or asks for co... |
| **Spatial layout** | [spatial-layout.md](./references/spatial-layout.md) | Spatial layout techniques help you take advantage of the infinite canvas of Apple Vision Pro and pre... |
| **Split views** | [split-views.md](./references/split-views.md) | A split view manages the presentation of multiple adjacent panes of content, each of which can conta... |
| **Status** | [status.md](./references/status.md) |  |
| **Status bars** | [status-bars.md](./references/status-bars.md) | A status bar appears along the upper edge of the screen and displays information about the device's ... |
| **Steppers** | [steppers.md](./references/steppers.md) | A stepper is a two-segment control that people use to increase or decrease an incremental value. |
| **System experiences** | [system-experiences.md](./references/system-experiences.md) |  |
| **Tab bars** | [tab-bars.md](./references/tab-bars.md) | A tab bar lets people navigate between top-level sections of your app. |
| **Tab views** | [tab-views.md](./references/tab-views.md) | A tab view presents multiple mutually exclusive panes of content in the same area, which people can ... |
| **Tap to Pay on iPhone** | [tap-to-pay-on-iphone.md](./references/tap-to-pay-on-iphone.md) | Tap to Pay on iPhone lets merchants accept contactless payments using an app on their iPhone, withou... |
| **Technologies** | [technologies.md](./references/technologies.md) | Discover the Apple technologies, features, and services you can integrate into your app or game. |
| **Text fields** | [text-fields.md](./references/text-fields.md) | A text field is a rectangular area in which people enter or edit small, specific pieces of text. |
| **Text views** | [text-views.md](./references/text-views.md) | A text view displays multiline, styled text content, which can optionally be editable. |
| **The menu bar** | [the-menu-bar.md](./references/the-menu-bar.md) | On a Mac or an iPad, the menu bar at the top of the screen displays the top-level menus in your app ... |
| **Toggles** | [toggles.md](./references/toggles.md) | A toggle lets people choose between a pair of opposing states, like on and off, using a different ap... |
| **Token fields** | [token-fields.md](./references/token-fields.md) | A token field is a type of text field that can convert text into *tokens* that are easy to select an... |
| **Toolbars** | [toolbars.md](./references/toolbars.md) | A toolbar provides convenient access to frequently used commands, controls, navigation, and search. |
| **Top Shelf** | [top-shelf.md](./references/top-shelf.md) | The Apple TV Home Screen provides an area called Top Shelf, which showcases your content in a rich, ... |
| **Typography** | [typography.md](./references/typography.md) | Your typographic choices can help you display legible text, convey an information hierarchy, communi... |
| **Undo and redo** | [undo-and-redo.md](./references/undo-and-redo.md) | Undo and redo gives people easy ways to reverse many types of actions, which can also help people ex... |
| **Virtual keyboards** | [virtual-keyboards.md](./references/virtual-keyboards.md) | On devices without physical keyboards, the system offers various types of virtual keyboards people c... |
| **VoiceOver** | [voiceover.md](./references/voiceover.md) | VoiceOver is a screen reader that lets people experience your app's interface without needing to see... |
| **Wallet** | [wallet.md](./references/wallet.md) | Wallet helps people securely store their credit and debit cards, driver's license or state ID, trans... |
| **Watch faces** | [watch-faces.md](./references/watch-faces.md) | A watch face is a view that people choose as their primary view in watchOS. |
| **Web views** | [web-views.md](./references/web-views.md) | A web view loads and displays rich web content, such as embedded HTML and websites, directly within ... |
| **Widgets** | [widgets.md](./references/widgets.md) | A widget provides quick access to essential information and focused interactions from your app or ga... |
| **Windows** | [windows.md](./references/windows.md) | A window presents UI views and components in your app or game. |
| **Workouts** | [workouts.md](./references/workouts.md) | A great workout or fitness experience encourages people to engage with their current activity and he... |
| **Writing** | [writing.md](./references/writing.md) | The words you choose within your app are an essential part of its user experience. |
