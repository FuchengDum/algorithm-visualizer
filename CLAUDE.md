# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is Algorithm Mentor, an enhanced algorithm visualization tool based on Algorithm Visualizer. The project combines Algorithm Visualizer's core functionality with an intelligent tutoring system to help beginners learn algorithms more effectively through guided explanations and interactive visualizations.

## Architecture

### Core Components Structure

The project is based on Algorithm Visualizer's architecture with the following key components:

#### Tracer System (`src/core/tracers/`)
- **Base class**: `Tracer.jsx` - Base tracer class that all visualization tracers extend
- **Array tracers**: `Array1DTracer.js`, `Array2DTracer.js` - For 1D and 2D array visualizations
- **Graph tracer**: `GraphTracer.js` - For graph algorithm visualizations
- **Specialized tracers**: `LogTracer.js`, `ChartTracer.js`, `ScatterTracer.js` - For different visualization types

#### Renderer System (`src/core/renderers/`)
- **Base renderer**: `Renderer/index.js` - Core rendering logic
- **Specialized renderers**: `Array1DRenderer`, `Array2DRenderer`, `GraphRenderer`, etc.
- Each renderer handles the visual representation of its corresponding tracer data

#### UI Components (`src/components/`)
- **Player**: `Player/index.js` - Main animation playback controller with play/pause/step controls
- **CodeEditor**: `CodeEditor/index.js` - Code editing interface using react-ace
- **VisualizationViewer**: Main visualization display component
- **BaseComponent**: Shared component base class

#### State Management (`src/reducers/`)
- Redux-based state management with reducers for:
  - `current.js` - Current file/algorithm being edited
  - `player.js` - Player state (playback position, speed, etc.)
  - `directory.js` - Algorithm directory structure

### Algorithm Execution Flow

1. **Code Input**: User writes algorithm code in the CodeEditor component
2. **Build Process**: Player component builds the code using TracerApi
3. **Command Generation**: Tracers generate visualization commands during algorithm execution
4. **Chunking**: Commands are grouped into chunks based on line numbers
5. **Playback**: Player steps through chunks, triggering renderer updates
6. **Visualization**: Renderers display the algorithm state at each step

## Development Commands

### Basic Development
```bash
# Start development server
npm start

# Build for production
npm run build

# Run tests
npm run test
```

### Development Workflow
```bash
# The project uses react-scripts (Create React App) for development
# Development server runs on port 3000 by default
# Backend API proxy configured for localhost:8080 (see package.json)
```

## Key Technical Details

### Supported Languages
- JavaScript (.js)
- C++ (.cpp)
- Java (.java)

### Visualization Types
- **Array1D**: Linear array visualizations with element highlighting
- **Array2D**: Matrix/grid visualizations
- **Graph**: Node-edge graph visualizations
- **Log**: Text logging output
- **Chart**: Data charting with Chart.js integration

### State Management Pattern
The project uses Redux with the following key actions:
- Algorithm building and execution
- Playback control (play/pause/step/speed)
- File/directory navigation
- Line indicator synchronization between code and visualization

### Styling
- Uses SCSS modules for component-scoped styling
- Centralized theming in `src/common/stylesheet/`
- CSS class naming follows BEM methodology

## Algorithm Tutor Integration

When extending with Algorithm Tutor features:

1. **Tracer Enhancement**: Extend existing tracers to capture learning-focused metadata
2. **Tutorial Components**: Add tutor UI components alongside existing Player controls
3. **Hint System**: Implement hint generation alongside command generation in tracer system
4. **State Extensions**: Add tutor-specific state to Redux store

The modular architecture allows for gradual enhancement of the existing visualization system without breaking core functionality.