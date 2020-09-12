# Bevy Input Mapper
Input Mapper decouples gameplay code from device specific input api. By converting user inputs from different input hardware into game specific actions, eg. *keyboard "Space" or joystick "A" can be mapped to "Jump" Action*. This improves the overall code quality, by keeping the gameplay code separate from input code.

## Usage

*Add to Cargo.toml dependencies*
```
[dependencies]
bevy_prototype_input_map = "0.1.1"
```

*In code*
```rust
fn main() {
    App::build()
        ...
        .add_plugin(InputMapPlugin::default())
        .add_startup_system(setup.system())
        .add_system(system.system())
        .run();
}

fn setup(
    mut key_map: ResMut<KeyboardMap>
) {

    key_map.bind_keyboard_pressed(KeyCode::Space, "JUMP".to_string());
}

fn system(input_map: Res<InputMap>) {
    if input_map.is_action_in_progress("JUMP".to_string()) {
        println!("Jumping...");
    }
```

*Check out [example/input_map.rs](https://github.com/PradeepKumarRajamanickam/bevy_input_map/blob/master/example/input_map.rs)*

## Example
Use command
> cargo run --example input_map

## Features
- new* Support to set custom strength curve function
- Keyboard Key Mapping
- Mouse Button Mapping
- Mouse Move Mapping
- Action Strength
- Action Deadzone

## Planned
Joystick Mapping
> Depends on bevy input support for joystick

RON based binding config file
>Allow bindings to be loaded from a ron string/file

Context based binding switch
>Allow multiple binding sets to be defined in the ron config. That can be swapped out based on the context, eg.
"E" can be mapped to "use" action in game view but
can be remapped to "equip" action in game inventory ui as shortcut...etc. Based on the view context the bindings will be swapped.

# Release Notes

## v0.1.1 (7 Sept, 2020)
- minor* Readme changes
  - Had to bump the version to publish some readme changes

## v0.1.0 (7 Sept, 2020)
- Keyboard Key Mapping
  - Key press can now be binded to action
- Mouse Button Mapping
  - Mouse button press can now be binded to action
- Mouse Move Mapping
  - Mouse move event can now be mapped to action
- Action Strength
  - Can now query strength of an action. 
  - It will be in range of 0.0 - 1.0
  - Useful for analog inputs like joystick
- Action Deadzone
  - For analog inputs sometimes it is meaningful to have a min threshold to avoid small input noise and to reduce sensitivity

## Author
PradeepKumar Rajamanickam

## Acknowledgments
Inspired by 
- Godot Input Mapper
[https://godotengine.org/article/handling-axis-godot]
- Unreal Action/Axis Mapping
  [https://docs.unrealengine.com/en-US/Gameplay/Input/index.html]
