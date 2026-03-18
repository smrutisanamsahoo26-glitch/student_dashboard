# student_dashboard
# 📚 Student Attendance Viewer

A modern React web application for tracking and visualizing student attendance data with real-time filtering, powerful search capabilities, and interactive charts.

## 🌟 Features

- **30 Student Dataset** - 10 from JSONPlaceholder API + 20 synthetic students
- **Real-time Filtering** - Filter by All/Present/Absent attendance status
- **Smart Search** - Search students by name with instant results
- **Advanced Sorting** - Sort by attendance high-to-low or low-to-high
- **Low Attendance Alert** - Filter students with attendance below 75%
- **Data Visualization** - Three interactive Recharts:
  - Pie chart: Present vs Absent distribution
  - Bar chart: Attendance range distribution (60-69%, 70-79%, 80-89%, 90-100%)
  - Bar chart: Top 5 students by attendance
- **Statistics Dashboard** - Total students, present count, average attendance
- **Student Details Panel** - Click a student to view detailed information
- **CSV Export** - Download attendance reports as CSV file
- **Dark Mode** - Toggle between light and dark themes
- **Loading States** - User-friendly feedback during data loading
- **Error Handling** - Graceful error messages if API fails

## 🛠️ Tech Stack

| Technology              | Purpose                         |
| ----------------------- | ------------------------------- |
| **React 18.2**          | UI framework with Hooks         |
| **Vite 5.0.8**          | Fast bundler & dev server       |
| **Tailwind CSS 3.3**    | Utility-first styling           |
| **Recharts**            | Interactive data visualizations |
| **JSONPlaceholder API** | Mock data source                |

## 📦 Installation

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn

### Setup Steps

```bash
# 1. Navigate to project directory
cd student-attendance-viewer

# 2. Install dependencies
npm install

# 3. Start development server
npm run dev

# 4. Open in browser
# Visit http://localhost:5173
```

## 🚀 Usage

### Development

```bash
npm run dev     # Start dev server with hot reload
npm run build   # Build for production
npm run preview # Preview production build locally
```

### Features Guide

- **Filter Students** - Click All/Present/Absent buttons to filter by attendance status
- **Search** - Type student name in search box for instant filtering
- **Sort** - Toggle between high-to-low or low-to-high attendance
- **View Details** - Click a student row to see detailed information
- **Export Data** - Click "Export CSV" button to download attendance report
- **Dark Mode** - Click 🌙/☀️ button in header to toggle theme

## 📁 Project Structure

```
student-attendance-viewer/
├── src/
│   ├── App.jsx                          # Main component & state management
│   ├── constants.js                     # Configuration constants
│   ├── utils/
│   │   ├── calculations.js              # Data processing & filtering logic
│   │   ├── dataGeneration.js            # API fetch & synthetic data generation
│   │   └── export.js                    # CSV export functionality
│   ├── components/
│   │   ├── StateComponents.jsx          # Loading/Error/Empty state components
│   │   ├── Header.jsx                   # Header & statistics dashboard
│   │   ├── Charts.jsx                   # Pie chart & bar charts
│   │   ├── Filters.jsx                  # Filter buttons & search bar
│   │   ├── StudentTable.jsx             # Student list table
│   │   └── StudentDetails.jsx           # Selected student details panel
│   └── styles/
│       ├── base.css                     # Base Tailwind directives
│       ├── animations.css               # Keyframe animations
│       ├── components.css               # Reusable CSS classes
│       └── index.css                    # CSS import manifest
├── index.html                           # HTML entry point
├── vite.config.js                       # Vite configuration
├── tailwind.config.js                   # Tailwind CSS configuration
├── package.json                         # Project dependencies
└── README.md                            # This file
```

## 🔧 File Responsibilities

### Core Files

**`App.jsx`** - Main orchestrator component

- Manages all application state (students, filters, search, dark mode)
- Fetches student data on component mount
- Applies filtering, sorting, and searching logic
- Passes data and handlers to child components

**`constants.js`** - Configuration management

- `ATTENDANCE_THRESHOLD` - Cutoff for Present/Absent (75%)
- `FIRST_NAMES` & `LAST_NAMES` - Student name generation arrays
- Centralized configuration for easy maintenance

### Utility Files

**`utils/calculations.js`** - Data processing functions

- `statusFromAttendance()` - Convert % to Present/Absent status
- `calculateStats()` - Compute total, present count, average attendance
- `generatePieData()` - Format pie chart data
- `generateAttendanceDistribution()` - Group students by attendance ranges
- `generateTopStudents()` - Extract top 5 students
- `filterStudents()` - Combined filtering & sorting logic

**`utils/dataGeneration.js`** - Data fetching

