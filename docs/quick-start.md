# 🚀 Quick Start / Usage Guide

This guide will help you **integrate Eye By Proctorme** into your project and start monitoring candidates in **minutes**.


!!! warning "Tip"

    Ensure the installation script—or, better still, the page DOM—is loaded before calling `LoadEyeWidget()`.


## Load the Widget

After adding the script, the widget exposes a **global function**:

```javascript
const widget = await LoadEyeWidget();
```

This function **returns a Promise**, so you should always use `async/await` or `.then()` to handle it.

---

## Configure Your Session

The widget requires a **configuration object** to initialize a proctoring session. Here's an example:

```javascript
const config = {
  apiKey: "YOUR_API_KEY", // (1)
  assessmentId: "assessment123",
  assessmentTitle: "Frontend Development Assessment",
  candidateId: "candidate456",
  candidateEmail: "test@example.com",
  candidateFirstName: "John",
  candidateLastName: "Doe",
  candidateImageUrl: "https://example.com/avatar.jpg",
  institutionName: "Tech Academy International",
  examDuration: 1800, // In seconds (30 minutes)
  features: {
    aiProctoring: true,
    facialRecognition: true,
  },
};
```

1.   🔑 **API Key**  Used to authenticate requests. Generate it from 
    **Settings → API & Integrations** in the Eye Dashboard. 👉 [Docs](./api-key.md)

!!! info "info"

    - `features.aiProctoring` enables all AI monitoring features.  
    - `features.facialRecognition` enables face verification snapshots.

---

## Initialize the Widget

Once your configuration is ready:

```javascript
await widget.init(config);
console.log("✅ Proctoring session initialized!");
```

> 📝 **Note:** Initialization **starts the system checks** (webcam, microphone, internet speed) automatically.

---

## Listen to Events

The widget is **event-driven**. Use `widget.on(event, callback)` to listen for specific events:

```javascript
widget.on("STARTED", () => console.log("🎬 Proctoring started"));
widget.on("FACE_ABSENCE", (data) => console.warn("🙈 No face detected!", data));
widget.on("MULTIPLE_FACE", (data) => console.warn("🧑‍🧒 Multiple faces detected", data));
widget.on("SOUND_DETECTED", (data) => console.log("🎶 Unexpected sound detected", data));
widget.on("TAB_NOT_FOCUS", (data) => console.log("💻 Tab lost focus", data));
widget.on("PERIODIC_SNAPSHOT", (data) => console.log("📸 Snapshot captured", data));
widget.on("END_PROCTORING", () => console.log("⛔️ Proctoring ended"));
```

---

## Manually Ending a Session

If you need to stop proctoring before the exam ends:

```javascript
widget.endProctoring();
```

!!! info

    Ending the session triggers the `END_PROCTORING` event. All active monitoring stops immediately.

---

## Full Quick Start Example

Here’s the **complete workflow**:

```javascript
<script>
async function startProctoring() {
  try {
    // Load the widget
    const widget = await LoadEyeWidget();

    // Event listeners
    widget.on("STARTED", () => console.log("🎬 Proctoring started"));
    widget.on("FACE_ABSENCE", (data) => console.warn("🙈 No face detected!", data));
    widget.on("MULTIPLE_FACE", (data) => console.warn("🧑‍🧒 Multiple faces detected", data));
    widget.on("SOUND_DETECTED", (data) => console.log("🎶 Unexpected sound detected", data));
    widget.on("TAB_NOT_FOCUS", (data) => console.log("💻 Tab lost focus", data));
    widget.on("PERIODIC_SNAPSHOT", (data) => console.log("📸 Snapshot captured", data));
    widget.on("END_PROCTORING", () => console.log("⛔️ Proctoring ended"));

    // Configuration
    const config = {
      apiKey: "YOUR_API_KEY", // (1)
      assessmentId: "assessment123",
      assessmentTitle: "Frontend Development Assessment",
      candidateId: "candidate456",
      candidateEmail: "test@example.com",
      candidateFirstName: "John",
      candidateLastName: "Doe",
      candidateImageUrl: "https://example.com/avatar.jpg",
      institutionName: "Tech Academy International",
      examDuration: 1800,
      features: { aiProctoring: true, facialRecognition: true },
    };

    // Initialize
    await widget.init(config);
    console.log("✅ Proctoring session initialized!");
  } catch (error) {
    console.error("❌ Failed to start proctoring:", error);
  }
}

startProctoring();
</script>
```

1.   🔑 **API Key**  Used to authenticate requests. Generate it from 
    **Settings → API & Integrations** in the Eye Dashboard. 👉 [Docs](./api-key.md)


---

## Tips & Best Practices

!!! tip "Tips for a smooth integration"
    - Always load the widget asynchronously to prevent blocking your page.  
    - Validate your API key and domains before deployment.  
    - Make your event handlers **idempotent**; same events may fire multiple times.  
    - Test in **different browsers** to ensure compatibility.  

---

## Ready to Go

Once integrated, Eye By Proctorme **automatically handles**:

- Webcam & microphone checks  
- AI-based monitoring  
- Event triggers & flagging  

!!! success "🎉 You are now ready to monitor"

    You are now ready to monitor candidates in real-time with **confidence and compliance**.

---

[ ← Back to Installation](./installation.md){: .md-button } | [Next: Configuration →](./configuration.md){: .md-button .md-button--primary }

