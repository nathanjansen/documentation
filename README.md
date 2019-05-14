# Live Contracts specifications

### Note to Readers

The issues for each service can be found at the [GitHub issue tracker](https://github.com/legalthings/livecontracts-specs/issues). For additional information, see [LTO Network website](https://lto.network) and [community guide](https://docs.lto.network/project/).

To provide feedback, use this issue tracker or the communication methods listed on the website.

### Copyright Notice

Copyright © 2017-2019 LTO Network. All rights reserved.

You may use this specification, the documentation and tutorials under the [Creative Commons Attribution 4.0 International Public License](https://raw.githubusercontent.com/legalthings/livecontracts-specifications/master/LICENSE). Source code displayed in the tutorials is placed in [Public Domain](https://creativecommons.org/publicdomain/zero/1.0/deed).

## General

### Cryptography

Live Contracts uses the `SHA256` to create a cryptographic hashes. The `Blake2b256` and `Keccak256` hashing algorithms are used for creating public/secret key pairs. The `ED25519` scheme is applied to create and verify signatures. `X25519` is used to for asymmetric encryption. For symmetric encrypt use `AES256` in Galois/Counter Mode \(gcm\). `Base58` is used to create the string from of bytes.

{% page-ref page="advanced-topics/cryptography.md" %}

### Network

Live Contracts relies on message brokers to share event chains between nodes. The message broker MUST use the `AMQP 0-9-1` to communicate and SHOULD be available over a secured connection.

{% page-ref page="advanced-topics/network/" %}

## Key concepts

The Live Contracts specifications are described as [JSON schema](http://json-schema.org/).

### Event chain

The event chain is a miniature blockchain that is shared between parties involved in a contract or process. Each event is signed and that added referencing the previous event, forming a chain. All information of the system is derived from event chains.

{% page-ref page="key-concepts/event-chain-service/events/" %}

### Identity

An identity within the event chain. The identity is used for authentication and authorization. An identity is not a user, a user has an identity for each event chain it's participating in.

{% page-ref page="key-concepts/event-chain-service/identity.md" %}

### Scenario

A Live Contract scenario is a definition of procedure as a Finite State Machine \(FSM\). As an FSM, the scenario can be visualized as flowchart and instantiated as a process.

{% page-ref page="key-concepts/workflow-engine/scenario/" %}

#### Action

In a process an action may be performed to trigger a state change or to update the process projection. For each action in the scenario, the `$schema` property MUST be set which is used to execute an action of to display it correctly in the UI.

{% page-ref page="key-concepts/workflow-engine/scenario/action.md" %}

#### Actor

An actor is an identity or a group of identities that participate on a process. The actors are predefined in a scenario and instantiated for the process.

{% page-ref page="key-concepts/workflow-engine/scenario/actor.md" %}

#### Data instruction

Data instructions allow you to dynamically set properties of a state or actions when they are instantiated using data from the projected process.

{% page-ref page="key-concepts/workflow-engine/scenario/data-instruction.md" %}

### Process

A process is an instantation of a scenario. It is traversable, at any moment you are at a specific point in the process. A process is also a deterministic projection, generated by processing responses following the update instructions and transitions of the scenario.

{% page-ref page="key-concepts/workflow-engine/process.md" %}

### Response

Executing an action in a process always yields a response. This is regardless of whether the action is performed manually by the user of automatically by the node. A response may update the process projection and/or trigger a state transition.

{% page-ref page="key-concepts/workflow-engine/response.md" %}

## Node-to-node communication

### Chain request

A node may request a chain or a portion of a chain. When an identity is registers, a node might request the full event chain for that identity. If a node receives an event, but can't find the corresponding previous event, it will request the missing event.

{% page-ref page="advanced-topics/network/chain-request.md" %}

### Rejection

A node is required to validate if an event is valid before adding it to the event chain. Events that are invalid may be rejected.

{% page-ref page="advanced-topics/network/rejection.md" %}

### Conflict resolution

In any decentralized system conflicts can arise. Multiple nodes may add an event at the same time or a node might miss an event causing it to branch the chain. Because an event represents something that happened off-chain, we can't simply drop events instead they need to be added in such a way that it's visible that a conflict occurred.

{% page-ref page="advanced-topics/network/conflict-resolution.md" %}

