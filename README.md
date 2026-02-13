# Repercussion 
## Intro
**Repercussion** is a high stakes 3D - first person shooting game. The player navigates through zombie-infested levels and collects coins to unlock exit gates to reach to the next level. Players can try to eliminate the zombies with shooting, however, shooting costs their health point. They have to balance between battle and other strategies to keep themselves in the safezone, as blind slaughter and cowardly avoidance will only lead to failure.

## Support Input
The prototype utilizes a standard FPS control scheme to ensure immediate player accessibility:
- WASD: Spatial Navigation
- Spacebar: Jumping
- Mouse Movement: Precision Aiming
- Left Mouse Click: Projectile Discharg

## Twist & Mechanics Matrix

| Mechanic | Description | Interaction with Twist | Affected Genre Elements | Type of Genre Innovation |
| - | - | - | - | - |
| Health Drain Weapon | When the player fires a shot, their health drains by a set amount. This continues for every shot. | The core twist that transforms shooting from a risk-free offensive action to a strategy based action. | Shooting Mechanics; Health Management system | Core Mechanic Innovation |
| Coin Collection Gating | Players must collect a target number of coins scattered throughout levels, to unlock the exit gate and progress to the next level. | Forces players to explore areas strategically to avoid contact with zombies and collect enough coins to unlock gates. | Resource Collections; Level based Progression | Strategic Twist |



## Update Logs
**Feb.12.2026 Initial Prototype**
- Prototype weapon with shooting function
  - Player's forward direction of movement is binded to shooting direction now
- Variables Blackboard based on Scriptable Object
  - **Problem**: Unity prefabs cannot hold references to scene objects — those references break when loaded in a different scene. For example, if member A builds a HUD prefab that reads `PlayerHP` from a scene object, member B opening a different scene will see a missing reference and has to manually re-link it.
  - **Solution**: Store shared runtime data (HP, speed, coins, etc.) in ScriptableObject assets that live in the **Project** folder, not in any scene. Every prefab references the same asset file, so references never break regardless of which scene is open or who opens it.
- Player Attributes based on Variables Blackboard
- Simple UI to show player HP and aim point
- Simple Prototype Scene
- Simple Monster
  - Randomly choosing moving around or chasing player, based on AI Nav Mesh 
  - Can be killed by player's weapon
  - Can hit player with on trigger detection
- Simple Coin & Escape Point
  - Player have to collect enough coin to escape from the scene
  
**Feb.06.2026 Initial Commit**
- Event Publisher
  - ScriptableObject-based type-safe publish/subscribe event system
  - Generic subscribe, unsubscribe, and publish with automatic caller source tracking
  - Built-in null reference detection, automatically skips callbacks from destroyed objects
  - Predefined input events (movement, jump, look, fire, dash, aim) and player state events (speed, orientation, animation state)
- Debugger Printer
  - ScriptableObject-based custom logging utility with Log / Warning / Error levels
  - Auto-attaches file path, method name, and line number context with color-coded output
  - Configurable block list for per-module log suppression, modifiable at runtime
- Basic Free Look Camera Implement with Cinemachine
  - Real-time camera following via tracking point, mouse input for look rotation with configurable sensitivity
  - Right-click aim mode automatically aligns character orientation to camera direction
- MVC Framework for Main Player Character
  - **Model**: Stores player state data (speed, orientation, ground detection, etc.) and broadcasts changes via the event system
  - **View**: Listens to player state events, responsible for world-space movement and smooth rotation
  - **Controller**: Dual-layer state machine managing Lower Body (Idle / Move / Jump / Fall) and Upper Body (Idle / HipFire) states with full enter/update/exit lifecycle
- Basic Movement, Jumping, Rotation Control
  - New Input System based input management supporting WASD movement, Space jump, fire, aim
  - Camera-relative movement direction with smooth acceleration and deceleration
  - Jump system with per-frame gravity simulation and sphere-cast ground detection
  - Character rotates toward movement direction (or camera direction when aiming) with angular speed limiting for smooth turning