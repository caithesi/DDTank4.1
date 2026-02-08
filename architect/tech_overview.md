# Technical Overview

This project is an open-source implementation of DDTank version 4.1, providing a complete server-client ecosystem. It includes a multi-component C# game server, an ASP.NET web API for client communication, and an Electron-based desktop client that wraps the original Flash-based game.

## Main Components

- **Source Server**: The core game logic written in C# (.NET Framework 4.5.2).
  - `Center.Server`: Handles central server logic and coordination.
  - `Fighting.Server`: Manages combat and battle instances.
  - `Game.Server`: Main game world logic and player management.
  - `SqlDataProvider`: Data access layer for SQL Server.
  - `Bussiness`: Shared business logic.
- **Request**: An ASP.NET web application (`Tank.Request`) that acts as the primary communication bridge between the game client and the server logic.
- **Web**: A PHP-based user portal (Registration, Login, Rankings) located in the `Web/` directory. It requires PHP 7.4 with the `sqlsrv` extension.
- **ClientWeb**: An Electron wrapper for the Flash client. It uses a local Express server to serve the game assets and integrates a Pepper Flash Player plugin.
- **Source Flash**: Contains the ActionScript source code and assets for the Flash-based game client.
- **Db**: Contains SQL Server database backups (`.BAK` files) and migration queries needed to set up the game database.

## Technologies

- **Server-side**: C#, .NET Framework 4.5.2, ASP.NET.
- **Database**: Microsoft SQL Server.
- **Client Shell**: Node.js, Electron, Express.
- **Game Client**: Adobe Flash (ActionScript).

## Development Conventions

- **Component Architecture**: The server is built on top of `Game.Base`, which provides the core networking and server management logic.
- **Data Access**: Data persistence is handled via the `SqlDataProvider` assembly, which interacts with SQL Server.
- **Scripting System**: 
  - **Server-side AI**: Game logic for NPCs and missions is implemented in C# within `Source Server/Game.Server.Scripts`.
  - **Hot-loading**: Logic in the scripts folder can often be synced or updated without a full recompile of the main server executable (see `EasyScript.bat`).
  - **Mission/NPC Logic**: Use classes inheriting from `ABrain` (for NPC AI) or mission-specific base classes.
- **Localization**: Localized strings are managed through the `LanguageMgr` system, typically loading from text files in the `Request/bin/Languages` or similar paths.
- **Communication Protocols**:
  - **Client-Request**: HTTP/XML for configuration and static data.
  - **Client-Server**: Persistent TCP Sockets for real-time gameplay.
  - **Inter-Server**: WCF/NetTCP bindings for communication between Center, Game, and Fighting servers.
- **Flash Client**: The original Flash source code is fully available in `Source Flash`, allowing for deep client-side customization.
