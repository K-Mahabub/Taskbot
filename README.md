# Taskbot
<img width="652" height="366" alt="Screenshot from 2025-12-31 23-26-45" src="https://github.com/user-attachments/assets/f110efb6-f2c3-4d01-973d-d345fb2f6577" />

## 1. Project Overview

**Taskbot** is a cross-platform, always-running personal assistant and task management system designed as a **desktop-first productivity tool** with deep system integration. The project combines **C (GTK)** for a lightweight native Linux GUI, **system-level automation**, **keyboard shortcuts**, **background services**, and **API-driven configuration**, with optional **IoT / ESP32 integration** for hardware interaction.

The core idea is simple but powerful: **Taskbot runs continuously in the background, listens for user actions (keyboard shortcuts, reminders, API updates), and responds instantly with useful tools**—calendar access, reminders, notes, system controls, messaging, and future AI responses.

---

## 2. Core Goals

* Create a **lightweight native desktop assistant** (not Electron-based)
* Ensure **non-blocking, always-running background execution**
* Provide **instant access via global keyboard shortcuts**
* Integrate **task management, reminders, calendar, notes, and messaging**
* Allow **remote control & configuration via REST API**

---

## 3. Technology Stack

### Desktop Application

* **Language:** C
* **GUI Toolkit:** GTK+ 3
* **Threading:** POSIX threads (pthreads)
* **Event Handling:** GTK main loop + background worker threads
* **OS Target:** Linux (X11)

### Backend / API

* **REST API** (remote settings & control)
* **JSON-based configuration**
* Used to dynamically control UI elements and bot behavior

---

## 4. Application Architecture

### 4.1 Always-Running Core

Taskbot starts once and **never blocks the main GTK loop**.

* Background threads handle:

  * Reminder checking
  * API polling
  * Keyboard shortcut listeners
* Main thread handles:

  * UI rendering
  * User interaction

This design ensures:

* No UI freezing
* Instant responsiveness
* Safe concurrent execution

---

### 4.2 Non-Blocking Reminder System

* `check_reminder()` runs in a **separate thread**
* Continuously checks scheduled reminders
* Triggers notifications or UI actions
* Starts automatically from `main()` without waiting for return

This allows Taskbot to act like a **daemon-style assistant**.

---

### 4.3 Global Keyboard Shortcuts

Taskbot listens for **system-wide keyboard shortcuts**, such as:

* **Ctrl + Shift + C** → Open Calendar
* Additional shortcuts for:

  * Notes
  * Messages
  * Settings
  * Quick actions

Key features:

* Works even when Taskbot window is hidden
* Uses low-level key event detection
* Extensible shortcut mapping

---

## 5. User Interface (GTK)

### 5.1 Main Window

* Chat-style interaction panel
* Input box for commands
* Output area for responses

### 5.2 Calendar Window
* Opens instantly via shortcut
* Used for:

  * Viewing dates
  * Managing reminders
  * Planning tasks

### 5.3 Settings Window
* Toggle-based controls
* Button visibility controlled by API
* Live UI updates based on backend data

# Taskbot – Button Descriptions & Use Cases

## 1. Overview

This document describes **all buttons visible in the Taskbot user interface** and explains their **purpose and real-world use cases**. Taskbot is a **desktop-only productivity and system assistant** designed to run continuously in the background and provide instant access to commonly used tools.

There is **no embedded system or hardware integration** involved in this project.

---

## 2. Left Panel Buttons (Core Utilities)

### 2.1 System Info
<img width="736" height="465" alt="Screenshot from 2025-12-31 23-27-09" src="https://github.com/user-attachments/assets/45b4f8b9-7445-43df-9079-3b8ab01e9db9" />

**Description:**
Provides real-time information about the current system state.

**Functions:**

* Displays CPU usage
* Displays RAM usage
* Shows basic system and OS details

**Use Case:**
Allows users to quickly monitor system health without opening terminal commands or external system-monitor applications.

---

### 2.2 Reminder
<img width="630" height="380" alt="Screenshot from 2025-12-31 23-27-34" src="https://github.com/user-attachments/assets/1a868eb5-f1b4-4809-a8f9-2416ddf00b2e" />

**Description:**
Manages scheduled reminders.

**Functions:**

* Create time- or date-based reminders
* Runs continuously in the background
* Triggers notifications when time is reached

**Use Case:**
Used for task deadlines, study reminders, meetings, and important alerts while Taskbot runs silently in the background.

---

### 2.3 Timer
<img width="709" height="230" alt="Screenshot from 2025-12-31 23-27-59" src="https://github.com/user-attachments/assets/5adb51e2-2dff-420b-b30b-6e63da01b0ff" />

**Description:**
Provides a simple countdown timer.

**Functions:**

* Start and stop timers
* Notify when the timer finishes

**Use Case:**
Useful for focused work sessions, break timing, or short-duration task tracking.

---

### 2.4 Converter
<img width="695" height="351" alt="Screenshot from 2025-12-26 22-36-34" src="https://github.com/user-attachments/assets/9b92d59c-46ba-49e6-9b12-e709572666de" />

