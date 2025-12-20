# Diagrams: Chapter 01 - Introduction

> Excalidraw specifications for creating shareable diagrams.

---

## Diagram 1: System Evolution (Most Popular!)

**Best for**: Instagram, LinkedIn
**Size**: 1080 x 1080

### Excalidraw Specification

```
TITLE: "How Systems Scale: 100 to 10M Users"

LAYOUT: Vertical stack, 5 stages

STAGE 1 (Top):
├── Label: "100 Users"
├── Box: Single server icon + "App + DB"
├── Color: Light gray background
└── Arrow down

STAGE 2:
├── Label: "10K Users"  
├── Two boxes: "App Server" → "Database"
├── Color: Light blue
└── Arrow down

STAGE 3:
├── Label: "100K Users"
├── Three boxes: "App" → "Cache (Redis)" → "DB"
├── Color: Light green
└── Arrow down

STAGE 4:
├── Label: "1M Users"
├── Layout: 
│   └── "Load Balancer" 
│        ├── "Server 1" ─┐
│        ├── "Server 2" ─┼──→ "Cache" → "DB"
│        └── "Server 3" ─┘
├── Color: Light orange
└── Arrow down

STAGE 5 (Bottom):
├── Label: "10M+ Users"
├── Layout:
│   └── "LB" → Multiple servers → "Cache Cluster"
│                               → "DB Shard 1"
│                               → "DB Shard 2"  
│                               → "DB Shard 3"
└── Color: Light purple

FOOTER: "@yourhandle | System Design Guide"
```

### Colors to Use
- Stage 1: `#F1F5F9` (gray)
- Stage 2: `#DBEAFE` (blue)
- Stage 3: `#D1FAE5` (green)
- Stage 4: `#FEF3C7` (orange)
- Stage 5: `#EDE9FE` (purple)

---

## Diagram 2: Building Blocks

**Best for**: Carousel slide, Twitter
**Size**: 1080 x 1080 or 1200 x 675

### Excalidraw Specification

```
TITLE: "System Design Building Blocks"

LAYOUT: 3x3 Grid

ROW 1:
├── 🌐 DNS          │ 📡 CDN        │ ⚖️ Load Balancer
└── "Name → IP"     │ "Edge cache"  │ "Traffic dist."

ROW 2:
├── 🖥️ Servers      │ 💾 Database   │ ⚡ Cache
└── "App logic"     │ "Data store"  │ "Fast access"

ROW 3:
├── 📬 Queue        │ 📦 Storage    │ 🔍 Search
└── "Async work"    │ "Files/media" │ "Full-text"

STYLE:
- Each cell: 280 x 280px
- Icon: Large centered emoji
- Label: Bold below icon
- Description: Small gray text
- Background: Each cell slightly different shade
```

---

## Diagram 3: HLD vs LLD Comparison

**Best for**: Educational posts
**Size**: 1200 x 675 (Twitter) or 1080 x 1080 (Instagram)

### Excalidraw Specification

```
TITLE: "HLD vs LLD: What's the Difference?"

LAYOUT: Two columns with VS in middle

LEFT COLUMN (Blue theme):
┌─────────────────────────────┐
│     HIGH LEVEL DESIGN       │
│         (HLD)               │
├─────────────────────────────┤
│ 🎯 Focus: Architecture      │
│ 📊 Output: Diagrams         │
│ 👥 Audience: Architects     │
│                             │
│ Answers:                    │
│ • WHAT components?          │
│ • WHERE do they go?         │
│ • HOW do they communicate?  │
└─────────────────────────────┘

CENTER:
[ VS ]

RIGHT COLUMN (Green theme):
┌─────────────────────────────┐
│     LOW LEVEL DESIGN        │
│         (LLD)               │
├─────────────────────────────┤
│ 🎯 Focus: Implementation    │
│ 📊 Output: Code/Classes     │
│ 👥 Audience: Developers     │
│                             │
│ Answers:                    │
│ • HOW to implement?         │
│ • WHAT algorithms?          │
│ • WHICH data structures?    │
└─────────────────────────────┘
```

