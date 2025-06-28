# Life.js - Artificial Life Simulation

A JavaScript port of [Scriptbots](https://sites.google.com/site/scriptbotsevo/), featuring evolving neural network agents in a dynamic ecosystem. Watch as artificial organisms compete, reproduce, and evolve complex behaviors through natural selection.

![Life.js Simulation](https://img.shields.io/badge/Status-Active-green.svg)
![JavaScript](https://img.shields.io/badge/Language-JavaScript-yellow.svg)
![License](https://img.shields.io/badge/License-Open_Source-blue.svg)

## 🌟 Features

- **Artificial Life Simulation**: Watch autonomous agents evolve and adapt
- **Neural Network Brains**: Each agent has an evolving neural network
- **Dynamic Ecosystem**: Herbivores, carnivores, and vegetation interact
- **Real-time Evolution**: Observe natural selection in action
- **Interactive Controls**: Pause, clone, kill agents, and adjust parameters
- **Visual Analytics**: Population charts and brain visualization
- **Web-based**: Runs in any modern browser

## 🏗️ Architecture Overview

```mermaid
graph TB
    A[HTML Interface] --> B[Life.UI]
    B --> C[Life.Simulation]
    C --> D[Web Worker]
    D --> E[Life.World]
    E --> F[Life.Agent Array]
    F --> G[Life.Brain]
    C --> H[Life.Renderer]
    H --> I[HTML5 Canvas]
    
    J[Bootstrap UI] --> B
    K[HighCharts] --> B
    L[JIT Visualization] --> B
    
    style C fill:#e1f5fe
    style E fill:#f3e5f5
    style G fill:#e8f5e8
    style H fill:#fff3e0
```

## 🔄 System Components

### Core Architecture

```mermaid
flowchart LR
    subgraph "Main Thread"
        UI[UI Controls]
        Renderer[Canvas Renderer]
        Charts[Population Charts]
    end
    
    subgraph "Web Worker"
        Simulation[Simulation Engine]
        World[World Grid]
        Agents[Agent Population]
        Physics[Physics Engine]
    end
    
    subgraph "Agent Components"
        Brain[Neural Network]
        Vision[Vision System]
        Movement[Movement]
        Behavior[Behavior Logic]
    end
    
    UI -.->|Commands| Simulation
    Simulation -->|State| Renderer
    Simulation -->|Data| Charts
    World --> Agents
    Agents --> Brain
    Brain --> Vision
    Brain --> Movement
    Brain --> Behavior
```

### Component Details

#### 🧠 Life.Simulation
- **Purpose**: Main simulation controller and interface
- **Responsibilities**: Manages world state, agent lifecycle, parameter configuration
- **Key Methods**: `init()`, `sendCommand()`, `update()`

#### 🌍 Life.World  
- **Purpose**: Simulation environment and physics
- **Features**: Toroidal grid system, food distribution, collision detection
- **Data**: Agent positions, food cells, environmental parameters

#### 🤖 Life.Agent
- **Purpose**: Individual organisms with neural network brains
- **Capabilities**: Vision, movement, eating, reproduction, combat
- **Evolution**: Genetic mutation of neural network weights

#### 🎨 Life.Renderer
- **Purpose**: Visual representation of the simulation
- **Features**: Real-time canvas rendering, agent visualization, environmental display
- **Performance**: Optimized for smooth 60fps rendering

#### 🎛️ Life.UI
- **Purpose**: User interface and interaction controls
- **Features**: Parameter adjustment, agent inspection, data visualization
- **Integration**: Bootstrap components, charts, brain graphs

## 🧬 Agent Neural Network Architecture

```mermaid
graph LR
    subgraph "Input Layer"
        I1[Vision Input 1]
        I2[Vision Input 2]
        I3[Vision Input 3]
        I4[Vision Input 4]
        I5[Health Status]
        I6[Age]
        I7[Random Input]
    end
    
    subgraph "Hidden Layer"
        H1[Hidden Node 1]
        H2[Hidden Node 2]
        H3[Hidden Node 3]
        H4[Hidden Node 4]
        H5[Hidden Node 5]
    end
    
    subgraph "Output Layer"
        O1[Move Forward]
        O2[Turn Left]
        O3[Turn Right]
        O4[Eat/Attack]
        O5[Give Food]
        O6[Spike Extend]
    end
    
    I1 --> H1
    I1 --> H2
    I2 --> H2
    I2 --> H3
    I3 --> H3
    I3 --> H4
    I4 --> H4
    I4 --> H5
    I5 --> H1
    I5 --> H5
    I6 --> H2
    I6 --> H4
    I7 --> H3
    
    H1 --> O1
    H1 --> O2
    H2 --> O2
    H2 --> O3
    H3 --> O3
    H3 --> O4
    H4 --> O4
    H4 --> O5
    H5 --> O5
    H5 --> O6
    
    style I1 fill:#e3f2fd
    style I2 fill:#e3f2fd
    style I3 fill:#e3f2fd
    style I4 fill:#e3f2fd
    style H1 fill:#f3e5f5
    style H2 fill:#f3e5f5
    style H3 fill:#f3e5f5
    style H4 fill:#f3e5f5
    style H5 fill:#f3e5f5
    style O1 fill:#e8f5e8
    style O2 fill:#e8f5e8
    style O3 fill:#e8f5e8
    style O4 fill:#e8f5e8
    style O5 fill:#e8f5e8
    style O6 fill:#e8f5e8
```

## 🔄 Simulation Lifecycle

```mermaid
sequenceDiagram
    participant UI as User Interface
    participant Sim as Simulation
    participant World as World
    participant Agent as Agents
    participant Brain as Neural Networks
    
    UI->>Sim: Initialize
    Sim->>World: Create world grid
    Sim->>Agent: Spawn initial population
    Agent->>Brain: Initialize neural networks
    
    loop Every Tick
        World->>World: Add food randomly
        World->>Agent: Set vision inputs
        Agent->>Brain: Process inputs
        Brain->>Agent: Generate outputs
        Agent->>World: Execute actions
        World->>Agent: Handle collisions
        Agent->>Agent: Age and health updates
        Agent->>World: Reproduction/death
        World->>Sim: Update complete
        Sim->>UI: Send state data
        UI->>UI: Update visualizations
    end
```

## 🚀 Quick Start

### Installation

1. Clone the repository:
```bash
git clone https://github.com/HyperCogWizard/lifejs.git
cd lifejs
```

2. Serve the files (required for Web Workers):
```bash
# Using Python
python3 -m http.server 8000

# Using Node.js (if you have http-server)
npx http-server

# Or any other static file server
```

3. Open your browser to `http://localhost:8000`

### Basic Setup

```html
<!DOCTYPE HTML>
<html>
<head>
    <title>Life.js Simulation</title>
    <script type="text/javascript" src="Life.js"></script>
</head>
<body>
    <script type="text/javascript">
        var view = new Life.Renderer();
        view.init();
        document.body.appendChild(view.canvas);
    </script>
</body>
</html>
```

### Advanced Setup with UI

```html
<!DOCTYPE html>
<html>
<head>
    <script src="Life.js"></script>
    <script src="LifeUI.js"></script>
</head>
<body>
    <div id="simulation"></div>
    <script>
        var parameters = {
            width: 800,
            height: 600,
            maxAgents: 50,
            tickDuration: 20
        };
        
        var simulation = new Life.Simulation(parameters);
        var renderer = new Life.Renderer(simulation);
        var ui = new Life.UI(simulation);
        
        simulation.init();
        renderer.init();
        
        document.getElementById('simulation').appendChild(renderer.canvas);
    </script>
</body>
</html>
```

## ⚙️ Configuration

### Simulation Parameters

```javascript
var parameters = {
    // Timing
    tickDuration: 20,           // Milliseconds between updates
    
    // World
    width: 1200,                // World width in pixels
    height: 800,                // World height in pixels
    cellSize: 64,               // Food cell size
    
    // Population
    minAgents: 25,              // Minimum agent population
    maxAgents: 50,              // Maximum agent population
    
    // Environment
    maxFood: 0.5,               // Maximum food per cell
    foodAddFrequency: 30,       // Ticks between food spawning
    
    // Agent properties
    agent: {
        radius: 10,             // Agent size
        speed: 0.3,             // Base movement speed
        viewDistance: 150,      // Vision range
        numberEyes: 4,          // Number of vision inputs
        babies: 2,              // Offspring count
        mutationRate: [0.002, 0.05]  // Neural network mutation
    }
};
```

### Agent Behavior Tuning

```javascript
agent: {
    // Movement
    speed: 0.3,
    sprintMultiplier: 2,
    
    // Vision system
    numberEyes: 4,
    viewDistance: 150,
    
    // Combat
    spikeStrength: 1,
    spikeSpeed: 0.005,
    
    // Metabolism
    foodIntake: 0.002,
    foodWasted: 0.001,
    foodTraded: 0.001,
    
    // Evolution
    reproductionRate: {
        carnivore: 7,
        herbivore: 7
    },
    mutationRate: [0.002, 0.05]
}
```

## 📊 Data Flow

```mermaid
flowchart TD
    A[User Input] --> B[UI Controls]
    B --> C[Simulation Commands]
    C --> D[Web Worker]
    
    D --> E[World Update]
    E --> F[Agent Processing]
    F --> G[Neural Network Computation]
    G --> H[Behavior Output]
    H --> I[Physics Simulation]
    I --> J[Population Dynamics]
    
    J --> K[State Data]
    K --> L[Main Thread]
    L --> M[Canvas Rendering]
    L --> N[Chart Updates]
    L --> O[UI Feedback]
    
    style A fill:#e1f5fe
    style D fill:#f3e5f5
    style G fill:#e8f5e8
    style M fill:#fff3e0
```

## 🎮 Interactive Controls

- **Pause/Resume**: Stop or continue the simulation
- **Clone Agent**: Duplicate the selected agent
- **Kill Agent**: Remove the selected agent
- **Advanced Controls**: Access detailed parameter tuning
- **Render Options**: Toggle visual elements (grass, health bars, vision cones)
- **Brain Visualization**: View neural network structure
- **Population Charts**: Track species over time

## 🧪 API Reference

### Life.Simulation

```javascript
// Constructor
var simulation = new Life.Simulation(parameters);

// Methods
simulation.init()                    // Initialize simulation
simulation.sendCommand(cmd, options) // Send control command
simulation.close()                   // Cleanup resources
```

### Life.Renderer

```javascript
// Constructor  
var renderer = new Life.Renderer(simulation, parameters);

// Methods
renderer.init()                      // Setup canvas
renderer.update()                    // Render frame
renderer.setRenderOptions(options)   // Configure display
```

### Life.Agent

```javascript
// Properties
agent.x, agent.y                    // Position
agent.health                        // Current health
agent.age                           // Agent age
agent.species                       // Herbivore/Carnivore
agent.brain                         // Neural network

// Methods
agent.update(world)                  // Process one tick
agent.reproduce(partner)             // Create offspring
agent.mutate()                       // Apply genetic mutations
```

## 🔬 Technical Details

### Neural Network Evolution

Each agent possesses a feed-forward neural network that controls its behavior. The network evolves through:

1. **Genetic Inheritance**: Offspring inherit parent neural networks
2. **Mutation**: Random weight modifications during reproduction  
3. **Selection Pressure**: Successful agents reproduce more frequently
4. **Crossover**: Future enhancement for genetic diversity

### Physics Engine

- **Collision Detection**: Spatial partitioning for performance
- **Toroidal World**: Wrap-around boundaries
- **Vision System**: Ray-casting for environmental perception
- **Movement**: Velocity-based with momentum

### Performance Optimizations

- **Web Workers**: Offload simulation to background thread
- **Spatial Partitioning**: Efficient collision detection
- **Culling**: Render only visible elements
- **Batch Processing**: Group similar operations

## 🎯 Use Cases

- **Educational**: Demonstrate evolutionary principles
- **Research**: Study emergent behaviors and evolution
- **Entertainment**: Watch artificial life unfold
- **Development**: Base for more complex simulations

## 🛠️ Troubleshooting

### Common Issues

**Simulation not starting:**
- Ensure you're serving files via HTTP/HTTPS (not file://)
- Check browser console for Web Worker errors
- Verify all JavaScript files are loading correctly

**Poor performance:**
- Reduce `maxAgents` parameter
- Increase `tickDuration` for slower updates
- Disable visual elements like grass rendering

**Neural network visualization not showing:**
- Click "Update Brain Graph" button
- Select an agent by clicking on it
- Switch to the "Selected Agent" tab

### Browser Compatibility

- **Modern browsers**: Chrome 80+, Firefox 75+, Safari 14+, Edge 80+
- **Required features**: HTML5 Canvas, Web Workers, ES5+
- **Recommended**: Hardware acceleration enabled

## 🎯 Use Cases

- **Educational**: Demonstrate evolutionary principles
- **Research**: Study emergent behaviors and evolution
- **Entertainment**: Watch artificial life unfold
- **Development**: Base for more complex simulations

## 🔗 Links

- **Original Scriptbots**: https://sites.google.com/site/scriptbotsevo/
- **Default Parameters**: https://github.com/JimAllanson/lifejs/wiki/Default-Parameters
- **Live Demo**: http://jimallanson.github.com/lifejs/

## 📄 License

Open source - see individual file headers for specific licensing information.

---

*Life.js brings the fascinating world of artificial life to your browser. Watch evolution in action!*
