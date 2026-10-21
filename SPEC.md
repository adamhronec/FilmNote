# FilmNote – Project Specification

## 1. Project Overview

FilmNote is an iOS application designed for analog photographers who want to keep track of the camera settings used for individual shots on film.

Unlike digital photography, analog cameras do not automatically store metadata such as aperture, shutter speed, or shooting conditions. After a film is developed, the photographer may therefore not remember which settings were used for a specific photograph.

FilmNote solves this problem by allowing the photographer to create a digital record for each analog shot. The record contains a reference photo of the scene together with the camera settings used for the actual analog photograph.

The application is primarily designed for personal use but can also be used by other analog photography enthusiasts.

---

## 2. Problem

Analog photographers often forget which camera settings they used for a specific shot. Analog cameras do not automatically store photographic metadata.

---

## 3. Project Goal

The goal of FilmNote is to provide a quick and simple way to record analog photography settings while shooting and allow the photographer to review them later after the film has been developed.

The application should make recording a shot fast enough that it does not significantly interrupt the photography process.

---

## 4. Target Users

### Primary User

The primary user is an analog photographer who manually controls camera settings such as aperture and shutter speed.

The application is primarily designed around my own use of an analog camera.

### Secondary Users

Other film photography enthusiasts who want to:

- keep track of exposure settings,
- organize photographs by film roll,
- learn which settings produced good or bad results,
- compare developed photographs with the conditions in which they were taken.

The application is intended mainly for hobby photographers rather than professional studio workflows.

---

## 5. Main Use Case

A photographer loads a new film into an analog camera and creates a corresponding film roll in FilmNote.

While taking photographs, the photographer creates a new shot record in the application.

For each shot, the photographer:

1. takes a reference photo of the scene using the iPhone,
2. enters the aperture used on the analog camera,
3. enters the shutter speed,
4. optionally enters a note,
5. saves the shot.

The application automatically associates the shot with the currently selected film roll and assigns it a frame number.

After the analog film is developed, the photographer can open the film roll in FilmNote and compare the developed photographs with the saved settings and reference images.

---

## 6. Functional Requirements

### 6.1 Film Roll Management

The user must be able to create a new film roll.

Each film roll should contain:

- film name,
- ISO value,
- number of available exposures,
- creation date,
- list of recorded shots.

Example:

```text
Kodak Gold 200
ISO 200
36 exposures
12 / 36 used
```

The user should be able to view all created film rolls.

Each film roll should display basic information that allows the user to quickly identify it.

The user should be able to open a film roll and see all shots associated with it.

The application should automatically track the number of used and remaining frames.

### 6.2 Shot Logging

The user must be able to create a shot inside a selected film roll.

Each shot should contain:

- frame number,
- reference photo,
- aperture,
- shutter speed,
- ISO inherited from the film roll,
- optional note,
- date and time of creation.

Example:

```text
Frame 12

Reference photo

Aperture: f/5.6
Shutter speed: 1/250
ISO: 200

Note:
Sunny afternoon, subject in shade
```

The shot should automatically receive the next available frame number.

The user should not need to manually enter the film ISO for every shot because it is already defined by the selected film roll.

### 6.3 Reference Photo

The user should be able to take a reference photograph using the iPhone camera.

The photo should be stored together with the corresponding shot record.

### 6.4 Camera Settings

The user should be able to select commonly used aperture values.

Examples:

```text
f/2.8
f/4
f/5.6
f/8
f/11
f/16
```

The user should also be able to select commonly used shutter speeds.

Examples:

```text
1/30
1/60
1/125
1/250
1/500
1/1000
```

Using predefined values is preferred over free text because it makes recording a shot faster and reduces input errors.

### 6.5 Notes

The user should be able to add an optional text note to each shot.

The note can contain additional information that is not represented by the camera settings.

Notes are optional and should not be required before saving a shot.

---

## 7. Light Meter Extension

A simple light meter is planned as an extension of the MVP.

The light meter will use the iPhone camera and available exposure information to estimate appropriate exposure settings for the selected film ISO.

The user should be able to select or inherit the ISO from the currently active film roll.

The application can then suggest a suitable combination of:

- aperture,
- shutter speed.

Example:

```text
ISO 200

Recommended exposure:

f/4    1/500
f/5.6  1/250
f/8    1/125
```

If the light meter cannot be completed within the available development time, the main shot logging functionality must remain fully usable.

