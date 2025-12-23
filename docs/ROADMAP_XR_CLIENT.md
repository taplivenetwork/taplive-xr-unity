# TapLive XR Client — Development Plan (v1)

This document defines the development scope and module-level tasks for the TapLive XR Client.
The XR client is a **Unity-based, client-side application** that consumes backend APIs and renders immersive XR experiences.

---

## Phase 1 — XR Client Foundation

### 1. Project & Environment Setup

- Verify / install Unity (LTS recommended)
- Enable Android and/or Windows build support
- Install OpenXR Plugin via Unity Package Manager
- Configure XR Plug-in Management
- Setup XR Interaction Toolkit

**Goal**  
The project builds and runs successfully on an XR-capable device or simulator.

---

### 2. Core XR Setup

- Create XR Origin (Camera Rig)
- Enable head tracking
- Enable controller and/or gesture input
- Verify basic XR interaction works correctly

**Goal**  
A stable XR runtime environment with reliable tracking and input.

---

## Phase 2 — Immersive Video Rendering

### 3. 360° / 180° Video Viewer

- Setup sphere-based or skybox-based video rendering
- Support mono video playback
- Stereo video support is optional and may be added later
- Implement basic video playback controls:
  - Play
  - Pause
  - Seek

**Goal**  
The XR client can render immersive 360° / 180° video content smoothly.

---

### 4. Basic XR UI

- Create a simple spatial UI panel
- Bind UI controls to video playback actions
- Drive interactions via XR input (controller or gaze)

**Goal**  
Users can control video playback directly inside the XR environment.

---

## Phase 3 — Backend Integration (Client-side Only)

### 5. Backend Connectivity

- Support a configurable backend base URL
- Implement placeholder or mock API calls:
  - Join session
  - Fetch stream or video metadata
- Handle missing or unavailable backend data gracefully

**Goal**  
The XR client behaves as a backend-driven application, even when backend responses are mocked or incomplete.

---

## Phase 4 — Documentation & Developer Experience

### 6. Documentation

- Project setup guide (`README.md`)
- Usage instructions
- Basic architecture overview

**Goal**  
Another developer can clone, run, and understand the XR client without direct assistance.

---

## Explicit Non-Goals

The XR client does **NOT**:

- Implement backend business logic
- Manage authentication or user accounts
- Store persistent data
- Define or maintain streaming protocols
- Replace or duplicate the TapLive web backend

These responsibilities belong exclusively to the backend system.

---

## Success Definition (v1)

A successful v1 XR client:

- Runs on Unity with OpenXR enabled
- Renders immersive 360° / 180° video
- Accepts XR input (head tracking, controllers, or gestures)
- Connects to a configurable backend endpoint
- Provides a clean foundation for future live presence features
