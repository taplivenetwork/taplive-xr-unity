# TapLive XR Integration – Stream Config API (v1)

**Audience:** XR Developers (Unity / Godot / WebXR)  
**Status:** Mock / Pre-Streaming  
**Version:** v1  
**Purpose:** Unblock XR client development before real streaming integration

---

## 1. Overview

This API provides XR clients with a **stream configuration contract** required to initialize
the connection flow.

> ⚠️ This version does **NOT** require a real live video stream.

The goal is to:
- Unblock XR client development
- Align XR clients with backend API contracts
- Allow UI and connection state machines to proceed independently

---

## 2. Endpoint

### `GET /api/v1/stream/config`

Returns a **mock stream configuration** that XR clients can consume to:
- Validate networking
- Parse WebRTC-compatible fields
- Transition UI state from `Loading` → `Ready / Connecting`

---

## 3. Request

### Method

GET


### Headers
```http
Accept: application/json


Authorization is not required in v1 mock
Token handling will be added in later versions

4. Response (Mock v1)
Example
{
  "version": "v1",
  "mode": "mock",
  "stream": {
    "streamId": "demo-stream-001",
    "status": "idle",
    "type": "live"
  },
  "signaling": {
    "url": "wss://mock-signaling.taplivenetwork.local",
    "protocol": "webrtc"
  },
  "iceServers": [
    {
      "urls": "stun:stun.l.google.com:19302"
    }
  ],
  "auth": {
    "token": "mock-token",
    "expiresAt": null
  }
}

5. Field Semantics (XR Perspective)
Root Fields
Field	Description
version	API version
mode	mock or live (future)
stream
Field	Description
streamId	Logical identifier for XR session
status	Initial state (idle)
type	Reserved for future use
signaling
Field	Description
url	Placeholder signaling endpoint
protocol	Signaling protocol (webrtc)

⚠️ In mock mode, signaling is not active

iceServers

Standard WebRTC ICE configuration.

Must be parsed by:

Unity WebRTC

Godot WebRTC

Any WebRTC-compatible XR stack

auth
Field	Description
token	Mock auth token
expiresAt	Always null in mock
6. Expected XR Client Behavior
XR Client SHOULD

Call /api/v1/stream/config

Parse the JSON response successfully

Initialize internal connection state

Update UI state:

Loading → Ready or Connecting

Log or display mock mode clearly

XR Client SHOULD NOT

Assume a real video stream exists

Block execution waiting for media tracks

Treat signaling failure as a fatal error in mock mode

7. Success Criteria (v1 Mock)

Integration is considered successful when:

API request succeeds

Response is parsed without errors

XR UI progresses past Failed to fetch

Connection state machine runs

❌ A real live video stream is NOT required

8. Engine Independence

This API is engine-agnostic and behaves the same for:

Unity

Godot

Unreal

WebXR

Switching engines does not change behavior unless the API contract changes.

9. Forward Compatibility

This endpoint is designed to evolve into a live streaming configuration API.

Planned future extensions:

Real signaling URLs

Valid auth tokens

LiveKit / Agora / native WebRTC integration

Media codec metadata

Permission scopes

Existing fields will be extended, not removed.

10. Summary for XR Developers

This API exists to let XR development continue now,
without waiting for backend streaming infrastructure.

If your XR client can consume this endpoint correctly,
it is aligned with the backend roadmap.
