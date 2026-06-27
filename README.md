# SoloFlow: Smart CRM & Digital Assistant for Solopreneurs 🚀

> **Note:** The original source code for this project is currently unavailable due to hardware migration. This repository serves as an **architectural case study**, documenting the system design, technical challenges solved, and product lifecycle of the application.

## 📱 Project Overview
SoloFlow is a comprehensive digital assistant and CRM tailored for solo entrepreneurs (freelancers, beauty masters, tutors, etc.). It automates routine operations by intercepting client requests across various social networks, managing scheduling, tracking finances, and calculating LTV (Lifetime Value) — allowing professionals to focus on their craft, not administrative tasks.

Built entirely with **Kotlin** and **Jetpack Compose**, the app features a premium dark-mode, glassmorphism-inspired UI and relies heavily on deep Android OS integration for background processing and smart routing.

---

## 🛠 Technology Stack & Architecture
* **Language:** Kotlin
* **UI Framework:** Jetpack Compose (Glassmorphism, Custom Animations)
* **Asynchronous Programming:** Kotlin Coroutines & Flow
* **Architecture Pattern:** MVVM / Clean Architecture concepts
* **Local Storage:** SQLite / Room Database (for CRM, Analytics, and Image URI persistence)
* **Core Android APIs:** `NotificationListenerService`, `AlarmManager`, Implicit/Explicit Intents, Deep Linking.

---

## 🔥 Key Features & Technical Implementation

### 1. Smart Lead Radar (Notification Interception)
The core "killer feature" that acts as a 24/7 background secretary.
* **The Problem:** Freelancers lose leads scattered across Telegram, WhatsApp, Instagram, and local classifieds (Avito).
* **The Solution:** Implemented a custom `NotificationListenerService` that runs persistently in the background.
* **Under the Hood:** 
  * The service filters incoming push notifications, discarding group chats and system noise.
  * Utilizes a keyword-matching algorithm (e.g., "price", "booking", "slots") to identify potential leads.
  * Automatically creates a "New Lead" CRM card, parsing the client's name, message body, and source platform without requiring the user to open the messaging app.

### 2. Seamless Communication & Intent Routing
* **The Feature:** 1-click smart replies using pre-configured templates with dynamic variables (e.g., `{Name}`, `{Time}`).
* **Under the Hood:** 
  * Advanced deep linking and Intent routing (`tg://resolve`, `https://wa.me`). 
  * The app parses contact data and utilizes system Intents to directly open the specific client's chat in third-party closed applications (WhatsApp, Telegram, IG), pre-filling the input field with the generated response.
  * Includes an automated FAQ bot logic for instant replies.

### 3. Intellectual CRM & LTV Tracking
* **The Feature:** Automated client profiling.
* **Under the Hood:** 
  * Relational database design linking clients to appointments, financial records, and before/after portfolios.
  * Safely manages and persists local image URIs using Android's Scoped Storage guidelines.
  * Real-time calculation of Lifetime Value (LTV) to highlight VIP clients.

### 4. Smart Calendar & "Open Slots" Generator
* **The Feature:** Advanced scheduling and automated social media content generation.
* **Under the Hood:**
  * Uses `AlarmManager` for precise, system-level push notifications (24h/1h reminders).
  * An algorithm that subtracts booked appointments from the master schedule to automatically generate formatted "Available Slots" text, ready to be copied or directly shared to Instagram Stories.

### 5. Financial Analytics & Conversion Funnels
* **The Feature:** Dashboard for tracking income, average checks, and lead conversion rates.
* **Under the Hood:** 
  * Aggregation of data using Kotlin Flow to provide reactive UI updates.
  * Traffic source analysis (e.g., comparing the ROI of leads from Telegram vs. VK), visualised through custom Compose charts.

---

## 💎 UI/UX Design: Premium Fintech Aesthetic
* **Jetpack Compose First:** Fully declarative UI.
* **Aesthetic:** Dark Mode default, Glassmorphism (frosted glass effects), deep shadows, and neon gradients (Cyan/Pink).
* **Experience:** Floating cards, fluid transitions, and haptic feedback to mimic the feel of a high-end fintech application.

---

## 📈 Key Takeaways & Engineering Impact
Developing SoloFlow required bypassing standard limitations of background execution in modern Android versions, ensuring battery optimization while maintaining a persistent notification listener, and mastering implicit intent routing across highly sandboxed third-party applications.
