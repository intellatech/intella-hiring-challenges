# Intella Frontend Engineer Assessment

**Project:** Satellite Telemetry Dashboard

## Context

At Intella, we build AI-powered software for satellite operations. A critical capability is visualizing satellite telemetry data through intuitive, customizable dashboards that enable operators to monitor system health and identify anomalies.

Your task is to build a **minimal but well-designed dashboard visualization system** using Next.js, TypeScript, and Mantine UI. This assessment evaluates your ability to:

- Design intuitive, responsive user interfaces
- Create reusable, composable visualization components
- Handle time-series data visualization effectively
- Build flexible, user-configurable dashboard layouts
- Write clean, maintainable TypeScript code

## Domain Model

The dashboard visualizes telemetry data from satellite sensors organized in a hierarchical structure:

```
Satellite (e.g., "Intella-Sat-1")
└── Sensor Category (e.g., "Power System", "Thermal Control")
    └── Sensor (individual sensor: voltage, temperature, pressure, etc.)
        └── Time-series Data Points (timestamp, value)
```

**Available Sensor Types:**

| Sensor Type | Unit | Typical Range | Description |
|-------------|------|---------------|-------------|
| `voltage` | V | 11.5 - 13.0 | Battery and system voltage |
| `temperature` | °C | -20 to 50 | Internal/external temperatures |
| `pressure` | bar | 0.8 - 1.2 | Cabin/tank pressure |
| `battery_level` | % | 0 - 100 | Battery charge percentage |
| `signal_strength` | dBm | -90 to -40 | Communication signal quality |
| `current` | A | 0 - 10 | Power system current draw |

## Requirements

### 1. Dashboard Canvas System

Implement a configurable dashboard canvas where users can:

- **Add widgets**: Place multiple visualization widgets on the canvas
- **Resize widgets**: Adjust width and height of each widget
- **Position widgets**: Arrange widgets in a grid or free-form layout
- **Remove widgets**: Delete unwanted widgets from the dashboard

**Widget Types (Minimum Required):**

| Widget | Description | Priority |
|--------|-------------|----------|
| **Text/Metric Card** | Display current sensor value with label | Required |
| **Line Chart** | Time-series visualization | Required |
| **Scatter Plot** | Value distribution over time | Required |
| **Pie/Donut Chart** | Categorical distribution | Required |
| **Box Plot** | Statistical distribution view | Optional |

### 2. Data & Filtering

Generate and visualize mock telemetry data:

- **Mock Data Generator**: Create realistic time-series data for at least 5 sensor types
- **Time Range**: Generate data for the past 24 hours with readings every 10 seconds
- **Realistic Patterns**: Values should follow realistic patterns (gradual changes, no random jumps)

**Filtering Capabilities:**

- **Global Date Filter**: Apply date range filter to all widgets simultaneously
- **Per-Widget Date Filter**: Override global filter for individual widgets
- **Sensor Selection**: Choose which sensor type to display in each widget

### 3. Technology Stack

| Technology | Purpose |
|------------|---------|
| **Next.js 14+** | React framework with App Router |
| **TypeScript** | Type-safe development |
| **Mantine UI** | Component library for UI elements |
| **Recharts** or **Chart.js** | Data visualization (or equivalent) |

**Recommended Mantine Components:**

- `AppShell` - Dashboard layout structure
- `Grid` / `SimpleGrid` - Widget positioning
- `Card` - Widget containers
- `DatePickerInput` / `DateRangePicker` - Date filtering
- `Select` / `MultiSelect` - Sensor type selection
- `Switch` / `Checkbox` - Toggle controls
- `Modal` - Widget configuration dialogs
- `Menu` - Context menus and dropdowns
- `Tabs` - Dashboard navigation
- `ActionIcon` / `Button` - User interactions

### 4. User Interface Requirements

Design a clean, professional dashboard interface:

- **Header**: App title, global filters, user actions
- **Sidebar** (optional): Widget palette, navigation
- **Main Canvas**: Widget grid with drag/resize capabilities
- **Widget Toolbar**: Per-widget controls (sensor selection, date filter, remove)

**Responsive Design:**

- Desktop-first approach (1280px+ target)
- Graceful degradation for tablet sizes
- Mobile responsiveness is a bonus, not required

### 5. Code Quality Standards

Your code must demonstrate professional software engineering practices:

