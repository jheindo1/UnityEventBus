# UnityEventBus
 An Event Bus system for Unity based on the [EventBus repo by Adam Mhyre](https://github.com/adammyhre/Unity-Event-Bus). 
 This EventBus system provides a way to create decoupled architectures in Unity projects. It allows communication between different parts of an application without requiring direct references.

# Example Usage
The usage generally works like:

```C#
using Josh.EventBus;

public struct PlayerEvent : IEvent {
    public int health;
    public int mana;
}

EventBinding<PlayerEvent> playerEventBinding;

void OnEnable() {    
    playerEventBinding = new EventBinding<PlayerEvent>(HandlePlayerEvent);
    EventBus<PlayerEvent>.Register(playerEventBinding);

    // Can Add or Remove Actions to/from the EventBinding
}

void OnDisable() {
    EventBus<PlayerEvent>.Deregister(playerEventBinding);
}

void Start() {
    EventBus<PlayerEvent>.Raise(new PlayerEvent {
        health = healthComponent.GetHealth(),
        mana = manaComponent.GetMana()
    });    
}

void HandlePlayerEvent(PlayerEvent playerEvent) {
    Debug.Log($"Player event received! Health: {playerEvent.health}, Mana: {playerEvent.mana}");
}
```
# Installation and Setup
I changed the original project structure to be compatible with Unitys package manager.
To install open the package manager *(Window > Package Manager)* and then install from git *(+ Icon on the top left > Install package from git URL...)*
