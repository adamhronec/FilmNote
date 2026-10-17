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

## Initiative

Make analog photography settings easy to record and review, so that a photographer can save the important information about each shot in less than 15 seconds.

## Epics

### Epic 1: Film Roll Management
Allow users to create and manage analog film rolls.

#### User Story 1
As a photographer, I want to create a new film roll so that I can organize shots taken on the same film.

**Tasks:**
- Create film roll data model
- Create "Add Film" screen (including film name, ISO and number of exposures)
- Display list of created film rolls

#### User Story 2
As a photographer, I want to see how many frames I have already used so that I know how many shots remain on the film.

**Tasks:**
- Add frame counter
- Display remaining frames
- Update counter when a new shot is added

### Epic 2: Shot Logging
Allow users to record camera settings and a reference photo for each analog shot.

#### User Story 3
As a photographer, I want to save the aperture and shutter speed used for a shot, with optional note, so that I can review the settings after developing the film.

**Tasks:**
- Create shot data model
- Add aperture, shutter speed selection and optional note
- Store shot settings with the selected film roll

#### User Story 4
As a photographer, I want to take a reference photo of the scene with my iPhone so that I can later identify which settings belong to each developed photograph.

**Tasks:**
- Add camera access and save a reference photo with the shot

### Epic 3: Light Meter
Provide an optional exposure assistant using the iPhone camera.

#### User Story 5
As a photographer, I want the app to estimate suitable exposure settings so that I can choose an appropriate aperture and shutter speed for my film.

**Tasks:**
- Access camera exposure data using AVFoundation
- Read camera exposure data and calculate recommended settings