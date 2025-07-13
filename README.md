# 🎓 Dynamic Exam Invigilation Planner

A sophisticated web application for scheduling exam invigilators using advanced graph coloring algorithms. Built with React/TypeScript frontend and high-performance C++ backend API.

## ✨ Features

### 🧠 Advanced Graph Coloring Algorithms
- **Welsh-Powell Algorithm**: Optimized for degree-based vertex ordering
- **Greedy Algorithm**: Simple but effective sequential coloring
- **DSATUR Algorithm**: Degree of Saturation for optimal coloring
- **Real-time Algorithm Comparison**: Compare performance and efficiency

### 🎯 Realistic Scheduling Logic
- **Conflict Detection**: Time overlap detection with 30-minute buffer
- **Invigilator Availability**: Respects unavailable dates and time slots
- **Workload Balancing**: Distributes assignments fairly among invigilators
- **Department Preferences**: Matches invigilators to preferred departments
- **Venue Constraints**: Considers venue conflicts and requirements

### 🚀 Dynamic Features
- **Real-time Updates**: Live conflict detection and statistics
- **Auto-generation**: Automatic schedule generation when data changes
- **Data Persistence**: localStorage for session continuity
- **Export Functionality**: JSON export for schedules and comparisons
- **Validation System**: Schedule feasibility checking

### 🎨 Modern UI/UX
- **Glass Morphism Design**: Beautiful, modern interface
- **Responsive Layout**: Works on desktop and mobile
- **Interactive Visualizations**: Graph visualization with D3.js
- **Status Indicators**: Real-time API status and loading states
- **Toast Notifications**: User feedback and error handling

## 🏗️ Architecture

### Frontend (React/TypeScript)
```
src/
├── components/          # React components
│   ├── ExamForm.tsx    # Exam creation/editing
│   ├── InvigilatorForm.tsx # Invigilator management
│   ├── ScheduleDisplay.tsx # Schedule visualization
│   ├── GraphVisualization.tsx # D3.js graph
│   └── ...
├── utils/
│   ├── graphColoring.ts # JavaScript algorithm fallback
│   └── apiService.ts   # C++ API communication
├── types/
│   └── scheduling.ts   # TypeScript type definitions
└── App.tsx             # Main application
```

### Backend (C++ with Crow Framework)
```
backend/
├── src/
│   ├── main.cpp        # HTTP server and endpoints
│   └── graph_coloring.cpp # Core algorithms
├── include/
│   └── graph_coloring.hpp # Header definitions
└── CMakeLists.txt      # Build configuration
```

## 🚀 Quick Start

### Prerequisites
- Node.js 16+ and npm
- C++17 compatible compiler (GCC 7+, Clang 5+, MSVC 2017+)
- CMake 3.15+

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd exam-invigilation-planner
   ```

2. **Install frontend dependencies**
   ```bash
   npm install
   ```

3. **Build the C++ backend**
   ```bash
   # Linux/macOS
   cd backend
   mkdir build && cd build
   cmake ..
   make -j4
   
   # Windows
   cd backend
   mkdir build && cd build
   cmake .. -G "Visual Studio 16 2019"
   cmake --build . --config Release
   ```

4. **Start the backend server**
   ```bash
   # Linux/macOS
   ./exam_scheduler_api
   
   # Windows
   exam_scheduler_api.exe
   ```

5. **Start the frontend development server**
   ```bash
   npm start
   ```

6. **Open your browser**
   Navigate to `http://localhost:3000`

## 📊 Algorithm Details

### Welsh-Powell Algorithm
- **Principle**: Sort vertices by degree in descending order
- **Advantage**: Often produces optimal or near-optimal coloring
- **Time Complexity**: O(V² + E)
- **Best for**: Dense graphs with high conflict rates

### Greedy Algorithm
- **Principle**: Color vertices in arbitrary order
- **Advantage**: Simple and fast implementation
- **Time Complexity**: O(V + E)
- **Best for**: Sparse graphs and quick solutions

### DSATUR Algorithm
- **Principle**: Choose vertex with maximum saturation degree
- **Advantage**: Generally produces optimal coloring
- **Time Complexity**: O(V²)
- **Best for**: Complex graphs requiring optimal solutions

