Hierarchical State Machine
==========================

### About
This module allows you to create both single-level and hierarchical finite state machines.
State Machines are composed of states, and each state has (optional) callbacks for entering and exiting state. It's also possible to restrict the transition from states using the *from* property.

### Usage
Available states can be set with addState and initial state can be set using initialState setter.

The following example creates a state machine for a player model with 3 states (Playing, paused and stopped)

```javascript
 var playerSM = new StateMachine();

 playerSM.addState("playing",{ enter: this.onPlayingEnter, exit: this.onPlayingExit, from:["paused","stopped"] });
 playerSM.addState("paused",{ enter: this.onPausedEnter, from:"playing"});
 playerSM.addState("stopped",{ enter: this.onStoppedEnter, from:"*"});

 playerSM.on('transition_denied', this.handleTransitionDenied);
 playerSM.on('transition_complete', this.handleTransitionComplete);

 playerSM.initialState = "stopped";
```

It's also possible to create hierarchical state machines using the argument "parent" in the addState method. This example shows the creation of a hierarchical state machine for the monster of a game (Its a simplified version of the state machine used to control the AI in the original Quake game)

```javascript
 var monsterSM = new StateMachine();
 monsterSM.addState("idle",{enter:this.onIdle, from:["smash", "punch", "missle attack"]});
 monsterSM.addState("attack",{enter:this.onAttack, from:"idle"});
 monsterSM.addState("melee attack",{parent:"attack", enter:this.onMeleeAttack, from:"attack"});
 monsterSM.addState("smash",{parent:"melee attack", enter:this.onSmash});
 monsterSM.addState("punch",{parent:"melee attack", enter:this.onPunch});
 monsterSM.addState("missle attack",{parent:"attack", enter:this.onMissle});
 monsterSM.addState("die",{enter:this.onDead, from:["smash", "punch", "missle attack"]});

 monsterSM.initialState = "idle";
```

### Install
* [npm](http://npmjs.org/): `npm install --save hierarchical-fsm`
* [Download](https://raw.githubusercontent.com/cassiozen/State-Machine/master/lib/StateMachine.js)

### Ports
* [ActionScript 3](https://github.com/cassiozen/State-Machine/tree/as3)
* [Dart](https://github.com/JesterXL/Dart-JXL-State-Machine)
* [Lua (Corona)](https://github.com/JesusEspejo/Lua-Corona-SDK-State-Machine)

### License

Copyright (c) 2009-16 Cássio M. Antonio

Released under the Open Source MIT license, which gives you the possibility to use it and modify it in every circumstance.