- **TypeScript**: Strict mode enabled, proper type definitions
- **ESLint**: Follow Next.js recommended rules
- **Prettier**: Consistent code formatting
- **Component Structure**: Logical organization, reusable components
- **Clean Code**: Meaningful names, proper abstraction, DRY principles

**Project Structure (Suggested):**

```
frontend/
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── layout.tsx
│   │   ├── page.tsx            # Dashboard page
│   │   └── login/
│   │       └── page.tsx        # Login page (optional)
│   ├── components/
│   │   ├── dashboard/          # Dashboard-specific components
│   │   │   ├── DashboardCanvas.tsx
│   │   │   ├── WidgetContainer.tsx
│   │   │   └── WidgetToolbar.tsx
│   │   ├── widgets/            # Visualization widgets
│   │   │   ├── MetricCard.tsx
│   │   │   ├── LineChartWidget.tsx
│   │   │   ├── ScatterPlotWidget.tsx
│   │   │   └── PieChartWidget.tsx
│   │   ├── filters/            # Filter components
│   │   │   ├── GlobalDateFilter.tsx
│   │   │   └── SensorSelector.tsx
│   │   └── ui/                 # Shared UI components
│   ├── hooks/                  # Custom React hooks
│   ├── lib/                    # Utilities and helpers
│   │   ├── mockData.ts         # Mock data generator
│   │   └── types.ts            # TypeScript type definitions
│   └── styles/                 # Global styles (if needed)
├── public/
├── package.json
├── tsconfig.json
├── next.config.js
└── README.md
```

### 6. Documentation

Provide comprehensive documentation:

- **Project README.md** must include:
  - Project overview and objectives
  - Prerequisites (Node.js version, etc.)
  - Installation instructions
  - How to run the application
  - Available scripts
  - Design decisions and trade-offs

- **Component Documentation**:
  - Props interfaces for all components
  - Usage examples in code comments

### 7. Testing (Optional but Recommended)

If time permits, add basic tests:

- **Component tests** using React Testing Library
- **Utility function tests** using Jest
- Focus on critical user interactions

### 8. Version Control Best Practices

Demonstrate professional Git workflow:

- **Repository Setup**:
  - Fork the `intella-hiring-challenges` repository
  - Work within your forked repository
  - Commit frequently with meaningful messages

- **Commit Strategy** (recommended):
  - `feat: add dashboard canvas with grid layout`
  - `feat: implement line chart widget`
  - `refactor: extract date filter to shared component`
  - `style: improve widget card styling`
  - `fix: correct date range filter behavior`

## Bonus Requirements (Optional)

Pick any of these to showcase additional skills:

- [ ] **Login Page**: Simple authentication UI
  - Email/password form with validation
  - Mock authentication (no backend required)
  - Protected route for dashboard

- [ ] **Threshold Visualization**: Display thresholds on charts
  - Toggle to show/hide threshold lines
  - Visual indicators when values exceed thresholds
  - Configurable threshold values per sensor type

- [ ] **Additional Chart Types**: Extend visualization options
  - Area chart for cumulative values
  - Bar chart for comparisons
  - Gauge/Speedometer for current values
  - Heatmap for correlation analysis

- [ ] **Widget Persistence**: Save dashboard configuration
  - LocalStorage for layout persistence
  - Export/import dashboard configuration

- [ ] **Dark Mode**: Theme switching capability
  - Mantine's built-in color scheme support
  - Charts that adapt to theme

- [ ] **Real-time Simulation**: Live data updates
  - WebSocket simulation or polling
  - Animated chart transitions

- [ ] **Dashboard Templates**: Pre-configured layouts
  - "Power System Overview" template
  - "Thermal Monitoring" template

- [ ] **Drag & Drop**: Advanced widget positioning
  - React DnD or similar library
  - Smooth animations

## Evaluation Criteria

Your submission will be evaluated across multiple dimensions:

| Area | What We Look For | Weight |
|------|------------------|--------|
| **UI/UX Design** | Clean, intuitive interface, good visual hierarchy, consistent styling | ⭐⭐⭐⭐⭐ |
| **Component Architecture** | Reusable, composable components, proper prop drilling, state management | ⭐⭐⭐⭐⭐ |
| **TypeScript Usage** | Proper types, interfaces, generics, type safety | ⭐⭐⭐⭐⭐ |
| **Code Quality** | Readability, consistency, React best practices | ⭐⭐⭐⭐⭐ |
| **Data Visualization** | Effective use of charts, proper axis labels, legends, tooltips | ⭐⭐⭐⭐ |
| **Responsiveness** | Adaptive layouts, flexible widgets | ⭐⭐⭐ |
| **Documentation** | Clear README, code comments | ⭐⭐⭐ |
| **Creativity** | Unique design choices, thoughtful UX improvements | ⭐⭐⭐ |
| **Git Workflow** | Commit history that shows iterative development | ⭐⭐ |

