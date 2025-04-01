# Go BitTorrent Client (Educational Skeleton)

This project provides a basic code structure and skeleton for building a BitTorrent client in the Go programming language. The primary goal is educational: to understand the fundamentals of the BitTorrent protocol (BEP-0003 and related) and practice concurrent network programming in Go.

**Current Time Context:** This README was generated around Tuesday, April 1, 2025 at 10:08 PM IST in Midnapore, West Bengal, India.

## Current Status

⚠️ **This is NOT a functional BitTorrent client.** ⚠️

This repository currently contains only the foundational structure:

* **Package organization:** Code is separated into logical packages (`torrent`, `tracker`, `peer`, `pieces`, `storage`).
* **Core data structures:** Basic Go structs are defined to represent torrent metadata, tracker responses, peer connections, pieces, and blocks.
* **Function/Method signatures:** Key functions and methods needed for the client's operation are outlined.
* **Minimal Implementation:** Only very basic elements (like Peer ID generation, some structure initialization, initial handshake attempt structure) might be present. Most core logic is missing.

**Missing Implementation:**

* Most Bencode parsing logic (`torrent/parser.go`).
* Tracker communication logic (HTTP requests, response parsing) (`tracker/tracker.go`).
* Peer Wire Protocol message serialization/deserialization and handling (`peer/protocol.go`, `peer/peer.go`).
* The main peer message loop (`peer.Peer.Run`).
* Piece selection strategy and management (`pieces/manager.go`).
* Block request/download coordination.
* Piece verification and assembly.
* Writing downloaded data to disk (`storage/storage.go`).
* Robust error handling and concurrency management (mutexes, etc.).
* Logging.

## Goal & Planned Features (Conceptual)

The structure is designed to eventually support the core functionalities of a simple BitTorrent download client:

* Parsing `.torrent` metadata files.
* Communicating with HTTP trackers to discover peers.
* Establishing TCP connections with peers.
* Performing the BitTorrent handshake.
* Implementing the Peer Wire Protocol messages (Choke, Unchoke, Interested, Not Interested, Have, Bitfield, Request, Piece, Cancel).
* Managing the state of pieces and blocks (needed, requested, downloaded).
* Requesting blocks from peers.
* Receiving and verifying downloaded pieces against SHA-1 hashes.
* Assembling verified pieces and writing them to disk.

Advanced features like UDP trackers, DHT, Magnet Links, Peer Exchange (PEX), encryption (MSE), and uploading are **not** part of the current basic structure.

## Project Structure

```text
bittorrent-client/
├── main.go                 # Entry point, CLI handling, initialization
│
├── torrent/                # .torrent file parsing and representation
│   ├── torrent.go
│   └── parser.go
│
├── tracker/                # Tracker communication (HTTP/UDP)
│   └── tracker.go
│
├── peer/                   # Peer connection, state, and protocol implementation
│   ├── peer.go
│   ├── protocol.go
│   └── manager.go          # (Optional) Manages peer pool
│
├── pieces/                 # Piece/block management and download strategy
│   ├── pieces.go
│   └── manager.go
│
├── storage/                # Writing verified data to disk
│   └── storage.go
│
├── client/                 # Optional: Central coordinating component
│   └── client.go
│
└── utils/                  # Common utilities (Peer ID generation, etc.)
    └── utils.go