## 🔧 API Endpoints

### Health Check
```http
GET /api/health
```
Returns server status and available algorithms.

### Generate Schedule
```http
POST /api/schedule
Content-Type: application/json

{
  "exams": [...],
  "invigilators": [...],
  "algorithm": "welsh-powell"
}
```

### Compare Algorithms
```http
POST /api/compare
Content-Type: application/json

{
  "exams": [...],
  "invigilators": [...]
}
```

### Get Statistics
```http
POST /api/stats
Content-Type: application/json

{
  "exams": [...],
  "invigilators": [...]
}
```

### Sample Data
```http
GET /api/sample-data
```
Returns realistic sample exams and invigilators.

### Graph Data
```http
POST /api/graph
Content-Type: application/json

{
  "exams": [...],
  "invigilators": [...]
}
```

## 📝 Usage Guide

### 1. Setup Phase
- **Load Sample Data**: Click "Load Sample Data" to get started quickly
- **Add Exams**: Create exams with realistic constraints (time, venue, students)
- **Add Invigilators**: Define invigilators with availability and preferences

### 2. Scheduling Phase
- **Select Algorithm**: Choose from Welsh-Powell, Greedy, or DSATUR
- **Generate Schedule**: Click "Generate Schedule" for single algorithm
- **Compare Algorithms**: Click "Compare Algorithms" for all three
- **Validate Schedule**: Check for conflicts and feasibility issues

### 3. Analysis Phase
- **View Statistics**: Monitor graph density, conflicts, and invigilator shortage
- **Export Results**: Download schedules and comparisons as JSON
- **Visualize Graph**: See the conflict graph with D3.js visualization

## 🎯 Realistic Constraints

### Exam Constraints
- **Time Overlap**: 30-minute buffer between exams
- **Venue Conflicts**: Same venue cannot host overlapping exams
- **Student Count**: Affects invigilator requirements
- **Department**: Influences invigilator preferences

### Invigilator Constraints
- **Daily Hours**: Maximum hours per day (typically 6-8 hours)
- **Unavailable Dates**: Specific dates when unavailable
- **Time Slots**: Specific time periods when unavailable
- **Department Preferences**: Preferred subject areas
- **Workload Balance**: Fair distribution of assignments

## 🔍 Conflict Detection

The system detects conflicts based on:
1. **Temporal Conflicts**: Overlapping exam times on same date
2. **Spatial Conflicts**: Same venue used simultaneously
3. **Resource Conflicts**: Insufficient invigilators available
4. **Preference Conflicts**: Invigilator department mismatches

## 📈 Performance Metrics

### Algorithm Comparison
- **Colors Used**: Number of time slots required
- **Execution Time**: Algorithm performance in milliseconds
- **Assignment Quality**: Distribution fairness and preferences
- **Conflict Resolution**: Effectiveness in avoiding conflicts

### System Statistics
- **Graph Density**: Ratio of edges to maximum possible edges
- **Conflict Percentage**: Percentage of exams with conflicts
- **Invigilator Utilization**: Efficiency of resource usage
- **Schedule Feasibility**: Whether all constraints are satisfied

## 🛠️ Development

### Frontend Development
```bash
# Start development server
npm start

# Run tests
npm test

# Build for production
npm run build
```

### Backend Development
```bash
# Build with debug symbols
cd backend/build
cmake .. -DCMAKE_BUILD_TYPE=Debug
make

# Run with logging
./exam_scheduler_api --verbose
```

### Code Structure
- **TypeScript**: Strict typing for all data structures
- **React Hooks**: Modern state management with useEffect and useState
- **C++17**: Modern C++ features for performance
- **Crow Framework**: Lightweight HTTP server
- **nlohmann/json**: JSON parsing and serialization

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Graph Coloring Algorithms**: Based on classical computer science algorithms
- **Crow Framework**: Lightweight C++ web framework
- **D3.js**: Data visualization library
- **React**: Frontend framework
- **TypeScript**: Type-safe JavaScript

## 📞 Support

For questions, issues, or contributions:
- Create an issue on GitHub
- Contact the development team
- Check the documentation

---

**Built with ❤️ for educational institutions and exam scheduling efficiency** 