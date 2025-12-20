# Excalidraw Style Guide

> Consistent hand-drawn style for all system design diagrams.

---

## 🎨 Default Settings

When creating diagrams in Excalidraw, use these settings:

### Stroke Style
- **Stroke style**: Hand-drawn (default)
- **Stroke width**: Medium (default)
- **Roughness**: 1 (slightly rough)
- **Edges**: Round

### Colors to Use

```
BACKGROUNDS:
- Blue boxes:     #DBEAFE (light) / #3B82F6 (border)
- Green boxes:    #D1FAE5 (light) / #10B981 (border)  
- Orange boxes:   #FEF3C7 (light) / #F59E0B (border)
- Purple boxes:   #EDE9FE (light) / #8B5CF6 (border)
- Gray boxes:     #F1F5F9 (light) / #64748B (border)
- Red boxes:      #FEE2E2 (light) / #EF4444 (border)

ARROWS:
- Primary:        #3B82F6 (blue)
- Secondary:      #64748B (gray)
- Data flow:      #10B981 (green)
- Error/Warning:  #EF4444 (red)

TEXT:
- Headers:        #1E293B (dark)
- Body:           #475569 (gray)
- Labels:         #64748B (light gray)
```

---

## 📐 Component Templates

### Server/Service Box
```
┌─────────────────────┐
│    🖥️ Service Name   │  ← Icon + Name
├─────────────────────┤
│   Description       │  ← Optional description
│   (Technology)      │  ← Technology used
└─────────────────────┘

Color: Blue background (#DBEAFE)
Border: Blue (#3B82F6)
Size: 150-200px width
```

### Database
```
    ╭─────────╮
   ╱           ╲
  │  Database  │  ← Cylinder shape
  │   Name     │
   ╲           ╱
    ╰─────────╯

Color: Green background (#D1FAE5)
Border: Green (#10B981)
```

### User/Client
```
    ○
   /│\    ← Stick figure or user icon
   / \
  User

Color: Purple (#8B5CF6)
```

### Cloud/External Service
```
  ☁️ AWS/GCP/Azure

Color: Orange (#FEF3C7)
Border: Orange (#F59E0B)
```

### Cache
```
  ⚡ Redis/Cache

Color: Red/Orange (#FEF3C7)
Icon: Lightning bolt
```

### Load Balancer
```
     ╱───╲
    │ LB  │  ← Hexagon or diamond shape
     ╲───╱

Color: Purple (#EDE9FE)
```

---

## 🔄 Arrow Styles

### Request/Response
```
────────────▶  Solid arrow for requests
◀─ ─ ─ ─ ─ ─  Dashed arrow for responses
```

### Data Flow
```
═══════════▶  Thick arrow for data stream
```

### Async/Events
```
- - - - - -▶  Dashed arrow for async
```

---

## 📏 Layout Rules

1. **Flow Direction**: Left-to-right or top-to-bottom
2. **Spacing**: Keep consistent gaps (40-60px between elements)
3. **Grouping**: Use light gray boxes to group related components
4. **Labels**: Always label arrows with action/data type
5. **Legend**: Add legend for complex diagrams

---

## 📱 Export Settings

### For Social Media
- **Scale**: 2x (for crisp images)
- **Background**: White or transparent
- **Format**: PNG
- **Dimensions**: 
  - LinkedIn: 1200 x 627
  - Instagram: 1080 x 1080
  - Twitter: 1200 x 675

### For GitHub
- **Format**: SVG (scalable)
- **Background**: Transparent

---

## 🖼️ Template Examples

### Basic Client-Server Architecture
```
[User] ──▶ [Load Balancer] ──▶ [Server 1]
                           └──▶ [Server 2] ──▶ [Database]
                           └──▶ [Server 3]
```

### Microservices Layout
```
                    ┌── [Service A] ──┐
[API Gateway] ──────┼── [Service B] ──┼── [Database]
                    └── [Service C] ──┘
                           │
                    [Message Queue]
```

### Caching Layer
```
[Client] ──▶ [CDN] ──▶ [Load Balancer] ──▶ [App Server]
                                              │
                                    ┌─────────┼─────────┐
                                    ▼         ▼         ▼
                               [Redis]   [Database]  [S3]
```

---

## 🎯 Quick Checklist

Before exporting:
- [ ] All boxes aligned
- [ ] Consistent colors used
- [ ] Arrows labeled
- [ ] Text readable at export size
- [ ] No overlapping elements
- [ ] Legend included (if needed)