---

## Diagram 4: RESHADE Framework

**Best for**: Cheatsheet, save-worthy content
**Size**: 1080 x 1350 (Portrait)

### Excalidraw Specification

```
TITLE: "The RESHADE Framework for System Design"

LAYOUT: Vertical list with icons

┌─────────────────────────────────────┐
│ 🏗️ RESHADE FRAMEWORK               │
│    Master Any System Design         │
├─────────────────────────────────────┤
│                                     │
│ R │ REQUIREMENTS                    │
│   │ What must the system do?        │
│   │ Functional + Non-functional     │
│   └─────────────────────────────────│
│                                     │
│ E │ ESTIMATION                      │
│   │ How much traffic & storage?     │
│   │ Back-of-envelope math           │
│   └─────────────────────────────────│
│                                     │
│ S │ STORAGE                         │
│   │ Database design                 │
│   │ SQL vs NoSQL decision           │
│   └─────────────────────────────────│
│                                     │
│ H │ HIGH LEVEL DESIGN               │
│   │ Architecture diagram            │
│   │ Major components                │
│   └─────────────────────────────────│
│                                     │
│ A │ API DESIGN                      │
│   │ Endpoints & interfaces          │
│   │ REST/GraphQL/gRPC               │
│   └─────────────────────────────────│
│                                     │
│ D │ DEEP DIVES                      │
│   │ Scaling & bottlenecks           │
│   │ Trade-off discussions           │
│   └─────────────────────────────────│
│                                     │
│ E │ EDGE CASES                      │
│   │ Failure scenarios               │
│   │ Security & monitoring           │
│   └─────────────────────────────────│
│                                     │
├─────────────────────────────────────┤
│ Save this! 🔖  @yourhandle          │
└─────────────────────────────────────┘

COLORS:
- R: Red accent (#EF4444)
- E: Orange accent (#F59E0B)
- S: Yellow accent (#EAB308)
- H: Green accent (#10B981)
- A: Teal accent (#14B8A6)
- D: Blue accent (#3B82F6)
- E: Purple accent (#8B5CF6)
```

---

## Diagram 5: Netflix Architecture (Simple)

**Best for**: Case study posts
**Size**: 1200 x 675

### Excalidraw Specification

```
TITLE: "How Netflix Serves 200M Users"

LAYOUT: Left to right flow

┌────────────┐    ┌─────────────┐    ┌────────────────┐
│   Users    │    │    CDN      │    │   AWS Backend  │
│ ┌──┐ ┌──┐  │───▶│ Open Connect│    │ ┌────────────┐ │
│ │📱│ │💻│  │    │ ┌──┐ ┌──┐   │───▶│ │Microservices│
│ └──┘ └──┘  │    │ │🖥️│ │🖥️│   │    │ └────────────┘ │
│   ┌──┐     │    │ └──┘ └──┘   │    │       │        │
│   │📺│     │    │   Edge      │    │ ┌─────┴──────┐ │
│   └──┘     │    │  Servers    │    │ │ Cassandra  │ │
└────────────┘    └─────────────┘    │ │  EVCache   │ │
                                     └────────────────┘

LABELS:
- Arrow 1: "Video Streaming (95%)"
- Arrow 2: "API Calls"

STATS BOX (bottom):
┌──────────────────────────────────────┐
│ 📊 15% of global internet traffic    │
│ 🎬 1B hours watched per week         │
│ 🌍 190+ countries                    │
└──────────────────────────────────────┘
```

---

## 📥 Export Instructions

1. **Open Excalidraw** ([excalidraw.com](https://excalidraw.com))
2. **Create diagram** using specifications above
3. **Select all** (Ctrl/Cmd + A)
4. **Export** → Export image
5. **Settings**:
   - Scale: 2x
   - Background: Include
   - Format: PNG
6. **Save** with naming: `ch01-diagram-name.png`

---

## 📁 File Naming Convention

```
ch01-system-evolution.png
ch01-building-blocks.png
ch01-hld-vs-lld.png
ch01-reshade-framework.png
ch01-netflix-architecture.png
```

