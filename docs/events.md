# 📡 Events

Eye By Proctorme uses an **event-driven architecture**.  
All monitoring activity (face, audio, tab focus, system checks) is emitted as events from the widget.

Events are subscribed to using:

```ts
widget.on(eventName, callback);
```

---

## Registering Event Listeners

```ts
widget.on("FACE_ABSENCE", (payload) => {
  console.log("Candidate not visible", payload);
});
```

!!! info "Best practice"
    Register all event listeners **before** calling `widget.init(config)`.

---

## Event Payloads

Each event may return:

- No payload
- A metadata payload
- A payload that includes a media file (image or audio)

!!! note "Payload type definitions"
    All payload types are documented separately to avoid duplication.

👉 See: **Payload Types Reference**

---

## Event Reference

### ▶️ Lifecycle Events

| Event | Description | Payload |
|-------|-------------|---------|
| `STARTED` | Fired when proctoring begins | – |
| `END_PROCTORING` | Fired when proctoring ends | – |
| `SET_CONFIG` | Fired when widget configuration is set | `{ config: {...} }` |

---

### 🖥 Fullscreen & Tab Events

| Event | Description | Payload |
|-------|-------------|---------|
| `FULLSCREEN_CHANGE` | Fired when fullscreen mode changes | `{ fullscreen: boolean }` |
| `EXIT_FULLSCREEN` | Fired when candidate exits fullscreen | `FlagData` |
| `TAB_FOCUS_CHANGE` | Fired when tab focus changes | `{ focused: boolean }` |
| `TAB_NOT_FOCUS` | Fired when candidate switches tabs or loses focus | `FlagData` |

---

### 👤 Face Monitoring Events

| Event | Description | Payload |
|-------|-------------|---------|
| `FACE_ABSENCE` | No face detected | `FlagDataWithFile` |
| `MULTIPLE_FACE` | Multiple faces detected | `FlagDataWithFile` |
| `PERIODIC_SNAPSHOT` | Periodic snapshot captured | `FlagDataWithFile` |

---

### 🔊 Audio Monitoring Events

| Event | Description | Payload |
|-------|-------------|---------|
| `SOUND_DETECTED` | Sound detected during assessment | `FlagDataWithFile` |

---

### 🧪 System Check Events

| Event | Description | Payload |
|-------|-------------|---------|
| `SYSTEM_CHECK_STARTED` | System checks have started | – |
| `SYSTEM_CHECK_COMPLETED` | System checks completed | `SystemCheck` |

---

## Example: Handling Multiple Events

```ts
widget.on("STARTED", () => {
  console.log("Proctoring started");
});

widget.on("FACE_ABSENCE", (payload) => {
  console.log(payload.description);
});

widget.on("SOUND_DETECTED", (payload) => {
  console.log(payload.mediaFile);
});

widget.on("END_PROCTORING", () => {
  console.log("Session ended");
});
```

---

## Media Payload Notes

!!! info "Media payloads"
    Events returning `FlagDataWithFile` include a browser `File` object.

    - **Images** → face snapshots
    - **Audio** → detected sound clips

    Media is also stored server-side and may trigger webhooks.

---

## Important Behavior Notes

!!! warning "Events may repeat"
    Monitoring events such as `FACE_ABSENCE` or `SOUND_DETECTED` can fire multiple times during an exam.

!!! tip "Idempotent handling"
    If persisting events, ensure your logic safely handles duplicate payloads.

---

## Client Events vs Webhooks

!!! note
    - Widget events are delivered **client-side**
    - Flags may also be delivered **server-side** via webhooks
    
    👉 See **Webhook Documentation**

---

[ ← API Methods](./api-methods.md){: .md-button } | [Next: Payload Types →](./payload-types.md){: .md-button .md-button--primary }