### Key Evaluation Questions

We'll be asking ourselves:

1. **Is the dashboard intuitive?** Can we understand it without instructions?
2. **Do the visualizations work?** Charts render correctly with proper labels
3. **Is the code maintainable?** Could another engineer extend this easily?
4. **Are components reusable?** Good abstraction and composition
5. **Is TypeScript used effectively?** Not just `any` everywhere
6. **Did they make good trade-offs?** Balance between features and polish
7. **Is the UI polished?** Attention to detail, consistent spacing, colors

## Time Expectation

**Estimated time**: Maximum 8 hours

**Our advice**: Focus on **quality over quantity**. A smaller, polished dashboard is significantly better than a feature-complete but buggy one.

### Suggested Breakdown

| Hours | Focus Area |
|-------|------------|
| **1-2** | Project setup, layout structure, Mantine configuration |
| **2-3** | Mock data generator, basic widget components |
| **3-4** | Chart widgets (Line, Scatter, Pie) with proper styling |
| **5-6** | Dashboard canvas, widget management, date filtering |
| **7** | Sensor selection, per-widget configuration |
| **8** | Polish, documentation, final testing |

## Expected Deliverables

### 1. Working Application

- Next.js app that starts without errors
- Dashboard canvas with at least 4 widget types
- Functional date filtering (global and per-widget)
- Sensor type selection for widgets

### 2. Source Code

- Well-organized project structure
- TypeScript with proper type definitions
- Reusable component architecture
- Clean, readable code

### 3. Documentation

- **README.md** with:
  - Project description
  - Setup instructions
  - Available scripts
  - Design decisions
- Component prop documentation

### 4. Git History

- Meaningful commit messages
- Logical progression of features

## Technical Setup

### Prerequisites

- Node.js 18+ (LTS recommended)
- npm, yarn, or pnpm

### Quick Start

```bash
# Clone your forked repository
git clone https://github.com/YOUR_USERNAME/intella-hiring-challenges.git
cd intella-hiring-challenges/frontend

# Install dependencies
npm install

# Start development server
npm run dev

# Open http://localhost:3000
```

### Recommended Development Tools

- **VS Code** with extensions:
  - ESLint
  - Prettier
  - TypeScript Vue Plugin (for better TS support)
  - Mantine UI snippets (if available)

## Tips for Success

- **Start with layout**: Get the AppShell and grid working first
- **One widget at a time**: Perfect one chart type before moving to others
- **Use Mantine docs**: They have excellent examples and recipes
- **Mock data early**: Generate realistic data before building charts
- **Test interactions**: Make sure filters actually update charts
- **Polish matters**: Consistent spacing, colors, and typography
- **Commit often**: Don't wait until the end

## FAQ

**Q: Which charting library should I use?**  
A: Recharts integrates well with React/Mantine. Chart.js with react-chartjs-2 is also great. Choose what you're comfortable with.

**Q: How realistic should the mock data be?**  
A: Realistic enough to look convincing. Values should follow logical patterns (temperature doesn't jump 50°C in one second).

**Q: Should I implement actual authentication?**  
A: No backend required. A mock login flow (any email/password works) is sufficient for the bonus.

**Q: Can I use additional libraries?**  
A: Yes, but justify your choices. Don't add libraries for features you don't implement.

**Q: How many widgets should the dashboard support?**  
A: At least 4-6 widgets simultaneously. Performance with 10+ is a bonus.

**Q: Should widgets be draggable?**  
A: Optional bonus. A simple grid layout that allows adding/removing widgets is sufficient.

**Q: What about mobile responsiveness?**  
A: Desktop-first. Basic tablet support is expected. Full mobile is a bonus.

---

## Final Note

This assessment is designed to showcase your frontend development skills in a practical context. We're looking for engineers who can:

- Build intuitive, visually appealing interfaces
- Write clean, maintainable TypeScript/React code
- Make pragmatic decisions under time constraints
- Create reusable, composable components
- Handle data visualization effectively

**Remember**: We value a polished, working subset of features over a complete but rough implementation.

Good luck! We're excited to see your dashboard. 🛰️📊

