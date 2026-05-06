# html_timetable_manager

## Principal Workflow

The app stores all imported setup data in browser `localStorage`.

1. Use **Setup** to import the teacher list CSV and teacher grade-section subject mapping CSV.
2. Edit imported teachers or mappings directly in the CRUD tables, then click **Save Changes**.
3. Set timetable config: school days, periods per day, max periods per teacher, and AI prompt detail.
4. Use **AI Prompt** to generate/copy/download a prompt that asks an AI to produce a no-overlap timetable CSV.
5. Use **Upload Timetable** to import the AI-generated CSV.
6. Use **View Timetable** for class-wise, teacher-wise, and subject-wise views, plus overlap checks.

## Teacher List CSV

```csv
Teacher ID,Teacher Name,Subjects,Phone,Email
T001,Indira,"Maths; English",,
T002,Sai Priya,EVS,,
```

## Teacher Grade-Section Subject Mapping CSV

```csv
Teacher ID,Teacher Name,Grade-Section,Subject,Periods Per Week
T001,Indira,Grade-I-A,Maths,5
T002,Sai Priya,Grade-I-A,EVS,4
```

## CSV Upload Format

Use a CSV with columns like:

```csv
Class-Section,Day,P1,P2,P3,P4,P5,P6,P7,P8,P9,P10
```

Each period cell must follow:

```text
TeacherID:TeacherName:Subject
```

Separator rules:
- `:` between `TeacherID` and `TeacherName`
- `:` between `TeacherName` and `Subject`
- `-` between `Class` and `Section` (for example `Grade-I-A`)

## Excel Upload Formats

Supported Excel formats in the app:
- `Standard (Sheet-per-Class)`: One sheet per class, row-wise day timetable.
- `STATE TIME TABLE (19.07.2025)`: Teacher-wise matrix with day blocks and period numbers.

Before uploading an Excel file, choose the matching format from the Excel Format dropdown in the Upload section.

## Subject Mapping CSV (Teacher -> Subject)

You can upload a separate mapping CSV to auto-fill missing subjects.

Required columns:

```csv
Teacher Name,Teacher ID,Subject
```

Notes:
- At least one of `Teacher Name` or `Teacher ID` must be present.
- `Subject` is required.
- During timetable import, if a period has teacher info but no subject, the subject is auto-filled from this mapping.

## Timetable Cleanup and Standardization Requirements

### Formatting Corrections
- Remove extra spaces and unnecessary line breaks within cells.
- Ensure consistent spacing throughout the document.
- Remove duplicate rows (for example repeated Grade V A and Grade V B entries).
- Maintain uniform CSV-compatible formatting (comma-separated values).

### Naming Standardization
- Standardize teacher names (for example use `Shivathmika` consistently).
- Standardize subject names and capitalize properly (for example `EVS`, `Science`, `Maths`).
- Fix inconsistent grade-section labels.

### Class and Section Format
- Separate Class and Section using a hyphen (`-`).
- Examples:
  - `Grade-I-A`
  - `Grade-II-B`

### Teacher ID Generation
- Generate a unique Teacher ID for each teacher.
- Add the Teacher ID as a prefix before the teacher name.
- Each teacher must have only one unique ID across the entire timetable.

### Separator Rules (Important)
- Use this structure strictly: `TeacherID:TeacherName:Subject`
- `:` separates TeacherID and TeacherName
- `:` separates TeacherName and Subject
- `-` separates Class and Section