- `getRandomAttendance()` - Generate random 60-100% attendance
- `fetchStudentsData()` - Main function: fetches 10 from API + generates 20 synthetic students

**`utils/export.js`** - CSV export

- `exportToCSV()` - Convert student data to downloadable CSV file

### Component Files

| Component               | Purpose                                                              |
| ----------------------- | -------------------------------------------------------------------- |
| **StateComponents.jsx** | `LoadingState`, `ErrorState`, `EmptyState` - Feedback components     |
| **Header.jsx**          | `Header` - Title & dark mode toggle; `StatsDashboard` - Stats cards  |
| **Charts.jsx**          | `ChartsSection` - Pie & bar charts; `TopStudentsChart` - Top 5 chart |
| **Filters.jsx**         | `FilterBar` - Filter buttons; `SearchBar` - Search + entry counter   |
| **StudentTable.jsx**    | Display filtered students with attendance data                       |
| **StudentDetails.jsx**  | Show selected student's detailed information                         |

### Style Files

| File               | Purpose                                               |
| ------------------ | ----------------------------------------------------- |
| **base.css**       | Tailwind imports & foundational styles                |
| **animations.css** | Keyframe animations (slideIn, fadeIn, pulse-slow)     |
| **components.css** | Reusable CSS classes (.card, .btn, .badge, .stat-box) |
| **index.css**      | Import manifest for all stylesheets                   |

## 💡 Key React Concepts Used

### useState Hook

Manages component state for students, filters, search, dark mode, etc.

```javascript
const [students, setStudents] = useState([]);
const [filter, setFilter] = useState("All");
```

### useEffect Hook

Performs side effects (API calls) when component mounts.

```javascript
useEffect(() => {
  // Fetch data on mount
  fetchStudentsData();
}, []); // Empty dependency array = run once
```

### useMemo Hook

Memoizes expensive calculations (filtering 30 students) for performance.

```javascript
const filtered = useMemo(
  () =>
    filterStudents(
      students,
      filter,
      showLowAttendance,
      searchQuery,
      sortToggle,
    ),
  [students, filter, showLowAttendance, searchQuery, sortToggle],
);
```

### Props

Pass data from parent (App) to child components (Header, Tables, Charts).

```javascript
<Header darkMode={darkMode} setDarkMode={setDarkMode} />
```

### Controlled Components

Form inputs (search box) controlled by React state for real-time filtering.

```javascript
<input value={searchQuery} onChange={(e) => setSearchQuery(e.target.value)} />
```

### Conditional Rendering

Render different UI based on state (loading, error, or success).

```javascript
{
  loading ? <LoadingState /> : error ? <ErrorState /> : <MainContent />;
}
```

## 📊 Data Flow

```
1. App mounts
   ↓
2. useEffect fetches 30 students
   ↓
3. Students stored in state
   ↓
4. useMemo calculates filtered data & chart data
   ↓
5. Components render with data
   ↓
6. User interacts (filter, search, sort)
   ↓
7. State updates → Components re-render
   ↓
8. useMemo recalculates only if dependencies change
   ↓
9. UI updates instantly with new data
```

## 🎨 Styling Architecture

- **Tailwind CSS** - Utility-first approach for rapid development
- **Custom Animations** - Smooth slideIn, fadeIn, and pulse effects
- **Dark Mode** - Automatic light/dark theme switching
- **Responsive Design** - Mobile, tablet, and desktop layouts
- **Component Classes** - Reusable `.card`, `.btn-primary`, `.badge` classes

## 🔒 Performance Optimizations

- **useMemo** - Prevents unnecessary filtering calculations
- **Module Separation** - Smaller bundle with tree-shaking
- **Component Composition** - Fewer re-renders with focused components
- **Vite Bundling** - Fast development server and optimized production builds

## 🐛 Error Handling

- **API Failures** - Try-catch wraps fetch calls
- **Loading States** - Spinner shown while fetching
- **Empty States** - User-friendly messages when no data available
- **Error Messages** - Display error details if API fails

## 📈 Future Enhancements

- Add attendance history (dates & absence records)
- Implement user authentication
- Add ability to manually update student attendance
- Create attendance trends over time
- Add email notifications for low attendance
- Implement data persistence (database)
- Add role-based access (admin, teacher, student)

## 📝 License

This project is open source and available for educational purposes.

## 👨‍💻 Author

Created as a comprehensive React learning project demonstrating:

- Modern React Hooks patterns
- Component-based architecture
- Data visualization with Recharts
- Tailwind CSS styling
- Responsive design
- State management best practices

## 🤝 Contributing

Feel free to fork this project and submit pull requests for any improvements.

---

**Happy Coding! 🚀**

For questions or issues, feel free to open an issue in the repository.
