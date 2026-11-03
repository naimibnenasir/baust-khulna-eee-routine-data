# Routine data files

These are files for the public `baust-khulna-eee-routine-data` GitHub repository. The source is the July 2026 BAUST Khulna EEE class routine PDF, with the EEE 4A MATH 213 and EEE 217 changes supplied by the user. The section labels map to semesters as follows: EEE 1A = Level 1 Term 1, EEE 2A = Level 1 Term 2, EEE 3A = Level 2 Term 1, EEE 4A = Level 2 Term 2, and EEE 5A = Level 3 Term 1. The app uses the student's Firestore `level` and `term` fields to select a section. The PDF lists course codes rather than full course titles, so `subjectName` currently repeats each course code. The July 2026 semester dates and academic events in `config.json` come from the BAUSTK Academic Calendar 2026.

Each class object's `batch` field stores its routine section label (for example, `EEE 4A`). Keep the section labels as printed in the PDF; admission batch values such as `2nd` do not identify the routine section. Consecutive periods shown as one class are represented as a single session. The current JSON contains transcribed entries for all five sections: EEE 1A, EEE 2A, EEE 3A, EEE 4A, and EEE 5A. The July 2026 semester dates, holidays, class weeks, exams, preparatory leave, and result events have been added from the BAUSTK Academic Calendar 2026.

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
| `examSchedule` | array | Published exam entries; leave empty to keep the Exams tab hidden (see below) |
| `holidays` | array | Objects with a `date` (`YYYY-MM-DD`) and `name` |
| `academicEvents` | array | Objects with `startDate`, `endDate`, `name`, and `noClasses`; shown in the app calendar |
| `calendarNote` | string | A note shown below the calendar month grid |

Keep valid JSON syntax: use double quotes, commas between items, and no comma after the final item. Keep each class `id` unique. Upload both files to the repository's `main` branch root so they appear beside the repository README.


### Publishing an exam schedule

Add one object per exam to `examSchedule` in `config.json`. The Exams tab appears automatically when this array contains at least one entry. Each entry must include `date` (`YYYY-MM-DD`), `startTime` and `endTime` (`HH:mm`, 24-hour), `level`, `term`, `examType` (such as `Midterm` or `Final`), and `subjectCode`. `subjectName` is optional and defaults to the code. Do not include a room field. Entries are filtered for the signed-in student's level and term; completed exams are removed automatically. Keep the array empty when no exam routine is published.
