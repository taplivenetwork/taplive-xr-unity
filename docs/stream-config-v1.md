# TapLive Stream Configuration API – v1

Status: Mock (Pre-Streaming)  
API Version: v1  
Audience: Backend / XR Integration  
Purpose: Provide a stable API contract for XR clients before real streaming integration

---

## Overview

The Stream Configuration API provides XR clients with the minimum required
configuration to initialize a streaming connection workflow.

In v1, this API operates in **mock mode** and does NOT require:
- A real live video stream
- A running signaling server
- Media track availability

This endpoint exists to:
- Unblock XR client development
- Establish a clear backend ↔ XR API contract
- Allow parallel development between backend and XR teams

---

## Endpoint Definition

### GET /api/v1/stream/config

Returns a stream configuration object that is compatible with
WebRTC-based XR clients (Unity, Godot, WebXR).

---

## Request

### Method
GET

### Headers
```http
Accept: application/json

Authorization is optional in v1 and not enforced in mock mode.

Response
200 OK (Mock Mode)
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

Field Specification
Root Fields
Field	Type	Description
version	string	API version
mode	string	mock (v1) or live (future)
stream
Field	Type	Description
streamId	string	Logical identifier for the XR session
status	string	Initial stream state (idle)
type	string	Reserved for future expansion
signaling
Field	Type	Description
url	string	Placeholder signaling WebSocket URL
protocol	string	Signaling protocol (webrtc)

In v1 mock mode, the signaling URL is not expected to be reachable.

iceServers

Standard WebRTC ICE server configuration.

This field must be compatible with:

Unity WebRTC

Godot WebRTC

Browser-based WebRTC clients

auth
Field	Type	Description
token	string	Mock authentication token
expiresAt	string | null	Token expiration time (null in mock mode)
Expected Backend Behavior (v1)

The backend should:

Always return HTTP 200 with a valid JSON body

Return consistent field names and types

Clearly indicate mock mode via the mode field

The backend should NOT:

Attempt to establish real signaling connections

Require a live stream to exist

Block responses based on stream availability

Error Handling (Optional)
503 Service Unavailable
{
  "error": "SERVICE_NOT_READY",
  "message": "Stream configuration service is initializing"
}

Versioning Strategy

This endpoint is versioned under /api/v1 to allow future evolution.

Planned non-breaking extensions include:

Switching mode to live

Providing real signaling URLs

Issuing valid authentication tokens

Adding media codec metadata

Adding permission and capability fields

Existing fields will be extended, not removed.

Implementation Notes

This endpoint may be implemented as a static or mocked response in v1

It serves as an API contract, not a final streaming solution

XR clients depend on this contract to proceed with development

Summary

The Stream Configuration API v1 establishes a stable interface between
the TapLive backend and XR clients.

It enables immediate XR progress while preserving a clean upgrade path
to real-time streaming infrastructure in future versions.


---

## ✅ Commit Example (use directly)

**Commit message：**

docs: add stream configuration API v1 (mock)
