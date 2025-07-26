# Monopoly Game Documentation

Welcome to the documentation for the Monopoly Game web application. This document provides a more in-depth look at the game's architecture, core components, and how to extend its functionality.

## Table of Contents

- [Game Overview](#game-overview)
- [Core Game Logic (app.js)](#core-game-logic-appjs)
  - [MonopolyGame Class](#monopolygame-class)
  - [Properties Initialization](#properties-initialization)
  - [Board Rendering](#board-rendering)
  - [Player Actions](#player-actions)
  - [Modals and UI Updates](#modals-and-ui-updates)
- [Styling (style.css)](#styling-stylecss)
- [HTML Structure (index.html)](#html-structure-indexhtml)
- [Extending the Game](#extending-the-game)
  - [Adding New Properties](#adding-new-properties)
  - [Customizing Cards](#customizing-cards)
  - [Implementing New Features](#implementing-new-features)

## Game Overview

The Monopoly Game is a client-side web application built using HTML, CSS, and JavaScript. It simulates the classic board game, allowing multiple players to interact with a dynamic game board, manage properties, and compete to be the last player standing.

## Core Game Logic (app.js)

The `app.js` file contains the main game logic, encapsulated within the `MonopolyGame` class.

### MonopolyGame Class

The `MonopolyGame` class manages the entire game state, including:

- **`players`**: An array of player objects, each containing their ID, name, money, current position, owned properties, and color.
- **`currentPlayerIndex`**: Tracks whose turn it is.
- **`properties`**: An array defining all squares on the board, including their type (property, railroad, utility, tax, chance, community chest, go, jail, free parking, go-to-jail), price, rent, color group, and owner.
- **`freeParkingPot`**: Accumulates money from taxes and fines.
- **`lastRoll`**: Stores the result of the last dice roll.

### Properties Initialization

The `initializeProperties()` method sets up the game board with all the standard Monopoly squares. Each square is an object with specific attributes that determine its behavior.

### Board Rendering

`initializeBoard()` is responsible for dynamically creating the HTML elements for the game board based on the `properties` array. It also handles the positioning of players on the board.

### Player Actions

Key player actions are handled by methods such as:

- **`rollDice()` / `rollDiceWithDoubles()`**: Simulates dice rolls, moves the player, and checks for passing GO or landing on special squares. `rollDiceWithDoubles()` adds logic for consecutive doubles.
- **`handleSquareLanding()`**: Determines the action to take when a player lands on a specific square (e.g., buy property, pay rent, draw card, pay tax, go to jail, collect Free Parking).
- **`buyProperty()`**: Allows the current player to purchase an unowned property.
- **`payRent()`**: Calculates and transfers rent between players.
- **`endTurn()`**: Advances to the next player's turn.

### Modals and UI Updates

- **`showPropertyModal()`**: Displays detailed information about a property when clicked.
- **`showCardModal()`**: Shows the text of Chance or Community Chest cards.
- **`showInfoModal()`**: A generic modal for displaying game messages or confirmations.
- **`updateDisplay()`**: Refreshes the player information panel.
- **`addMessage()`**: Logs game events to the message log.

## Styling (style.css)

The `style.css` file provides all the visual styling for the game, including:

- Grid-based layout for the game board.
- Styling for individual squares, properties, and player tokens.
- Responsive design considerations.
- Visual cues for property colors, houses, and hotels.

## HTML Structure (index.html)

`index.html` is the main entry point of the application. It defines the basic layout of the game interface, including:

- The game board container (`.board`).
- Player information panels (`#players-info`).
- Dice display (`#dice1`, `#dice2`).
- Control buttons (`#rollDice`, `#buyProperty`, `#endTurn`).
- Message log (`#messageLog`).
- Modals for property details and game information.

## Extending the Game

The modular structure of the `MonopolyGame` class makes it relatively straightforward to extend or modify the game.

### Adding New Properties

To add new properties or modify existing ones, update the `initializeProperties()` array in `app.js`. Ensure you define all necessary attributes like `name`, `type`, `price`, `rent`, `color`, `houses`, and `owner`.

### Customizing Cards

The `drawCard()` method in `app.js` contains the logic for Chance and Community Chest cards. You can add, remove, or modify the `cards` array to introduce new card effects.

### Implementing New Features

For new features like building houses, trading, or mortgaging, you would typically:

1.  **Add UI elements** to `index.html` (e.g., buttons for building).
2.  **Implement new methods** within the `MonopolyGame` class in `app.js` to handle the game logic for the new feature.
3.  **Integrate the new methods** into existing game flow (e.g., call `buildHouse()` when a player clicks a build button).
4.  **Update styling** in `style.css` as needed.
