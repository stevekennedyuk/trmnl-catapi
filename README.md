# TRMNL Cat Plugin

Displays random cats from [The Cat API](https://thecatapi.com/) on your TRMNL e-ink display.
When breed information is available, it is shown in the title bar and body.

## Setup

### Polling URL
```
https://api.thecatapi.com/v1/images/search?limit=1&has_breeds=1
```

> The `&has_breeds=1` parameter ensures a breed is always returned.
> Remove it if you want all cats (breed fields will then be blank and fallbacks apply).

### Polling Headers
```
x-api-key=live_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
Replace with your actual Cat API key from https://thecatapi.com/

### Polling Verb
```
GET
```

---

## Layout Files

| File | Best for | Shows |
|---|---|---|
| `full.liquid` | Full screen | Large image, breed + origin in title bar, temperament as subtitle |
| `half_horizontal.liquid` | Half width | Image left, breed details (name, origin, lifespan, temperament) right |
| `half_vertical.liquid` | Half height | Image top, breed name + origin + temperament below |
| `quadrant.liquid` | Quarter screen | Image only, breed name (or instance name) in title bar |

---

## Graceful Fallbacks

All layouts handle missing breed data cleanly:
- If `breeds` is empty, the title bar shows `instance_name` instead
- The cat's `id` is always shown as the instance subtitle
- No errors or blank panels

---

## Cat API Response Structure

The API returns an array — TRMNL exposes it as `data[0]`:

```json
[{
  "id": "abc123",
  "url": "https://cdn2.thecatapi.com/images/abc123.jpg",
  "breeds": [{
    "name": "Bengal",
    "origin": "United States",
    "life_span": "12 - 16",
    "temperament": "Alert, Agile, Energetic, Demanding, Intelligent"
  }]
}]
```
