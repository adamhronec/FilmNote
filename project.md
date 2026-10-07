# FilmNote - Project Overview

## Problem
Analog photographers often forget which camera settings they used for a specific shot on film.

## Users
The primary user is me as an analog photographer, but the app can also be used by other film photography enthusiasts or beginners.

## MVP
The app will allow users to create a film roll and save individual shots with a reference photo of the scene, aperture, shutter speed, ISO, frame number and an optional note.

As an extension of the MVP, the app may include a simple light meter that uses the iPhone camera to suggest suitable exposure settings for the selected film ISO.

## Non-goals
The app will not include:
- photo editing or filters,
- social features or photo sharing,
- user accounts or online profiles,
- cloud synchronization between devices,

These features are outside the scope of the project because the main goal is to keep the application focused on recording photography settings and reviewing them after the film is developed.

## Technologies
- Swift – main programming language used to develop the iOS application.
- SwiftUI – used to create the user interface and application screens.
- SwiftData – used for local storage of film rolls, shots, camera settings, and notes.
- AVFoundation – used to access the iPhone camera and later support the optional light meter.
- Xcode – development environment used to build, run and test the application.
- Git / GitHub – used for version control.