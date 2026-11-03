# Routine data files

These are files for the public `baust-khulna-eee-routine-data` GitHub repository. The source is the July 2026 BAUST Khulna EEE class routine PDF. The section labels map to semesters as follows: EEE 1A = Level 1 Term 1, EEE 2A = Level 1 Term 2, EEE 3A = Level 2 Term 1, EEE 4A = Level 2 Term 2, and EEE 5A = Level 3 Term 1. The app uses the student's Firestore `level` and `term` fields to select a section. The PDF lists course codes rather than full course titles, so `subjectName` currently repeats each course code. The schedule does not state semester dates or a holiday list; the semester dates and holiday entries in `config.json` are still examples and must be replaced with the approved academic calendar.

Each class object's `batch` field stores its routine section label (for example, `EEE 2A`). Keep the section labels as printed in the PDF; admission batch values such as `2nd` do not identify the routine section. Consecutive periods shown as one class are represented as a single session. The current JSON contains the transcribed EEE 2A entries; other sections still need their entries added before students in those semesters will see a complete timetable.

## `routine.json` format

The top level is an object with a `classes` array. Each class object contains:

| Field | Type | Meaning / format |
|---|---|---|
| `id` | string | Unique stable ID for this class entry |
| `batch` | string | Routine section label, such as `EEE 2A`; selected using the student's level and term |
| `day` | string | English weekday, for example `Sunday` |
| `startTime` | string | 24-hour `HH:mm`, for example `09:00` |
| `endTime` | string | 24-hour `HH:mm`, for example `10:20` |
| `subjectCode` | string | Subject code, also used for its consistent color |
| `subjectName` | string | Display name |
| `room` | string | Room or lab name |
| `facultyName` | string | Faculty name displayed and searched |
| `type` | string | Exactly `theory` or `lab` |

## `config.json` format

The top level is an object with these fields:

| Field | Type | Meaning / format |
|---|---|---|
| `semesterName` | string | Label displayed in the app |
| `semesterStartDate` | string | Semester start date, `YYYY-MM-DD` |
| `semesterEndDate` | string | Semester end date, `YYYY-MM-DD` |
| `minAppVersion` | string | Minimum compatible app version |
| `latestVersion` | string | Latest app version for a later update checker |
| `apkUrl` | string | GitHub Releases page or APK link |
| `holidays` | array | Objects with a `date` (`YYYY-MM-DD`) and `name` |

Keep valid JSON syntax: use double quotes, commas between items, and no comma after the final item. Keep each class `id` unique. Upload both files to the repository's `main` branch root so they appear beside the repository README.