---

## 8. Basic User Flow

The main application flow should be:

```text
Launch App
    ↓
Film Roll List
    ↓
Select Film
    ↓
Film Detail
    ↓
Add Shot
    ↓
Take Reference Photo
    ↓
Select Aperture
    ↓
Select Shutter Speed
    ↓
Add Optional Note
    ↓
Save Shot
```

Creating a new film follows:

```text
Film Roll List
    ↓
Add Film
    ↓
Enter Film Information
    ↓
Save
    ↓
Film Detail
```

Optional light meter flow:

```text
Film Detail / Add Shot
    ↓
Light Meter
    ↓
Measure Scene
    ↓
Suggested Exposure
```

---

## 9. Data Model

The application requires two main data entities.

### FilmRoll

Possible properties:

```text
id
name
iso
totalFrames
creationDate
shots
```

Example:

```text
name: Kodak Gold 200
iso: 200
totalFrames: 36
creationDate: 21.10.2026
```

### Shot

Possible properties:

```text
id
frameNumber
aperture
shutterSpeed
referencePhoto
note
creationDate
filmRoll
```

Example:

```text
frameNumber: 12
aperture: f/5.6
shutterSpeed: 1/250
note: Subject in shade
filmRoll: Kodak Gold 200
```

The relationship is:

```text
FilmRoll
    1
    │
    │ contains
    ↓
    N
   Shot
```

One film roll can contain multiple shots.

Each shot belongs to one film roll.

---

## 10. Data Storage

Application data should be stored locally on the iPhone.

SwiftData will be used to persist structured data such as:

- films,
- ISO values,
- frame numbers,
- aperture,
- shutter speed,
- notes.

Reference photographs must also be stored locally and associated with the appropriate shot.

Internet access should not be required for the core functionality.

---

## 11. Device Features

### Camera

Required for taking reference photographs.

It may also be used by the optional light meter.

### Local Storage

Required for storing film rolls, shot settings and reference images.

### GPS

GPS is not part of the MVP.

It may later be added to automatically save the location where a photograph was taken.

---

## 12. Technologies

### Swift

Main programming language used for the iOS application.

### SwiftUI

Used to create the user interface and application screens.

### SwiftData

Used for local persistence of film rolls, shots and camera settings.

### AVFoundation

Used to access camera functionality and potentially retrieve exposure information for the light meter.

### Xcode

Development environment used to build, run, test and debug the application.

### Git

Used for version control.

### GitHub

Used to store the repository and manage development history.

---

## 13. Non-Goals

The first version of FilmNote will intentionally not include:

- photo editing or filters,
- social network functionality,
- public profiles,
- likes or comments,
- photo sharing platform functionality,
- cloud synchronization,
- automatic detection of camera settings from photographs,
- professional calibrated exposure measurement,
- advanced photography statistics.

These features are outside the main purpose of the application and would unnecessarily increase the complexity of the project.

---

## 14. Usability Requirements

Because FilmNote is intended to be used while actively taking photographs, the application should prioritize speed and simplicity.

The user should be able to record a shot using only a small number of interactions.

Frequently used settings should therefore use predefined selections rather than requiring manual text input.

The interface should:

- be simple and uncluttered,
- use clearly visible controls,
- minimize typing,
- show the current film and frame number clearly,
- allow fast selection of aperture and shutter speed,
- make the primary "Add Shot" action easy to access.

---

## 15. Permissions

The application will require camera permission.

The application should clearly explain why camera access is required:

> Camera access is used to capture a reference image for your analog photograph.

If GPS is added in the future, location permission will also be required.

The application should remain functional without GPS access.

---

## 16. Error and Edge Cases

The application should prevent or appropriately handle situations such as:

- attempting to add a shot when all film frames have already been used,
- camera permission being denied,
- saving a shot without selecting required exposure settings,
- leaving the optional note empty,
- deleting a film that contains existing shots.

The application should avoid losing saved shot information when it is closed and reopened.

---

## 17. MVP Success Criteria

The MVP can be considered complete when the user can:

1. create a film roll,
2. define its ISO and number of exposures,
3. open the film roll,
4. create a new shot,
5. capture a reference image,
6. save aperture and shutter speed,
7. optionally save a note,
8. automatically assign a frame number,
9. view previously recorded shots,
10. close and reopen the application without losing stored data.

The light meter is considered an additional feature and is not required for the core application to be functional.
