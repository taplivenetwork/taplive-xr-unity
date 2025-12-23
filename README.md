# taplive-xr-unity

TapLive XR client implementation (Unity)

## TapLive XR Client (Unity)

This repository contains the Unity-based implementation of the TapLive XR client.

## Scope

- Client-side XR implementation only
- Backend logic lives in the TapLive web backend
- The XR client connects via configurable backend endpoints
- Rendering, input handling, and XR interaction are handled by Unity

## Responsibilities

The XR client is responsible for:
- Establishing sessions with the TapLive backend
- Rendering real-time presence and interaction
- Handling XR input (head tracking, controllers, gestures)
- Displaying spatial UI and live data

The XR client does NOT:
- Own backend business logic
- Manage authentication or data persistence
- Implement custom networking protocols beyond consuming backend APIs

## Tech Stack

- Unity (XR / OpenXR)
- C#
- OpenXR-compatible devices

## Status

Early development / initial setup.
