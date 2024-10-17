# Multi-View Calendar

A customizable React calendar component that supports week and month views, event scheduling, and internationalization.

## Table of Contents

- [Installation](#installation)
- [Features](#features)
- [Usage](#usage)
  - [Basic Example](#basic-example)
  - [Custom Event Handling](#custom-event-handling)
- [API](#api)
  - [Props](#props)
- [Author](#author)
- [License](#license)

## Installation

Install the package using npm:

```bash
npm install multi-view-calendar
```

Or with Yarn:

```bash
yarn add multi-view-calendar
```

### Peer Dependencies

Ensure you have `react` and `react-dom` installed in your project:

```bash
npm install react react-dom
```

## Features

- **Multiple Views**: Switch between week and month views.
- **Event Management**: Add and delete events with ease.
- **Internationalization**: Supports various languages via the `lang` prop.
- **Customizable Rendering**: Customize event chips with `renderEventChip`.
- **TypeScript Support**: Fully typed for enhanced developer experience.

## Usage

### Basic Example

```tsx
import React, { useState } from "react";
import {
  CalendarProvider,
  useCalendar,
  MultiViewCalendar,
} from "multi-view-calendar";

const CalendarControls = () => {
  const { toggleViewMode, goToNext, goToPrevious, viewMode, viewLabel } =
    useCalendar();

  return (
    <div
      style={{
        display: "flex",
        justifyContent: "space-between",
        alignItems: "center",
        margin: "1rem 0",
      }}
    >
      <button
        onClick={toggleViewMode}
        style={{
          background: "#0092D4",
          color: "#FFF",
          padding: "0.5rem",
          border: "none",
          cursor: "pointer",
        }}
      >
        Switch to {viewMode === "week" ? "Month" : "Week"} View
      </button>
      <div style={{ display: "flex", alignItems: "center", marginTop: "1rem" }}>
        <button
          onClick={goToPrevious}
          style={{
            fontSize: "1.5rem",
            fontWeight: "bold",
            background: "none",
            border: "none",
            cursor: "pointer",
            color: "#0092D4",
          }}
        >
          {"<"}
        </button>
        <span
          style={{
            display: "block",
            padding: "0 0.25rem",
            textAlign: "center",
            fontSize: "1.125rem",
            fontWeight: "bold",
          }}
        >
          {viewLabel}
        </span>
        <button
          onClick={goToNext}
          style={{
            fontSize: "1.5rem",
            fontWeight: "bold",
            background: "none",
            border: "none",
            cursor: "pointer",
            color: "#0092D4",
          }}
        >
          {">"}
        </button>
      </div>
    </div>
  );
};

const App = () => {
  const [eventSchedule, setEventSchedule] = useState<{
    [key: string]: { value: string }[];
  }>({
    "2024-09-28": [{ value: "Meeting with John" }],
    "2024-09-29": [{ value: "Project deadline" }],
    "2024-09-30": [{ value: "Team stand-up" }],
  });

  return (
    <CalendarProvider>
      <CalendarControls />
      <MultiViewCalendar
        lang="en"
        eventSchedule={eventSchedule}
        setEventSchedule={setEventSchedule}
      />
    </CalendarProvider>
  );
};

export default App;
```

### Custom Event Handling

```tsx
import React, { useState } from "react";
import {
  CalendarProvider,
  useCalendar,
  MultiViewCalendar,
} from "multi-view-calendar";

const CalendarControls = () => {
  const { toggleViewMode, goToNext, goToPrevious, viewMode, viewLabel } =
    useCalendar();

  return (
    <div
      style={{
        display: "flex",
        justifyContent: "space-between",
        alignItems: "center",
        margin: "1rem 0",
      }}
    >
      <button
        onClick={toggleViewMode}
        style={{
          background: "#0092D4",
          color: "#FFF",
          padding: "0.5rem",
          border: "none",
          cursor: "pointer",
        }}
      >
        Switch to {viewMode === "week" ? "Month" : "Week"} View
      </button>
      <div style={{ display: "flex", alignItems: "center", marginTop: "1rem" }}>
        <button
          onClick={goToPrevious}
          style={{
            fontSize: "1.5rem",
            fontWeight: "bold",
            background: "none",
            border: "none",
            cursor: "pointer",
            color: "#0092D4",
          }}
        >
          {"<"}
        </button>
        <span
          style={{
            display: "block",
            padding: "0 0.25rem",
            textAlign: "center",
            fontSize: "1.125rem",
            fontWeight: "bold",
          }}
        >
          {viewLabel}
        </span>
        <button
          onClick={goToNext}
          style={{
            fontSize: "1.5rem",
            fontWeight: "bold",
            background: "none",
            border: "none",
            cursor: "pointer",
            color: "#0092D4",
          }}
        >
          {">"}
        </button>
      </div>
    </div>
  );
};

const ExampleUsage = () => {
  const [eventSchedule, setEventSchedule] = useState<{
    [key: string]: { value: string }[];
  }>({
    "2024-09-28": [{ value: "Meeting with John" }],
    "2024-09-29": [{ value: "Project deadline" }],
    "2024-09-30": [{ value: "Team stand-up" }],
  });

  const handleCustomEventDelete = ({
    event,
    eventIndex,
    eventDate,
    dateKey,
  }: {
    dateKey: string;
    event: { value: string };
    eventIndex: number;
    eventDate: Date;
  }) => {
    setEventSchedule((prevSchedule) => {
      const updatedEvents =
        prevSchedule[dateKey]?.filter((_, index) => index !== eventIndex) || [];
      return updatedEvents.length > 0
        ? { ...prevSchedule, [dateKey]: updatedEvents }
        : Object.fromEntries(
            Object.entries(prevSchedule).filter(([key]) => key !== dateKey)
          );
    });

    console.log(`Event deleted on ${eventDate}: ${event.value}`);
  };

  const handleCustomEventAdd = (date: Date, dateKey: string) => {
    const newEvent = {
      value: `Custom event on ${dateKey}`,
    };

    setEventSchedule((prevSchedule) => ({
      ...prevSchedule,
      [dateKey]: prevSchedule[dateKey]
        ? [...prevSchedule[dateKey], newEvent]
        : [newEvent],
    }));

    console.log(`Custom event added on ${date} with key ${dateKey}`);
  };

  return (
    <CalendarProvider>
      <CalendarControls />
      <MultiViewCalendar
        lang="en"
        eventSchedule={eventSchedule} // Pass the state directly to MultiViewCalendar
        setEventSchedule={setEventSchedule} // Pass the setter function for internal state updates
        onEventDelete={handleCustomEventDelete} // Optional
        onEventAdd={handleCustomEventAdd} // Optional
      />
    </CalendarProvider>
  );
};

export default ExampleUsage;
```

## API

### Props
| Prop                                  | Type                                                                                                                                       | Default | Description                                               |
|---------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|---------|-----------------------------------------------------------|
| `lang` (optional)                     | `string`                                                                                                                                   | `'en'`  | Language code for localization.                           |
| `eventSchedule`                       | `{ [key: string]: { value: string }[] }`                                                                                                   |         | The current event schedule.                               |
| `setEventSchedule`                    | `React.Dispatch<React.SetStateAction<{ [key: string]: { value: string }[] }>>`                                                             |         | Function to update the event schedule.                    |
| `onEventAdd` (optional)               | `(date: Date, dateKey: string) => void`                                                                                                    |         | Custom handler for adding events.                         |
| `onEventDelete` (optional)            | `(eventData: { event: { value: string }; eventIndex: number; eventDate: Date; dateKey: string }) => void`                                  |         | Custom handler for deleting events.                       |
| `renderEventChip` (optional)          | `({ event, eventIndex, eventDate }: { event: { value: string }; eventIndex: number; eventDate: Date }) => React.ReactNode`                 |         | Custom renderer for event chips.                          |
| `containerClasses` (optional)         | `string`                                                                                                                                   |         | Custom CSS classes for the main container.                |
| `calendarDayNameClasses` (optional)   | `string`                                                                                                                                   |         | Custom CSS classes for the day name headers.              |
| `calendarDayClasses` (optional)       | `string`                                                                                                                                   |         | Custom CSS classes for each day cell in the calendar.     |
| `dayNumberContainerClasses` (optional)| `string`                                                                                                                                   |         | Custom CSS classes for the day number container.          |
| `dayNumberClasses` (optional)         | `string`                                                                                                                                   |         | Custom CSS classes for the day number itself.             |
| `ChipsContainerClasses` (optional)    | `string`                                                                                                                                   |         | Custom CSS classes for the container holding event chips. |
| `customAddIcon` (optional)            | `React.ReactNode`                                                                                                                          |         | Custom icon component for the add event button.           |


## Author

[Mais Aburabie](https://www.linkedin.com/in/mais-aburabie-1501731b9)
