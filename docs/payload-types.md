# 📦 Payload Types

This document defines all **payload structures** emitted by the Eye By Proctorme widget and backend systems.

These types are used by:

- Client-side **widget events**
- Server-side **flag webhooks**
- Internal logging and audit records

!!! info "Single source of truth"
    All event and webhook documentation references this page to avoid duplication and inconsistencies.

---

## Common Fields

Most payloads include the following shared fields:

| Field | Type | Description |
|-------|------|-------------|
| `examId` | string | Unique identifier of the assessment |
| `candidateId` | string | Unique identifier of the candidate |
| `type` | `Event` | Event or flag type |
| `description` | string | Human-readable description |
| `createdAt` | string | ISO timestamp of occurrence |

---

## FlagData

Represents a **non-media proctoring flag**.

**Used by:**

- `EXIT_FULLSCREEN`
- `TAB_NOT_FOCUS`
- Backend flag records

### Type Definition

```ts
type FlagData = {
  examId: string;
  candidateId: string;
  type: Event;
  description: string;
  createdAt: string;
};
```

---

## FlagDataWithFile

Represents a proctoring flag that includes a media file (image or audio).

**Used by:**

- `FACE_ABSENCE`
- `MULTIPLE_FACE`
- `SOUND_DETECTED`
- `PERIODIC_SNAPSHOT`

### Type Definition

```ts
type FlagDataWithFile = {
  examId: string;
  candidateId: string;
  mediaFile: File;
  type: Event;
  description: string;
  createdAt: string;
};
```

!!! info "Media file"
    `mediaFile` is a browser `File` object and may represent:
    
    - An image snapshot
    - An audio recording

---

## SystemCheck

Returned when system compatibility checks complete.

**Used by:**

- `SYSTEM_CHECK_COMPLETED`

### Type Definition

```ts
type SystemCheck = {
  success: boolean;
  timestamp: string;
  data: {
    status: "success" | "failed" | "default";
    finished: boolean;
    name: "internetSpeed" | "webcam" | "microphone" | "browser";
  }[];
};
```

### Example Payload

```json
{
  "success": true,
  "timestamp": "2025-09-21T12:00:00.000Z",
  "data": [
    {
      "name": "webcam",
      "status": "success",
      "finished": true
    },
    {
      "name": "microphone",
      "status": "success",
      "finished": true
    }
  ]
}
```

---

## Event (Enum-like)

The `type` field references a known event name.

Common values include:

```ts
type Event =
  | "STARTED"
  | "END_PROCTORING"
  | "SET_CONFIG"
  | "FULLSCREEN_CHANGE"
  | "EXIT_FULLSCREEN"
  | "TAB_FOCUS_CHANGE"
  | "TAB_NOT_FOCUS"
  | "FACE_ABSENCE"
  | "MULTIPLE_FACE"
  | "SOUND_DETECTED"
  | "PERIODIC_SNAPSHOT"
  | "SYSTEM_CHECK_STARTED"
  | "SYSTEM_CHECK_COMPLETED";
```

!!! note
    `Event` values are emitted as strings, not numeric enums.

---

<!-- ## 🔗 Relationship to Webhooks

!!! info
    - Widget events return `File` objects (`mediaFile`)
    - Webhook payloads return `mediaUrl` instead

| Context | Media Field |
|---------|-------------|
| Widget events | `mediaFile: File` |
| Webhooks | `mediaUrl: string` |

👉 See **Webhook Documentation**

--- -->

## Handling Recommendations

!!! tip "Persisting payloads"
    Store `examId`, `candidateId`, `type`, and `createdAt` as primary identifiers.

---

[ ← Back to Events](./installation.md){: .md-button } | [Next: Browser Support →](./configuration.md){: .md-button .md-button--primary }