**Description:**
Performs quick value and unit conversions.

**Functions:**

* Number system conversions (binary, decimal, hexadecimal)
* Other basic logical or numeric conversions

**Use Case:**
Designed for students and developers who need instant conversions without switching applications.

---

### 2.5 Setting
<img width="528" height="322" alt="Setting" src="https://github.com/user-attachments/assets/1d7807c3-60f9-4ad6-9c57-3e5a7bd61117" />

**Description:**
Controls Taskbot configuration and behavior.

**Functions:**

* Enable or disable UI buttons
* Apply configuration fetched from API
* Control shortcuts and behavior settings

**Use Case:**
Allows customization of Taskbot without recompiling the application and supports dynamic feature control.

---

## 3. Right Panel Buttons (Action Tools)

### 3.1 Notes
<img width="967" height="571" alt="Screenshot from 2025-12-27 21-16-59" src="https://github.com/user-attachments/assets/e2275ccd-a28c-4085-9eaa-d391409809a0" />

**Description:**
Provides quick note-taking functionality.

**Functions:**

* Create and view text notes
* Store short or temporary information

**Use Case:**
Used for jotting down ideas, reminders, or short notes during work or study sessions.

---

### 3.2 CMD
<img width="835" height="548" alt="image" src="https://github.com/user-attachments/assets/4eb08737-3304-4915-99e2-93d8b3e91f7d" />

**Description:**
Allows execution of system commands.

**Functions:**

* Open terminal or execute predefined commands
* Display command output inside the application

**Use Case:**
Designed for developers and advanced users who frequently interact with system commands.

---

### 3.3 Apps
<img width="473" height="376" alt="Apps" src="https://github.com/user-attachments/assets/2bf52162-641f-4193-a599-7d84af9c2c11" />

**Description:**
Acts as an application launcher.

**Functions:**

* Launch commonly used applications
* Provide fast access to user-defined apps

**Use Case:**
Reduces time spent searching through system menus by centralizing app launching.

---

### 3.4 SMS
<img width="571" height="413" alt="Screenshot from 2025-12-28 00-45-49" src="https://github.com/user-attachments/assets/a6b331ac-2fd3-46e9-a971-c5f07c0e66d8" />

**Description:**
Text-based messaging and notification module.

**Functions:**

* Display messages or logs
* Handle text-based communication features

**Use Case:**
Serves as a centralized message panel and is designed for future communication-related extensions.

---

## 4. Bottom Interaction Area

### 4.1 Text Input Box

**Description:**
Primary user interaction field.

**Functions:**

* Accepts commands or messages
* Acts as a chat-style input interface

**Use Case:**
Allows users to control Taskbot using typed commands instead of navigating multiple menus.

---

### 4.2 Send Button

**Description:**
Submits user input.

**Functions:**

* Processes entered commands or messages

**Use Case:**
Triggers Taskbot logic and actions based on user input.

---

### 4.3 Clear Button

**Description:**
Clears displayed output.

**Functions:**

* Removes previous messages and logs from the display

**Use Case:**
Keeps the interface clean and focused during extended use.

---

## 5. Central Display Area

**Description:**
Main content and output area of Taskbot.

**Functions:**

* Displays messages, results, and system feedback
* Shows visual status elements when required

**Use Case:**
Acts as a unified output region for all Taskbot features.

---

## 6. Summary

Taskbot’s button layout is designed for **speed, simplicity, and productivity**. Each button represents a self-contained module that can be accessed instantly while the application continues running in the background.

This design makes Taskbot suitable for:

* Desktop productivity enhancement
* Developer-focused workflows
* Academic software projects
* Long-running system assistant applications


---

## 7. AI & Chat Capabilities (Planned / Partial)

* Cleaned AI responses (no unwanted newlines, symbols, markdown noise)
* Taskbot-style personality
* Future integration with local LLMs (e.g., Ollama)
* Designed for:

  * Command understanding
  * Task suggestions
  * Smart reminders

---

## 8. System Control Features

Taskbot is not just a chat app—it can:

* Open terminal windows
* Control Wi-Fi / Bluetooth (GUI-based toggles)
* Launch system tools
* Act as a command hub

---

## 10. Use Cases

* Personal daily task manager
* Student productivity assistant
* System control dashboard
* AI-powered desktop helper

---

## 11. What Makes Taskbot Unique

* Written in **pure C with GTK** (rare today)
* True **non-blocking background execution**
* Deep **system-level integration**
* Keyboard-first workflow
* API + Desktop + Hardware in one ecosystem

---

## 12. Project Status

* Core GUI working
* Background threads implemented
* Keyboard shortcuts functional
* API integration active
* Hardware integration tested
* Actively evolving

---

## 13. Final Summary

**Taskbot** is a serious, system-level productivity assistant—not a toy project. It combines **low-level performance**, **modern features**, and **future-ready extensibility**, reflecting strong skills in **C programming, OS concepts, concurrency, GUI design, and embedded systems**.

This project is strong enough to be:

* A university capstone project
* A GitHub flagship repository
* A foundation for a startup-scale assistant

---

*Designed & developed by Mahabub Alam and team.*
