# ⚙️ Configuration

This page documents the **configuration object** used to initialize the **Eye By Proctorme** widget.

The configuration defines:
- Which assessment is being proctored
- Who the candidate is
- How long the exam lasts
- Which proctoring features are enabled

All fields listed here are derived **directly from the widget API**.

---

## Configuration Object Overview

The widget is initialized using a single `config` object passed to:

```ts
widget.init(config);
```

Example:

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
  examDuration: 1800,
  features: {
    aiProctoring: true,
    facialRecognition: true,
  },
};
```

1.   🔑 **API Key**  Used to authenticate requests. Generate it from 
    **Settings → API & Integrations** in the Eye Dashboard. 👉 [Docs](./api-key.md)
    
---

## `apiKey` **(Required)**

Your organisation’s **Eye API key**.

```ts
apiKey: "YOUR_API_KEY"
```

!!! info "How to get your API key"
    Generate and copy your API key from the Eye admin dashboard:

    **Settings → API & Integrations**  
    👉 [API Key documentation](./api-key.md)


---

## `assessmentId` (Required)

A unique identifier for the assessment being proctored.

```ts
assessmentId: "assessment123"
```

- Must match an assessment created in the Eye dashboard
- Used to associate flags and events with the correct exam

---

## `assessmentTitle` **(Required)**

The human‑readable title of the assessment.

```ts
assessmentTitle: "Frontend Development Assessment"
```

This value is used for:
- Logging
- Reporting
- Candidate review records

---

## `candidateId` **(Required)**

A unique identifier for the candidate.

```ts
candidateId: "candidate456"
```

This ID links all monitoring events and flags to the candidate.

---

## `candidateEmail` **(Required)**

The candidate’s email address.

```ts
candidateEmail: "test@example.com"
```

Used for:
- Identification
- Reporting
- Administrative review

---

## `candidateFirstName` **(Required)**

The candidate’s first name.

```ts
candidateFirstName: "John"
```

---

## `candidateLastName` **(Required)**

The candidate’s last name.

```ts
candidateLastName: "Doe"
```

---

## `institutionName` **(Required)**

The name of the institution conducting the assessment.

```ts
institutionName: "Tech Academy International"
```

Appears in:
- Logs
- Reports
- Admin dashboard views

---

## `examDuration` **(Required)**

Duration of the exam **in seconds**.

```ts
examDuration: 1800
```

!!! tip "Example durations"
    - 30 minutes → `1800`
    - 1 hour → `3600`
    - 2 hours → `7200`

---

## `candidateImageUrl` *(Optional)*

URL to a reference image of the candidate.

```ts
candidateImageUrl: "https://example.com/avatar.jpg"
```

Used for:
- Facial recognition comparison
- Identity verification

!!! note "Optional"
    If omitted, facial recognition can still run but without a reference image.

---

## `features` *(Optional)*

Controls which proctoring features are enabled.

```ts
features: {
  aiProctoring: true,
  facialRecognition: true,
}
```

### Available Feature Flags

| Feature | Type | Description |
|------|------|------------|
| `aiProctoring` | boolean | Enables AI‑based monitoring (face, sound, tab focus) |
| `facialRecognition` | boolean | Enables facial recognition snapshots |

!!! info "Default behavior"
    If `features` is omitted, all supported proctoring features may be enabled by default.

---

## Minimal Required Configuration

```ts
const config = {
  apiKey: "YOUR_API_KEY", // (1)
  assessmentId: "assessment123",
  assessmentTitle: "Assessment Title",
  candidateId: "candidate456",
  candidateEmail: "candidate@email.com",
  candidateFirstName: "First",
  candidateLastName: "Last",
  institutionName: "Institution Name",
  examDuration: 1800,
};
```

1.   🔑 **API Key**  Used to authenticate requests. Generate it from 
    **Settings → API & Integrations** in the Eye Dashboard. 👉 [Docs](./api-key.md)
---

## Validation Notes

!!! warning "Initialization will fail if:"
    - Required fields are missing
    - The API key is invalid
    - The domain is not registered for the API key

---

[ ← Quick Start Guide →](./quick-start.md){: .md-button } | [Next: API Methods →](./api-methods.md){: .md-button .md-button--primary }

